# Chapter 5: Introduction to Netmiko

Up until now, our scripts have executed locally, processing fake offline data. To automate a network, we must log into devices. While standard Python libraries like `telnetlib` or `paramiko` exist, they require handling all the manual complexities of network prompts (e.g. `Router>`, `Router#`, `More--`). 

Enter **Netmiko**, created by Kirk Byers. Netmiko simplifies SSH connections to network devices by automatically handling the login sequence, pagination, and prompt discovery. In this chapter, we will leverage the extensive examples from the `netmiko_course`.

## Section 5.1: Connecting to a Device

The foundational object in Netmiko is the `ConnectHandler`. You instantiate a `ConnectHandler` object by passing in the necessary connection parameters.

### Code Example: `simple_conn.py`

```python
import os
from getpass import getpass
from netmiko import ConnectHandler

# Fallback to getpass() if the environment variable is not set
password = os.getenv("NETMIKO_PASSWORD") if os.getenv("NETMIKO_PASSWORD") else getpass()

net_connect = ConnectHandler(
    device_type="cisco_ios",
    host="cisco3.lasthop.io",
    username="pyclass",
    password=password,
)

# find_prompt() returns the current router prompt (e.g., 'cisco3#')
print(net_connect.find_prompt())

# Always close the SSH session gracefully
net_connect.disconnect()
```

### Line-by-Line Breakdown
- **`from netmiko import ConnectHandler`**: Imports the primary connection class.
- **`getpass()`**: A built-in Python module that prompts the user for a password but hides the keystrokes on the screen. Hardcoding passwords in scripts is a massive security risk!
- **`device_type="cisco_ios"`**: *Crucial*. This tells Netmiko exactly what SSH algorithms, prompt patterns, and terminal settings to expect. (e.g., `cisco_nxos`, `juniper_junos`, `arista_eos`).
- **`net_connect.find_prompt()`**: Queries the device and returns the active prompt, proving you have successfully logged in.

## Section 5.2: Dictionary Unpacking

As seen in Chapter 4, passing many arguments into a function can get messy. Network engineers prefer storing device parameters in Dictionaries and using the `**` unpacking operator.

### Code Example: `simple_conn_dict.py`

This script (and the accompanying `exercise2.py`) demonstrates this best practice:

```python
from netmiko import ConnectHandler
from getpass import getpass

password = getpass()

my_device = {
    "device_type": "cisco_nxos",
    "host": "nxos1.lasthop.io",
    "username": "pyclass",
    "password": password,
}

net_connect = ConnectHandler(**my_device)
print(net_connect.find_prompt())
net_connect.disconnect()
```

By defining `my_device` as a dictionary, we can easily pull these dictionaries from databases or YAML files (like an Ansible inventory) and map them dynamically.

## Section 5.3: Context Managers and Session Logging

Instead of manually calling `net_connect.disconnect()`, Python provides "Context Managers" using the `with` statement. When the indented block finishes, Python automatically tears down the SSH connection.

Additionally, troubleshooting scripts can be difficult. Netmiko natively supports Session Logging to record every interaction payload.

### Code Example: `exercise3.py`

```python
import os
from netmiko import ConnectHandler
from getpass import getpass

password = os.getenv("NETMIKO_PASSWORD") if os.getenv("NETMIKO_PASSWORD") else getpass()

device = {
    "device_type": "cisco_nxos",
    "host": "nxos1.lasthop.io",
    "username": "pyclass",
    "password": password,
    # Netmiko will write all SSH I/O trace to this file
    "session_log": "nxos1.out",
}

# The 'with' statement acts as the context manager
with ConnectHandler(**device) as net_connect:
    print(net_connect.find_prompt())
# net_connect is automatically disconnected here!
```

- **`"session_log": "nxos1.out"`**: Appending this key to the dictionary instructs Netmiko to output all raw SSH reads/writes to `nxos1.out`. This is invaluable when debugging why a command failed natively. 

In the final chapter, we will combine these fundamentals—Data Types, Control Flow, and Netmiko—into Production-Ready, automated network workflows.
