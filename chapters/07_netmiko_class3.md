# Part 2: Netmiko Deep Dive
# Chapter 7: Advanced Timing and Data Parsing (Class 3)

The single biggest jump in Network Automation maturity is moving from reading raw strings to parsing structured data. When a router outputs a routing table, it's just a wall of text. We want that wall of text converted into a Python Dictionary!

In Chapter 7, using scripts from `netmiko_course/class3`, we first learn how to handle unpredictable command timing, and then we unleash three massive parsing engines: TextFSM, Genie, and TTP.

---

## Section 7.1: Advanced Timing (`show_timing.py`, `exercise1.py`, `exercise2.py`)

Sometimes, standard `send_command` fails because the router throws unexpected prompts or takes an unpredictable amount of time to return data without triggering a clear "prompt" ending.

### Deep Dive Q&A
**What is `send_command_timing()`?**
Unlike standard `send_command()` which aggressively hunts for a strict trailing router prompt (e.g., `#`), `send_command_timing()` is pattern-agnostic. It fires the command and then waits a specific amount of time (usually 2 seconds). If it doesn't see any new data populating on the screen for 2 full seconds, it simply assumes the command is finished and returns whatever it captured!

**Why would we use this?**
If a router drops privileges from `#` to `>`, or if it asks a Yes/No question `[confirm]`, the strict prompt never appears, causing `send_command` to freeze. Timing commands bypass this by merely watching for terminal "silence".

### Code Example: `show_timing.py`

```python
#!/usr/bin/env python
import os
from netmiko import ConnectHandler
from getpass import getpass

password = os.getenv("NETMIKO_PASSWORD") if os.getenv("NETMIKO_PASSWORD") else getpass()

my_device = {"device_type": "cisco_ios", "host": "cisco3.lasthop.io", "username": "pyclass", "password": password}
net_connect = ConnectHandler(**my_device)

# Send Command Timing waits for silence, ignoring the trailing prompt!
output = net_connect.send_command_timing("show ip int brief")
print(output)
net_connect.disconnect()
```

### Exercise 2: Massive Data Pulls with Timing

**Objective:** Use `send_command_timing` to pull a giant `show tech-support`, increasing the silence delay (`last_read`) to 10 seconds to account for router lag.

```python
#!/usr/bin/env python
import os
from datetime import datetime
from getpass import getpass
from netmiko import ConnectHandler

password = os.getenv("NETMIKO_PASSWORD") if os.getenv("NETMIKO_PASSWORD") else getpass()

device = {"host": "cisco3.lasthop.io", "username": "pyclass", "password": password, "device_type": "cisco_xe"}

ssh_conn = ConnectHandler(**device)

start_time = datetime.now()

# last_read=10 means "Wait until 10 straight seconds of silence before assuming we are done"
output = ssh_conn.send_command_timing(
    "show tech-support", 
    last_read=10, 
    read_timeout=180, 
    strip_prompt=False
)

end_time = datetime.now()
ssh_conn.disconnect()
print(f"Exec time: {end_time - start_time}")
```

---

## Section 7.2: TextFSM Parsing (`show_textfsm.py` & `exercise3.py`)

TextFSM uses regular expressions to rip apart router text walls and assemble them into beautiful Python Lists containing Dictionaries. NTC-Templates is a massive open-source repository containing TextFSM templates for nearly every vendor.

### Deep Dive Q&A
**How do we use TextFSM in Netmiko?**
Incredibly easily. Netmiko natively integrates! You just add `use_textfsm=True` to your command!

**What does it return?**
Instead of returning a String `\\nFastEthernet0/0 10.1.1.1 UP UP`, it returns a beautiful structure mapping the headers to the data: `[ {'interface': 'FastEthernet0/0', 'ipaddr': '10.1.1.1', 'status': 'up'} ]`.

### Code Example & Exercise: Parsed iteration

**Objective:** Issue `show vlan` on an Arista switch, parse it with TextFSM, and mathematically loop through the dictionary to find VLAN 7.

```python
#!/usr/bin/env python
import os
from pprint import pprint
from getpass import getpass
from netmiko import ConnectHandler

password = os.getenv("NETMIKO_PASSWORD") if os.getenv("NETMIKO_PASSWORD") else getpass()

arista1 = {"device_type": "arista_eos", "host": "arista1.lasthop.io", "username": "pyclass", "password": password}

with ConnectHandler(**arista1) as net_connect:
    # use_textfsm=True translates string walls into Dictionary Lists!
    show_vlan = net_connect.send_command("show vlan", use_textfsm=True)

    pprint(show_vlan)

    # Since it is a Python List of Dictionaries, we can loop over it!
    for vlan_dict in show_vlan:
        if vlan_dict["vlan_id"] == "7":
            print(f"\\nVLAN ID is {vlan_dict['vlan_id']} and name is {vlan_dict['vlan_name']}")
```

---

## Section 7.3: Genie and TTP (`show_genie.py`, `show_ttp.py`, `exercise4.py`)

TextFSM isn't the only parser. Cisco developed **Genie** (which returns massively nested dictionaries instead of lists). Another popular engine is **TTP** (Template Text Parser), which is much easier to write custom templates for than TextFSM.

### Deep Dive Q&A
**How do I use Genie?**
Exactly like TextFSM! Add `use_genie=True`.

**How does TTP differ?**
With TTP, you write a `.ttp` file that looks exactly like the router output, wrapping the target variables in double curley braces `{{ variable_name }}`. Netmiko requires you specify `use_ttp=True` and pass the path to your template `ttp_template="my_template.ttp"`.

### Genie Code Example (`exercise4.py` snippet)

```python
#!/usr/bin/env python
import os
from netmiko import ConnectHandler
from getpass import getpass

password = os.getenv("NETMIKO_PASSWORD") if os.getenv("NETMIKO_PASSWORD") else getpass()
my_device = {"device_type": "cisco_nxos", "host": "nxos1.lasthop.io", "username": "pyclass", "password": password}

with ConnectHandler(**my_device) as net_connect:
    output = net_connect.send_command("show lldp neighbors detail", use_genie=True)
    
    # Navigating Genie's deeply nested dictionaries
    output = output["interfaces"]
    for intf_name, v in output.items():
        neighbor_dict = v["port_id"][intf_name]["neighbors"]
        for neighbor_name, neighbor_data in neighbor_dict.items():
            print(f"Neighbor: {neighbor_name} | IP: {neighbor_data['management_address_v4']}")
```

### TTP Code Example (`show_ttp.py`)

```python
#!/usr/bin/env python
from pprint import pprint
# ... (standard setup logic) ...

# TTP requires both the flag and the path to the template file!
output = net_connect.send_command(
    "show run", 
    use_ttp=True, 
    ttp_template="show_run_intf.ttp"
)
pprint(output)
```

In Chapter 8 (Class 4), we move past read-only commands and learn how to safely and modularly push Configuration Changes down to live devices.
