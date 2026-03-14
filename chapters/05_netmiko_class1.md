# Part 2: Netmiko Deep Dive
# Chapter 5: Introduction to Netmiko (Class 1)

Welcome to Part 2! Here we pivot from raw Python theory into fully operational Network Automation using Kirk Byers' incredible **Netmiko** library. Netmiko simplifies SSH connections to network devices, handling prompts, paging, and vendor-specific quirks automatically.

In Chapter 5, we cover the exact scripts from `netmiko_course/class1` focusing entirely on establishing basic connections securely.

---

## Section 5.1: The Basic ConnectHandler (`simple_conn.py` & `exercise1.py`)

Netmiko's primary engine is the `ConnectHandler` class. You feed it connection parameters, and it returns a live SSH tunnel object.

### Deep Dive Q&A
**Why use `os.getenv("NETMIKO_PASSWORD")` and `getpass()`?**
You should *never* type your password directly into a script (hardcoding). It is a massive security violation. The `os.getenv()` checks your computer's hidden environment variables for a password. If it isn't set, the `getpass()` function activates, which pauses the script and securely blanks out your terminal while you manually type the password.

**What is `device_type`?**
Netmiko supports dozens of vendors. By specifying `cisco_ios` or `cisco_nxos`, Netmiko automatically knows how to handle Cisco's specific `--- more ---` paging, privilege exec prompts, and terminal length settings!

**What does `find_prompt()` do?**
It simply returns the current prompt the SSH session is sitting at (e.g., `router1#`). It proves you are successfully logged in.

### Code Example: `simple_conn.py`

```python
#!/usr/bin/env python
import os
from getpass import getpass
from netmiko import ConnectHandler

# Code so automated tests will run properly
# Check for environment variable, if that fails, use getpass().
password = os.getenv("NETMIKO_PASSWORD") if os.getenv("NETMIKO_PASSWORD") else getpass()

net_connect = ConnectHandler(
    device_type="cisco_ios",
    # device_type="invalid",
    host="cisco3.lasthop.io",
    username="pyclass",
    password=password,
)
print(net_connect.find_prompt())
```

### Exercise 1: Connecting to NX-OS

**Objective:** Write the same connection script but target a Cisco Nexus operating system.

```python
#!/usr/bin/env python
import os
from netmiko import ConnectHandler
from getpass import getpass

# Code so automated tests will run properly
password = os.getenv("NETMIKO_PASSWORD") if os.getenv("NETMIKO_PASSWORD") else getpass()

net_connect = ConnectHandler(
    device_type="cisco_nxos",
    host="nxos1.lasthop.io",
    username="pyclass",
    password=password,
)

print(net_connect.find_prompt())
```

---

## Section 5.2: Dictionary Unpacking (`simple_conn_dict.py` & `exercise2.py`)

Passing four or five arguments directly into `ConnectHandler()` isn't programmatic. If you are looping over a list of 100 routers, you want to store their profiles in Dictionaries.

### Deep Dive Q&A
**What is `**my_device` doing?**
Remember Python Keyword Unpacking from Chapter 4! Netmiko's `ConnectHandler` accepts keyword arguments. By passing a dictionary preceded by double asterisks `**`, Python instantly explodes the dictionary, feeding the `device_type`, `host`, `username`, and `password` variables natively into the function.

**Why are we calling `.disconnect()` now?**
When you script finishes, Python usually destroys the SSH object anyway. However, explicitly calling `net_connect.disconnect()` is a best practice. It actively tells the router to close the VTY line gracefully, preventing terminal session exhaustion on the device.

### Code Example: `simple_conn_dict.py`

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
print(net_connect.find_prompt())
net_connect.disconnect()
```

### Exercise 2: Dictionary Unpacking for NX-OS

**Objective:** Combine Exercise 1 and the dictionary logic to connect to `nxos1.lasthop.io`.

```python
#!/usr/bin/env python
import os
from netmiko import ConnectHandler
from getpass import getpass

password = os.getenv("NETMIKO_PASSWORD") if os.getenv("NETMIKO_PASSWORD") else getpass()

device = {
    "device_type": "cisco_nxos",
    "host": "nxos1.lasthop.io",
    "username": "pyclass",
    "password": password,
}
net_connect = ConnectHandler(**device)
print(net_connect.find_prompt())
net_connect.disconnect()
```

---

## Section 5.3: Context Managers and Session Logging (`simple_conn_cm.py`, `simple_conn_slog.py`, & `exercise3.py`)

Netmiko provides incredibly powerful advanced features right out of the box.

### Deep Dive Q&A
**Why use a `with` Context Manager for Netmiko?**
In Chapter 2, we used Context Managers `with open(filename)` to ensure local text files were securely closed even if the script crashed. Netmiko's `ConnectHandler` strongly supports Context Managers too! When the `with` block finishes (or if the script crashes midway), Netmiko cleanly executes the `.disconnect()` protocol automatically!

**What is `session_log`?**
This is perhaps Netmiko's greatest native feature. By merely adding `"session_log": "my_file.txt"` into your device dictionary, Netmiko will record *every single byte* transmitted over the SSH session directly to a text file. It is a perfect audit trail of exactly what you typed and exactly what the router returned.

### Code Example: Context Managers

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

# The 'with' block manages the connection entirely
with ConnectHandler(**my_device) as net_connect:
    print(net_connect.find_prompt())

# It safely disconnects here
print("Hello")
```

### Code Example: Session Logging

```python
#!/usr/bin/env python
import os
import time
from getpass import getpass
from netmiko import ConnectHandler

password = os.getenv("NETMIKO_PASSWORD") if os.getenv("NETMIKO_PASSWORD") else getpass()

time.sleep(4)

net_connect = ConnectHandler(
    device_type="cisco_ios",
    host="cisco3.lasthop.io",
    username="pyclass",
    password=password,
    session_log="cisco3.out",  # Outputs entire session!
)
print(net_connect.find_prompt())
output = net_connect.send_command("show ip int brief")
print(output)
net_connect.disconnect()
```

### Exercise 3: Putting it all together

**Objective:** Connect to `nxos1.lasthop.io` gracefully using a Dictionary, a Context Manager (`with`), AND log the session.

```python
#!/usr/bin/env python
import os
from netmiko import ConnectHandler
from getpass import getpass

password = os.getenv("NETMIKO_PASSWORD") if os.getenv("NETMIKO_PASSWORD") else getpass()

device = {
    "device_type": "cisco_nxos",
    "host": "nxos1.lasthop.io",
    "username": "pyclass",
    "password": password,
    "session_log": "nxos1.out",
}
with ConnectHandler(**device) as net_connect:
    print(net_connect.find_prompt())
```

In Chapter 6, we will advance to Class 2 of the Netmiko course, where we learn how to definitively send configuration commands and deal with network latency using timing controls.
