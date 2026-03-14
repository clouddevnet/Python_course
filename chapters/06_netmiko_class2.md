# Part 2: Netmiko Deep Dive
# Chapter 6: Command Execution & Timing (Class 2)

Connecting to a router (Chapter 5) is only the first step. The true power of Network Automation lies in securely sending operational check commands (`show ip int brief`, `show arp`, `traceroute`) and parsing the router's response.

In Chapter 6, we use the `netmiko_course/class2` scripts to learn how to dispatch commands, loop over multiple network devices, and handle commands that take a long time to return data.

---

## Section 6.1: Looping Connections Over Multiple Devices (`conn_mult_devices.py` & `exercise1.py`)

A single `ConnectHandler` manages a single device. To scan your network, you must mathematically iterate over a collection of dictionaries.

### Deep Dive Q&A
**Why do we build a Tuple `(arista1, arista2)` to loop over instead of a List `[arista1, arista2]`?**
Functionally, both work exactly the same in a `for` loop. However, Tuples are computationally faster in Python because they are immutable (cannot be changed once created). Since our list of target routers is static for the duration of the script, a Tuple is slightly more efficient.

**What happens if `arista2` fails to connect?**
If `arista2` is offline, it will throw a `NetmikoTimeoutException`, which will completely crash the entire script! `arista3` and `arista4` will never be scanned. This is exactly why we use `try/except` (Chapter 3) in production scripts.

### Code Example: `conn_mult_devices.py`

```python
#!/usr/bin/env python
import os
from netmiko import ConnectHandler
from getpass import getpass

password = os.getenv("NETMIKO_PASSWORD") if os.getenv("NETMIKO_PASSWORD") else getpass()

cisco3 = {"device_type": "cisco_ios", "host": "cisco3.lasthop.io", "username": "pyclass", "password": password}
nxos1 = {"device_type": "cisco_nxos", "host": "nxos1.lasthop.io", "username": "pyclass", "password": password}
arista1 = {"device_type": "arista_eos", "host": "arista1.lasthop.io", "username": "pyclass", "password": password}

# Loop over a tuple of Dictionary connection templates
for device in (cisco3, nxos1, arista1):
    net_connect = ConnectHandler(**device)
    print(net_connect.find_prompt())
    net_connect.disconnect()
```

### Exercise 1: Looping and Catching ARP

**Objective:** Write a script that logs into 4 Arista switches, grabs their prompt, and issues `show ip arp`.

```python
#!/usr/bin/env python
import os
import logging
from getpass import getpass
from netmiko import ConnectHandler

# Enable raw Netmiko SSH debug logging to a text file
logging.basicConfig(filename="test.log", level=logging.DEBUG)
logger = logging.getLogger("netmiko")

password = os.getenv("NETMIKO_PASSWORD") if os.getenv("NETMIKO_PASSWORD") else getpass()

arista1 = {"device_type": "arista_eos", "host": "arista1.lasthop.io", "username": "pyclass", "password": password}
arista2 = {"device_type": "arista_eos", "host": "arista2.lasthop.io", "username": "pyclass", "password": password}
arista3 = {"device_type": "arista_eos", "host": "arista3.lasthop.io", "username": "pyclass", "password": password}
arista4 = {"device_type": "arista_eos", "host": "arista4.lasthop.io", "username": "pyclass", "password": password}

for device in (arista1, arista2, arista3, arista4):
    with ConnectHandler(**device) as net_connect:
        device_name = net_connect.find_prompt()
        
        # Send the command and capture the massive text wall
        output = net_connect.send_command("show ip arp")
        
        print(f"\\nDevice: {device_name}:")
        print(output)
        print()
```

---

## Section 6.2: `send_command` and Modifying Expect Strings (`expect_str.py`, `show_command.py`, `exercise2.py`)

When you use `.send_command("show ip route")`, Netmiko automatically presses Enter (`\\n`), waits for the router to compile the data, and importantly, **keeps reading the data stream until it sees the router prompt return** (e.g., `router#`).

### Deep Dive Q&A
**What if the command changes my prompt?**
If you send `disable` to a Cisco router, your prompt drops from `router#` to `router>`. Netmiko, by default, will sit there infinitely waiting for `router#` to return (because Netmiko read that as your prompt when it connected). To stop the script from hanging forever, we override Netmiko's brain using `expect_string=r">"`.

**What is `r"#"`?**
The little `r` stands for "Raw String". It tells Python to treat the string exactly as written and ignore special escape characters like `\\n` or `\\t`. It is best practice when sending regex characters or prompts.

### Code Example: `expect_str.py`

```python
#!/usr/bin/env python
import os
from netmiko import ConnectHandler
from getpass import getpass

password = os.getenv("NETMIKO_PASSWORD") if os.getenv("NETMIKO_PASSWORD") else getpass()

my_device = {
    "device_type": "cisco_ios",
    "host": "cisco3.lasthop.io",
    "username": "pyclass",
    "password": password,
}

net_connect = ConnectHandler(**my_device)

# Provide an explicit string for Netmiko to hunt for instead of the prompt
output = net_connect.send_command("show ip int brief", expect_string=r"#")
print(output)
net_connect.disconnect()
```

### Exercise 2: Dropping Privileges

**Objective:** Connect to a Cisco XE router, note the prompt, issue the `disable` command, use `expect_string` to catch the prompt dropping down to `>`, and print both prompts.

```python
#!/usr/bin/env python
import os
from getpass import getpass
from netmiko import ConnectHandler

password = os.getenv("NETMIKO_PASSWORD") if os.getenv("NETMIKO_PASSWORD") else getpass()

cisco3 = {"device_type": "cisco_xe", "host": "cisco3.lasthop.io", "username": "pyclass", "password": password}

with ConnectHandler(**cisco3) as net_connect:
    start_prompt = net_connect.find_prompt()

    # net_connect.send_command("disable") # WILL FAIL (hangs waiting for '#')
    
    # Working with expect_string
    net_connect.send_command("disable", expect_string=r">")

    end_prompt = net_connect.find_prompt()
    
    print(f"\\nStarting prompt: {start_prompt}")
    print(f"\\nEnding prompt: {end_prompt}")
    print()
```

---

## Section 6.3: Handling Timeouts (`traceroute_long.py`, `exercise3.py`, `exercise4.py`)

Netmiko's `send_command()` does not wait forever. By default, it gives up (times out) after an internal countdown if the prompt never returns. Some commands, like massive `show tech-support` outputs or a long DNS-failing `traceroute`, naturally take 2 to 3 minutes to return!

### Deep Dive Q&A
**How do we prevent Netmiko from crashing if we expect the command to take 3 minutes?**
We use the `read_timeout` modifier! Usually, `.send_command("traceroute 8.8.8.8", read_timeout=180)` tells Netmiko, "You are absolutely forbidden from crashing or complaining until you have waited exactly 180 seconds."

**What if it still fails?**
We explicitly import `ReadTimeout` from `netmiko` and wrap the command in a `try/except` block (Chapter 3 logic!). If the timer strikes 0, Python gracefully jumps to our `except` block, preventing the entire automation pipeline from catastrophically dying.

### Code Example & Exercise (3/4 combined)

**Objective:** Combine datetime logging, `read_timeout`, and `try/except` blocks to handle a massive `show tech-support` data pull cleanly.

```python
#!/usr/bin/env python
import os
from datetime import datetime
from getpass import getpass
from netmiko import ConnectHandler, ReadTimeout

password = os.getenv("NETMIKO_PASSWORD") if os.getenv("NETMIKO_PASSWORD") else getpass()

device = {"host": "cisco3.lasthop.io", "username": "pyclass", "password": password, "device_type": "cisco_xe"}

try:
    ssh_conn = ConnectHandler(**device)
    start = datetime.now()
    
    # Force Netmiko to patiently wait up to 3 minutes for the data
    show_tech = ssh_conn.send_command("show tech-support", read_timeout=180)
    print("\\nCommand Succeeded.\\n")
    
except ReadTimeout:
    print("\\nProgram failed with ReadTimeout Exception. The router took too long!\\n")
    
finally:
    # Always runs!
    end = datetime.now()

try:
    ssh_conn.disconnect()
except Exception:
    pass

print(f"\\nExecution time: {end - start}\\n")
```

In Chapter 7, we tackle Netmiko Class 3: TextFSM parsing. We will move away from reading giant, useless "walls of text" string data, and start compiling router outputs into beautiful, native Python Lists and Dictionaries automatically!
