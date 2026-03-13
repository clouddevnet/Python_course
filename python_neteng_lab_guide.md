# Python for Network Engineers: Complete Lab Guide
## From Zero to Network Automation — A Comprehensive, Multi-Source Reference

---

**Sources Cross-Referenced in This Guide:**

| Abbreviation | Source | Focus |
|---|---|---|
| **LPTHW** | *Learn Python the Hard Way* (Zed Shaw) | Fundamentals via repetition |
| **PyNEng** | *Python for Network Engineers* (Natasha Samoylenko) | Python + networking context |
| **KByers** | *Python Course* (Kirk Byers — python_course_mar26) | Security automation (Check Point) |
| **Netmiko** | *Netmiko Course* (Kirk Byers — netmiko_course) | SSH device automation |

**How to Use This Guide:** Each chapter teaches a concept, shows code from multiple authors side by side, and ends with 5 lab tasks. All answers are in **Appendix A** at the end.

---

# TABLE OF CONTENTS

- [Chapter 1: Environment Setup & First Steps](#chapter-1-environment-setup--first-steps)
- [Chapter 2: Variables, Numbers, and Math](#chapter-2-variables-numbers-and-math)
- [Chapter 3: Strings and Text Processing](#chapter-3-strings-and-text-processing)
- [Chapter 4: Lists](#chapter-4-lists)
- [Chapter 5: Dictionaries](#chapter-5-dictionaries)
- [Chapter 6: Tuples, Sets, and Booleans](#chapter-6-tuples-sets-and-booleans)
- [Chapter 7: Conditionals (if/elif/else)](#chapter-7-conditionals-ifelifelse)
- [Chapter 8: Loops (for and while)](#chapter-8-loops-for-and-while)
- [Chapter 9: Functions](#chapter-9-functions)
- [Chapter 10: Working with Files](#chapter-10-working-with-files)
- [Chapter 11: Working with CSV, JSON, and YAML](#chapter-11-working-with-csv-json-and-yaml)
- [Chapter 12: Error Handling (try/except)](#chapter-12-error-handling-tryexcept)
- [Chapter 13: Modules and Packages](#chapter-13-modules-and-packages)
- [Chapter 14: Useful Built-in Functions](#chapter-14-useful-built-in-functions)
- [Chapter 15: Regular Expressions](#chapter-15-regular-expressions)
- [Chapter 16: List Comprehensions and Generators](#chapter-16-list-comprehensions-and-generators)
- [Chapter 17: Object-Oriented Programming — Basics](#chapter-17-object-oriented-programming--basics)
- [Chapter 18: OOP — Special Methods and Inheritance](#chapter-18-oop--special-methods-and-inheritance)
- [Chapter 19: OS Interaction — subprocess, pathlib, os](#chapter-19-os-interaction--subprocess-pathlib-os)
- [Chapter 20: Connecting to Network Devices (Netmiko)](#chapter-20-connecting-to-network-devices-netmiko)
- [Chapter 21: Sending Commands with Netmiko](#chapter-21-sending-commands-with-netmiko)
- [Chapter 22: Device Configuration with Netmiko](#chapter-22-device-configuration-with-netmiko)
- [Chapter 23: REST APIs with Python (requests)](#chapter-23-rest-apis-with-python-requests)
- [Chapter 24: Concurrent Connections — Threads and Processes](#chapter-24-concurrent-connections--threads-and-processes)
- [Chapter 25: Jinja2 Configuration Templates](#chapter-25-jinja2-configuration-templates)
- [Chapter 26: Parsing Output with TextFSM](#chapter-26-parsing-output-with-textfsm)
- [Chapter 27: Testing with pytest](#chapter-27-testing-with-pytest)
- [Chapter 28: Working with Databases (SQLite)](#chapter-28-working-with-databases-sqlite)
- [Chapter 29: Building a Complete Network Automation Project](#chapter-29-building-a-complete-network-automation-project)
- [Appendix A: Lab Task Answers](#appendix-a-lab-task-answers)

---


# Chapter 1: Environment Setup & First Steps

## 1.1 Why Python for Network Engineers?

Python has become the de facto language for network automation. Whether you manage Cisco IOS, NX-OS, Arista EOS, Juniper JunOS, or security platforms like Check Point, Python gives you a single language to automate them all.

**What you will automate with Python:**
- SSH into routers and switches to collect `show` commands
- Push configuration changes to hundreds of devices simultaneously
- Parse unstructured CLI output into structured data
- Interact with REST APIs (Cisco DNA Center, Check Point Management, Meraki, etc.)
- Generate configurations from templates (Jinja2)
- Build compliance audit scripts

## 1.2 Installing Python

### On Linux (Ubuntu/Debian) — Recommended for Network Engineers

```bash
sudo apt update
sudo apt install -y python3 python3-pip python3-venv git
python3 --version
```

### On macOS

```bash
# Install Homebrew first if not installed
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
brew install python3
```

### On Windows

Download the installer from [python.org](https://python.org). Check "Add Python to PATH" during installation.

## 1.3 Virtual Environments

> **PyNEng:** "Virtual environments allow different projects to have different sets of installed packages... this avoids conflicts between package versions."

> **LPTHW:** Focus on getting a clean terminal setup before writing any code.

```bash
# Create a virtual environment
python3 -m venv ~/netauto_venv

# Activate it
source ~/netauto_venv/bin/activate    # Linux/macOS
# netauto_venv\Scripts\activate       # Windows

# Verify
which python
pip install --upgrade pip
```

### Installing Key Packages for Network Automation

```bash
pip install netmiko paramiko requests pyyaml jinja2 rich textfsm
pip install python-dotenv ipdb
```

## 1.4 Your First Python Script

### LPTHW Approach — Type it, run it, see the output

Create a file called `ex1.py`:

```python
print("Hello, Network Engineer!")
print("I will automate your switches.")
print("I will automate your routers.")
print("I will automate your firewalls.")
```

Run it:
```bash
python3 ex1.py
```

### PyNEng Approach — Interactive interpreter (IPython)

```bash
pip install ipython
ipython
```

```python
In [1]: print("Hello, Network Engineer!")
Hello, Network Engineer!

In [2]: 2 + 2
Out[2]: 4

In [3]: exit()
```

### KByers Approach — Use the Rich library for pretty output

```python
#!/usr/bin/env python
from rich import print

print("Hello, Network Engineer!")
print("[bold green]Automation Ready![/bold green]")
```

## 1.5 The Python Interpreter and Comments

```python
# This is a comment — Python ignores this line
# Comments explain WHY, not WHAT

hostname = "core-rtr-01"  # inline comment

# Multi-line comments use consecutive # symbols
# or triple-quoted strings (docstrings)
"""
This script connects to all routers
and collects the running configuration.
"""
```

## 1.6 Git Basics (Version Control Your Scripts)

> **PyNEng:** "Git is a distributed version control system... even if you work alone, git can be useful."

```bash
# Initial setup
git config --global user.name "Your Name"
git config --global user.email "your_email@example.com"

# Create a repository
mkdir ~/network_automation
cd ~/network_automation
git init

# Basic workflow
git add script.py
git commit -m "Add initial device connection script"
git log --oneline
```

---

## Chapter 1 Lab Tasks

**Task 1.1:** Install Python 3 on your system. Create a virtual environment called `netauto`. Activate it and install `netmiko`, `requests`, `pyyaml`, and `rich`. Take a screenshot of `pip list` output.

**Task 1.2:** Write a script called `my_info.py` that prints your name, your role (e.g., "Network Engineer"), and the number of devices you manage. Use at least one comment.

**Task 1.3:** Open the Python interactive interpreter (or IPython). Perform these calculations: `255 * 255`, `10 / 3`, `2 ** 32`. What data types does Python return for each?

**Task 1.4:** Initialize a git repository in a new folder. Create a file called `hello.py` with a print statement, add it to git, and commit with the message "first commit". Run `git log` and note the output.

**Task 1.5:** Create a script that uses the `rich` library to print "Router connected!" in bold green and "Firewall blocked!" in bold red. (Hint: `from rich import print`, use `[bold green]` tags.)

---


# Chapter 2: Variables, Numbers, and Math

## 2.1 Variables

A variable stores a value. In Python, you do not declare variable types — Python infers them.

### LPTHW Style — Exercise 4: Variables and Names

```python
cars = 100
space_in_a_car = 4.0
drivers = 30
passengers = 90
cars_not_driven = cars - drivers
cars_driven = drivers
carpool_capacity = cars_driven * space_in_a_car
average_passengers_per_car = passengers / cars_driven

print("There are", cars, "cars available.")
print("There are only", drivers, "drivers available.")
print("We need to put about", average_passengers_per_car, "in each car.")
```

### PyNEng Style — Network Variables

```python
In [1]: hostname = "core-rtr-01"

In [2]: interface_count = 48

In [3]: cpu_load = 23.7

In [4]: type(hostname)
Out[4]: str

In [5]: type(interface_count)
Out[5]: int

In [6]: type(cpu_load)
Out[6]: float
```

### KByers Style — Networking Context

```python
#!/usr/bin/env python
from rich import print

fw_name = "chkpnt-pod99"
ip_address = "3.77.44.109"
os_version = "R82"

print(f"{fw_name=}")          # Python 3.8+ debug format
print(f"{ip_address=}")
print(f"{os_version=}")
```

**Output:**
```
fw_name='chkpnt-pod99'
ip_address='3.77.44.109'
os_version='R82'
```

## 2.2 Variable Naming Rules

```python
# GOOD names (descriptive, snake_case)
interface_name = "GigabitEthernet0/1"
vlan_id = 100
subnet_mask = "255.255.255.0"

# BAD names (avoid)
x = "GigabitEthernet0/1"    # too short, meaningless
InterfaceName = "Gi0/1"      # PascalCase is for classes
2nd_vlan = 200                # cannot start with a number — SyntaxError!
```

## 2.3 Numbers and Math

> **PyNEng:** "Python has several numeric types: int (integers) and float (floating-point numbers)."

```python
# Integer math
vlans_per_switch = 4094
switches = 5
total_vlans = vlans_per_switch * switches
print(total_vlans)            # 20470

# Float math
bandwidth_gbps = 10.0
utilization = 0.73
used_bandwidth = bandwidth_gbps * utilization
print(used_bandwidth)         # 7.3

# Division always returns float
print(10 / 3)                 # 3.3333333333333335

# Floor division (integer result)
print(10 // 3)                # 3

# Modulo (remainder)
print(10 % 3)                 # 1

# Exponentiation
print(2 ** 32)                # 4294967296 (IPv4 address space)
print(2 ** 128)               # IPv6 address space

# Rounding
print(round(10/3, 2))         # 3.33
```

## 2.4 Type Conversions

```python
# String to integer
vlan_str = "100"
vlan_int = int(vlan_str)
print(type(vlan_int))         # <class 'int'>

# Integer to string
port = 22
port_str = str(port)

# Float to integer (truncates, does NOT round)
print(int(3.9))               # 3

# Binary and Hexadecimal conversions (common in networking)
print(bin(255))               # '0b11111111'
print(hex(255))               # '0xff'
print(int('ff', 16))          # 255
print(int('11111111', 2))     # 255
print(bin(int('ff', 16)))     # '0b11111111'
```

## 2.5 Comparison Operators

```python
packets_sent = 1000
packets_received = 985

print(packets_sent > packets_received)     # True
print(packets_sent == packets_received)    # False
print(packets_sent != packets_received)    # True
print(packets_sent >= 1000)                # True

# Calculate packet loss
loss = packets_sent - packets_received
loss_pct = (loss / packets_sent) * 100
print(f"Packet loss: {loss_pct}%")         # Packet loss: 1.5%
```

---

## Chapter 2 Lab Tasks

**Task 2.1:** Create variables for a network device: `hostname`, `ip_address`, `model`, `ios_version`, `uptime_days`. Print them all using f-strings.

**Task 2.2:** Calculate the total number of usable IP addresses in a /24, /16, and /8 subnet using the formula `2^(32-prefix) - 2`. Print each result.

**Task 2.3:** Convert the decimal number 192 to binary and hexadecimal. Then convert the hex value "C0A80001" to decimal. What IP address does that represent?

**Task 2.4:** You have 1000 packets sent and 987 received. Calculate the packet loss percentage, rounded to 2 decimal places. Store each step in a variable.

**Task 2.5:** A 10 Gbps link runs at 73% utilization. Calculate the used bandwidth in Mbps. Then calculate how many megabytes can be transferred in 60 seconds at that rate (1 byte = 8 bits).

---


# Chapter 3: Strings and Text Processing

Strings are the most common data type in network automation. IP addresses, hostnames, show command output — it is all strings.

## 3.1 Creating Strings

```python
# Three ways to create strings
hostname = "core-rtr-01"
interface = 'GigabitEthernet0/0/0'
multiline_config = """interface Loopback0
 ip address 10.0.0.1 255.255.255.255
 no shutdown"""

print(hostname)
print(interface)
print(multiline_config)
```

## 3.2 String Operations

```python
hostname = "core-rtr-01"

# Length
print(len(hostname))          # 11

# Concatenation
domain = "example.com"
fqdn = hostname + "." + domain
print(fqdn)                   # core-rtr-01.example.com

# Repetition
divider = "-" * 40
print(divider)                # ----------------------------------------

# Membership test
print("rtr" in hostname)      # True
print("sw" in hostname)       # False
```

## 3.3 String Methods (Essential for Network Engineers)

### LPTHW + PyNEng Combined

```python
# .split() — Break strings apart (CRITICAL for parsing CLI output)
ip_address = "198.51.100.0/24"
network, mask = ip_address.split("/")
print(f"Network: {network}")     # Network: 198.51.100.0
print(f"Mask: {mask}")           # Mask: 24

octets = network.split(".")
print(octets)                    # ['198', '51', '100', '0']

# .join() — Combine list into string
commands = ['interface Gi0/1', 'switchport mode access', 'switchport access vlan 10']
config_block = "\n".join(commands)
print(config_block)
```

### KByers Approach — IPv4 and IPv6 Parsing

```python
#!/usr/bin/env python
from rich import print

ip_address = "198.51.100.0/24"
ipv6_address = "2001:db8:1:1::/64"

# IPv4 parsing
ipv4_network, ipv4_mask = ip_address.split("/")
octet1, octet2, octet3, octet4 = ipv4_network.split(".")

divider = "-" * 15
print(f"{'octet1':^15} {'octet2':^15} {'octet3':^15} {'octet4':^15}")
print(f"{divider:15} {divider:15} {divider:15} {divider:15}")
print(f"{octet1:^15} {octet2:^15} {octet3:^15} {octet4:^15}")

# IPv6 parsing
ipv6_network, ipv6_mask = ipv6_address.split("/")
start_ipv6, _ = ipv6_network.split("::")
hextet1, hextet2, hextet3, hextet4 = start_ipv6.split(":")
print(f"Hextets: {hextet1}, {hextet2}, {hextet3}, {hextet4}")
```

## 3.4 More Essential String Methods

```python
line = "  Interface GigabitEthernet0/1 is up, line protocol is up  "

# .strip() — Remove whitespace (critical for file/CLI output parsing)
print(line.strip())

# .upper() / .lower()
print("vlan100".upper())         # VLAN100
print("OSPF".lower())            # ospf

# .startswith() / .endswith()
if line.strip().startswith("Interface"):
    print("This is an interface line")

# .replace()
new_line = line.replace("up", "down")
print(new_line)

# .count()
config = "permit ip any any\npermit tcp any any\ndeny ip any any"
print(config.count("permit"))    # 2

# .find() — returns index, or -1 if not found
print(line.find("up"))           # first index where "up" occurs

# .isdigit()
vlan = "100"
print(vlan.isdigit())            # True
print("vlan100".isdigit())       # False
```

## 3.5 String Formatting (f-strings)

> **PyNEng:** "F-strings are the most convenient way of string formatting in Python 3.6+."

```python
hostname = "sw-access-01"
ip = "10.10.10.1"
vlan = 100

# f-string (Python 3.6+) — PREFERRED
print(f"Device {hostname} has IP {ip} on VLAN {vlan}")

# Alignment and padding
print(f"{'Hostname':<20} {'IP Address':<16} {'VLAN':>6}")
print(f"{hostname:<20} {ip:<16} {vlan:>6}")

# Debug format (Python 3.8+)
print(f"{hostname=}")            # hostname='sw-access-01'
print(f"{vlan=}")                # vlan=100
```

## 3.6 Escape Characters

```python
# Newline
print("line1\nline2")

# Tab
print("Name\tIP\tVLAN")
print("sw1\t10.0.0.1\t100")

# Backslash (for Windows paths)
print("C:\\Users\\admin\\scripts")

# Raw strings (ignore escapes) — useful for regex
print(r"C:\Users\admin\scripts")
```

---

## Chapter 3 Lab Tasks

**Task 3.1:** Given `show_ip = "Interface Gi0/1, IP 192.168.1.1/24, Status up"`, use `.split()` to extract the interface name, IP address (without mask), subnet mask, and status into separate variables. Print each.

**Task 3.2:** Create a list of 5 Cisco IOS interface configuration commands. Use `"\n".join()` to combine them into a single configuration block string. Print the result.

**Task 3.3:** Write a script that takes an IPv6 address `"2001:0db8:0000:0042:0000:0000:0000:0001"` and uses string methods to remove leading zeros from each hextet (produce the compressed form).

**Task 3.4:** Create a formatted table header using f-strings with these columns: Hostname (left-aligned, 20 chars), IP Address (left-aligned, 16 chars), Status (center-aligned, 10 chars). Print 3 sample rows beneath it.

**Task 3.5:** Given the string `"GigabitEthernet0/0/0"`, write code to check if it starts with "Gig", contains "0/0", and ends with "/0". Print each boolean result.

---


# Chapter 4: Lists

Lists are ordered, mutable collections. In network automation, lists hold device inventories, command sets, interface names, and parsed output lines.

## 4.1 Creating Lists

```python
# Empty list
my_devices = []

# List with values
vlans = [10, 20, 30, 40, 50]
hostnames = ["rtr1", "rtr2", "sw1", "sw2", "fw1"]
mixed = ["rtr1", 48, True, 3.14]   # mixed types allowed but not recommended

# List from string
show_output = "Gi0/1  10.0.0.1  up\nGi0/2  10.0.0.2  down"
lines = show_output.splitlines()
print(lines)  # ['Gi0/1  10.0.0.1  up', 'Gi0/2  10.0.0.2  down']
```

## 4.2 Indexing and Slicing

```python
devices = ["rtr1", "rtr2", "sw1", "sw2", "fw1"]

# Indexing (0-based)
print(devices[0])      # rtr1 (first)
print(devices[-1])     # fw1 (last)
print(devices[2])      # sw1

# Slicing [start:stop:step]
print(devices[0:2])    # ['rtr1', 'rtr2']  (stop is exclusive)
print(devices[:3])     # ['rtr1', 'rtr2', 'sw1']
print(devices[2:])     # ['sw1', 'sw2', 'fw1']
print(devices[::-1])   # ['fw1', 'sw2', 'sw1', 'rtr2', 'rtr1']  (reversed)
```

## 4.3 List Methods

### KByers Style — Firewall Device Lists

```python
#!/usr/bin/env python
from rich import print

locations = ["Munich", "Berlin", "Hamburg", "Frankfurt"]

# Print first and last
print(f"First element: {locations[0]}")
print(f"Last element: {locations[-1]}")
print(f"List length: {len(locations)}")

# .append() — Add one element to the end
locations.append("Leipzig")

# Modify an element by index
locations[3] = "Stuttgart"
print(locations)

# List concatenation
locations = locations + ["Dortmund", "Essen"]
# Alternative: locations += ["Dortmund", "Essen"]
print(locations)

# .pop() — Remove and return an element
city1 = locations.pop(0)     # remove first
city_n = locations.pop()     # remove last (default)
print(f"{city1=}")
print(f"{city_n=}")
print(f"{locations=}")
```

### PyNEng Style — More List Methods

```python
vlans = [10, 30, 20, 50, 40]

# .sort() — sort in-place
vlans.sort()
print(vlans)               # [10, 20, 30, 40, 50]

# sorted() — returns new sorted list (original unchanged)
original = [50, 20, 40, 10]
new_sorted = sorted(original)
print(original)            # [50, 20, 40, 10]  (unchanged)
print(new_sorted)          # [10, 20, 30, 40, 50]

# .insert(index, value)
vlans.insert(0, 1)
print(vlans)               # [1, 10, 20, 30, 40, 50]

# .remove(value) — removes first occurrence
vlans.remove(30)
print(vlans)               # [1, 10, 20, 40, 50]

# .extend() — add all elements from another list
vlans.extend([60, 70])
print(vlans)               # [1, 10, 20, 40, 50, 60, 70]

# .index(value) — find position
print(vlans.index(40))     # 3

# Check membership
print(20 in vlans)          # True
```

## 4.4 Iterating Over Lists (Preview — Full coverage in Chapter 8)

```python
firewalls = ["pod1-gaia", "pod2-gaia", "pod3-gaia", "pod4-gaia", "pod5-gaia"]

for fw in firewalls:
    print(fw)

# With index using enumerate
for idx, fw in enumerate(firewalls):
    print(f"{idx} -> {fw}")
```

---

## Chapter 4 Lab Tasks

**Task 4.1:** Create a list of 8 interface names (e.g., "Gi0/0" through "Gi0/7"). Print the third and last interfaces. Print the total count.

**Task 4.2:** Given `vlans = [10, 20, 30, 40, 50, 60]`, perform the following in order: (a) append VLAN 70, (b) insert VLAN 5 at position 0, (c) remove VLAN 30, (d) sort the list. Print the result after each step.

**Task 4.3:** Given two lists `core_devices = ["rtr1", "rtr2"]` and `access_devices = ["sw1", "sw2", "sw3"]`, combine them into a single list called `all_devices` using two different methods. Print both.

**Task 4.4:** Create a list of 5 IP addresses as strings. Use `.pop()` to remove the first and last. Print the removed IPs and the remaining list.

**Task 4.5:** Given `config_lines = ["interface Gi0/1", "switchport mode access", "switchport access vlan 10", "no shutdown"]`, reverse the list without using `.reverse()` and print the result.

---


# Chapter 5: Dictionaries

Dictionaries are key-value pairs — the most natural way to represent network device data (hostname → IP, interface → config, etc.).

## 5.1 Creating Dictionaries

```python
# Empty dictionary
device = {}

# Dictionary with values
device = {
    "hostname": "core-rtr-01",
    "ip": "10.10.10.1",
    "vendor": "Cisco",
    "model": "ISR4431",
    "ios_version": "17.3.4a",
    "interfaces": 48
}
```

### KByers Style — Firewall Service Object

```python
#!/usr/bin/env python
from rich import print

ftp_service = {
    "uid": "97aeb3d0-9aea-11d5-bd16-0090272ccb30",
    "name": "ftp",
    "type": "service-tcp",
    "domain": {
        "uid": "a0bbbc99-adef-4ef8-bb6d-defdefdefdef",
        "name": "Check Point Data",
        "domain-type": "data domain",
    },
    "port": "21",
    "icon": "Protocols/FTP",
    "color": "forest green",
}

# Access values
print(ftp_service["name"])            # ftp
print(ftp_service["port"])            # 21

# Nested dictionary access
print(ftp_service["domain"]["name"])  # Check Point Data
```

## 5.2 Dictionary Operations

### KByers Style — Network Object Manipulation

```python
#!/usr/bin/env python
from rich import print

network_obj = {
    "name": "hq_net_128",
    "subnet4": "172.31.128.0",
    "mask-length4": 24,
    "color": "green",
    "domain": {"uid": "abc-123-def"}
}

# Retrieve values
name = network_obj["name"]
network = network_obj["subnet4"]
netmask = network_obj["mask-length4"]
print(f"Network Object: {name} ({network}/{netmask})")

# Nested access
domain_uid = network_obj["domain"]["uid"]
print(f"Domain UID: {domain_uid}")

# Add a new key
network_obj["location"] = "Munich"

# Update a value
network_obj["location"] = "Cologne"

# Delete a key
network_obj.pop("color")

print(network_obj)
```

## 5.3 Dictionary Methods

```python
device = {
    "hostname": "sw1",
    "ip": "10.0.0.1",
    "vendor": "Cisco",
}

# .keys(), .values(), .items()
print(list(device.keys()))       # ['hostname', 'ip', 'vendor']
print(list(device.values()))     # ['sw1', '10.0.0.1', 'Cisco']

for key, value in device.items():
    print(f"{key}: {value}")

# .get() — safe access (returns None if key missing, no error)
model = device.get("model")
print(model)                     # None
model = device.get("model", "Unknown")
print(model)                     # Unknown

# .update() — merge dictionaries
extra_info = {"model": "C9300", "ports": 48}
device.update(extra_info)
print(device)

# .setdefault() — set value only if key does NOT exist
device.setdefault("vendor", "Arista")   # no change, "Cisco" already exists
device.setdefault("site", "HQ")         # adds "site": "HQ"

# Check membership (checks KEYS by default)
print("hostname" in device)     # True
print("sw1" in device)          # False (that's a value, not a key)
```

## 5.4 Netmiko Device Dictionaries

> **Netmiko Course:** Device parameters are always passed as dictionaries.

```python
from netmiko import ConnectHandler

# Standard Netmiko device dictionary
cisco_device = {
    "device_type": "cisco_ios",
    "host": "cisco3.lasthop.io",
    "username": "pyclass",
    "password": "secret123",
}

# Dictionary unpacking with **
net_connect = ConnectHandler(**cisco_device)
# This is equivalent to:
# ConnectHandler(device_type="cisco_ios", host="cisco3.lasthop.io", ...)
```

---

## Chapter 5 Lab Tasks

**Task 5.1:** Create a dictionary for a network device with keys: hostname, ip, vendor, model, os_version, site. Access and print each value using both bracket notation and `.get()`.

**Task 5.2:** Given a nested dictionary representing a firewall rule, access the "destination" IP which is nested 2 levels deep. Print it.
```python
fw_rule = {
    "name": "Allow_Web",
    "source": {"type": "host", "ip": "10.0.0.5"},
    "destination": {"type": "network", "ip": "192.168.1.0", "mask": "/24"},
    "action": "permit"
}
```

**Task 5.3:** Create two dictionaries for two routers. Merge them into a single `inventory` dictionary where the keys are hostnames and values are the full device dictionaries.

**Task 5.4:** Loop through a device dictionary using `.items()` and print each key-value pair formatted as `"key: value"` in a nicely aligned table.

**Task 5.5:** Create a Netmiko-style device dictionary for an Arista switch. Add a `session_log` key after creation. Change the `device_type` from `"arista_eos"` to `"arista_eos_ssh"`. Delete the `session_log` key. Print the final dictionary.

---


# Chapter 6: Tuples, Sets, and Booleans

## 6.1 Tuples

Tuples are immutable lists. They are used when data should not change (e.g., a fixed set of SNMP community strings, or coordinates).

```python
# Create tuples
dns_servers = ("8.8.8.8", "8.8.4.4")
credentials = ("admin", "secret123")

# Indexing (same as lists)
print(dns_servers[0])           # 8.8.8.8

# Unpacking
primary, secondary = dns_servers
print(primary)                  # 8.8.8.8

# Tuples are IMMUTABLE
# dns_servers[0] = "1.1.1.1"   # TypeError!

# Single element tuple requires trailing comma
single = ("only_one",)
not_a_tuple = ("only_one")     # This is just a string!
```

## 6.2 Sets

Sets are unordered collections of unique elements. They are excellent for comparing configurations, finding differences in VLAN lists, etc.

```python
# Create sets
vlans_sw1 = {10, 20, 30, 40, 50}
vlans_sw2 = {30, 40, 50, 60, 70}

# Union — all VLANs across both switches
all_vlans = vlans_sw1 | vlans_sw2
print(all_vlans)                # {10, 20, 30, 40, 50, 60, 70}

# Intersection — VLANs on BOTH switches
common = vlans_sw1 & vlans_sw2
print(common)                   # {30, 40, 50}

# Difference — VLANs on sw1 but NOT sw2
only_sw1 = vlans_sw1 - vlans_sw2
print(only_sw1)                 # {10, 20}

# Symmetric difference — VLANs on one OR the other but NOT both
unique = vlans_sw1 ^ vlans_sw2
print(unique)                   # {10, 20, 60, 70}

# Practical: Find blocked IPs to add/remove
current_blocked = {"1.2.3.4", "5.6.7.8", "9.10.11.12"}
new_blocked = {"5.6.7.8", "9.10.11.12", "13.14.15.16"}

add_ips = new_blocked - current_blocked
remove_ips = current_blocked - new_blocked
print(f"Add: {add_ips}")        # Add: {'13.14.15.16'}
print(f"Remove: {remove_ips}")  # Remove: {'1.2.3.4'}
```

### KByers Style — Set Comparison for Blocked IPs

```python
# From class4/exercises/main_project/03_mgmt_api_cfg.py
current_blocked_ips = get_current_blocked_ips(api_client, group_name)
new_blocked_ips = read_blocked_ips_file()

if set(current_blocked_ips) == set(new_blocked_ips):
    print("No Blocked IP Changes")
else:
    add_blocked_ips = set(new_blocked_ips) - set(current_blocked_ips)
    remove_blocked_ips = set(current_blocked_ips) - set(new_blocked_ips)
```

## 6.3 Booleans and Truthiness

### KByers Style — Truthiness in Python

```python
#!/usr/bin/env python
from rich import print

# Strings: empty string is False
some_str = ""
print(bool(some_str))           # False
print(bool("hello"))            # True

# Numbers: 0 is False
some_int = 0
print(bool(some_int))           # False
print(bool(42))                 # True

# Lists: empty list is False
some_list = []
print(bool(some_list))          # False
print(bool([1, 2]))             # True

# Dict: empty dict is False
some_dict = {}
print(bool(some_dict))          # False
```

### Short-Circuit Evaluation

```python
# and: if first condition is False, skip second
check_cond = False
if check_cond and some_function():    # some_function() never called
    print("Never printed")

# or: if first condition is True, skip second
skip_func = True
if skip_func or some_function():      # some_function() never called
    print("Always printed")
```

---

## Chapter 6 Lab Tasks

**Task 6.1:** Create a tuple of 3 DNS server IPs. Try to modify the first element. What error do you get? Unpack all three into individual variables and print them.

**Task 6.2:** Two switches have these VLANs: `sw1 = {10, 20, 30, 40, 50}` and `sw2 = {30, 40, 50, 60, 70}`. Find: (a) all VLANs, (b) common VLANs, (c) VLANs only on sw1, (d) VLANs unique to one switch.

**Task 6.3:** Create a list with duplicates: `[10, 20, 30, 10, 20, 40]`. Convert it to a set to remove duplicates, then back to a sorted list. Print each step.

**Task 6.4:** Write code that checks the "truthiness" of: `0`, `""`, `[]`, `{}`, `None`, `"hello"`, `[1]`, `42`. Print the boolean value of each.

**Task 6.5:** Given `current_acl = {"permit_web", "permit_ssh", "deny_telnet"}` and `desired_acl = {"permit_web", "permit_ssh", "permit_dns"}`, find which rules to add and which to remove. Print both.

---


# Chapter 7: Conditionals (if/elif/else)

## 7.1 Basic if/elif/else

> **PyNEng:** "The if/elif/else statement allows make branches during program execution."

### LPTHW Style — Simple Decisions

```python
people = 20
cats = 30
dogs = 15

if people < cats:
    print("Too many cats! The world is doomed!")
elif people > cats:
    print("Not many cats! The world is saved!")
else:
    print("The world is on a thin line.")
```

### KByers Style — Firewall Pod Selection

```python
#!/usr/bin/env python
from rich import print

pod_numb = input("Enter pod number: ")
fw_name = f"chkpnt-pod{pod_numb}"

if fw_name == "chkpnt-pod1":
    print("Found pod1")
elif fw_name == "chkpnt-pod99":
    print("Found pod99")
else:
    print("Not my pod")
```

## 7.2 Compound Conditions (and, or, not)

### KByers Style — API Version Checking

```python
#!/usr/bin/env python
from rich import print

api_version = "1.8"

if "1." in api_version:
    base_api = "v1"
elif "2." in api_version:
    base_api = "v2"

# Compound conditions
if base_api == "v1" and float(api_version) >= 1.8:
    print("API Version 1.8 or later (not V2)")

if base_api == "v1" or base_api == "v2":
    print("API V1 or V2")
```

## 7.3 Checking Data Structures

### PyNEng Style

```python
# Empty list check (Pythonic way)
route_table = []
if route_table:
    print("Routes found")
else:
    print("No routes in table")

# Membership check
allowed_vlans = [10, 20, 30, 40, 50]
new_vlan = 25
if new_vlan in allowed_vlans:
    print(f"VLAN {new_vlan} is allowed")
else:
    print(f"VLAN {new_vlan} is NOT allowed")
```

## 7.4 Nested Conditionals

### KByers Style — Service Matching with JSON

```python
#!/usr/bin/env python
import json
from rich import print

with open("tcp_services.json") as f:
    services = json.load(f)

service_list = services["objects"]
print(len(service_list))

for service in service_list:
    service_name = service["name"]
    if service_name == "ftp":
        print("Found FTP Service")
    elif service_name == "domain-tcp":
        print("Found DNS (TCP)")
    else:
        print(service_name)
```

## 7.5 Ternary Expressions

```python
# Compact conditional assignment
interface_status = "up"
color = "green" if interface_status == "up" else "red"
print(f"Status: [{color}]{interface_status}")

# From Netmiko course — password handling
import os
from getpass import getpass
password = os.getenv("NETMIKO_PASSWORD") if os.getenv("NETMIKO_PASSWORD") else getpass()
```

---

## Chapter 7 Lab Tasks

**Task 7.1:** Write a script that takes a VLAN number as input. If the VLAN is 1, print "Default VLAN — do not use". If the VLAN is between 2-1000, print "Standard VLAN". If between 1001-4094, print "Extended VLAN". Otherwise, print "Invalid VLAN".

**Task 7.2:** Given an interface status dictionary `{"name": "Gi0/1", "status": "up", "protocol": "up", "speed": "1000"}`, write code that checks: if both status AND protocol are "up", print "Fully operational". If status is "up" but protocol is "down", print "Layer 1 up, Layer 2 issue". Otherwise print "Interface down".

**Task 7.3:** Write a script that checks if a given IP address string is valid (simple check: split by ".", check exactly 4 octets, each octet is a digit between 0-255). Print "Valid" or "Invalid".

**Task 7.4:** Given `api_version = "1.8"`, use conditionals to determine the base URL. If version starts with "1.", use `base_api = "v1"`. If version starts with "2.", use `base_api = "v2"`. Print the resulting `base_url` as `https://host/{base_api}/api/`.

**Task 7.5:** Write a ternary expression that assigns "SSH" if port is 22, "HTTPS" if port is 443, or "Unknown" for any other port. Test with ports 22, 443, and 8080.

---


# Chapter 8: Loops (for and while)

## 8.1 for Loops

### KByers Style — Iterating Over Firewalls

```python
from rich import print

my_firewalls = [
    "pod1-gaia",
    "pod2-gaia",
    "pod3-gaia",
    "pod4-gaia",
    "pod5-gaia",
]

# Basic for loop
for fw in my_firewalls:
    print(fw)

# Conditional inside loop
for fw in my_firewalls:
    if fw == "pod5-gaia":
        print(f"\nConnecting to fw: {fw}\n")
```

### PyNEng Style — Generating Config

```python
access_template = [
    'switchport mode access',
    'switchport access vlan {}',
    'switchport nonegotiate',
    'spanning-tree portfast',
    'spanning-tree bpduguard enable'
]

vlans = [10, 20, 30]
for vlan in vlans:
    print(f"interface Vlan{vlan}")
    for command in access_template:
        print(f" {command.format(vlan)}")
    print("!")
```

## 8.2 break and continue

### KByers Style

```python
from rich import print

my_firewalls = [
    "pod1-gaia", "pod2-gaia", "pod3-gaia",
    "pod4-gaia", "pod5-gaia", "pod98-gaia", "pod99-gaia",
]

for fw in my_firewalls:
    if fw == "pod4-gaia":
        continue          # Skip pod4, go to next iteration
    if fw == "pod98-gaia":
        break             # Stop the entire loop
    print(fw)

# Output: pod1-gaia, pod2-gaia, pod3-gaia, pod5-gaia
```

## 8.3 enumerate() — Loop with Index

```python
from rich import print

my_firewalls = ["pod1-gaia", "pod2-gaia", "pod3-gaia"]

for idx, fw in enumerate(my_firewalls):
    print(f"{idx} -> {fw}")

# Start counting from 1
for idx, fw in enumerate(my_firewalls, start=1):
    print(f"Device #{idx}: {fw}")
```

## 8.4 Looping Over Dictionaries

```python
device = {
    "hostname": "rtr1",
    "ip": "10.0.0.1",
    "vendor": "Cisco",
    "model": "ISR4431"
}

# Loop over keys
for key in device:
    print(key)

# Loop over values
for value in device.values():
    print(value)

# Loop over key-value pairs (most common)
for key, value in device.items():
    print(f"{key:>12}: {value}")
```

## 8.5 while Loops

### KByers Style — Wait with Timeout

```python
from rich import print
import time

WAIT_TIME = 8

start_time = time.time()
while True:
    cur_time = time.time()
    if cur_time - start_time < WAIT_TIME:
        print("Sleeping 1s")
        time.sleep(1)
    else:
        print("All done...")
        break
```

### PyNEng Style — User Input Loop

```python
while True:
    password = input("Enter password (min 8 chars): ")
    if len(password) >= 8:
        print("Password accepted")
        break
    print("Too short, try again")
```

## 8.6 Nested Loops

```python
# Generate interface configs for multiple switches
switches = ["sw1", "sw2"]
interfaces = ["Gi0/1", "Gi0/2", "Gi0/3"]
vlan = 10

for switch in switches:
    print(f"\n! Configuration for {switch}")
    for intf in interfaces:
        print(f"interface {intf}")
        print(f" switchport access vlan {vlan}")
        vlan += 10
```

---

## Chapter 8 Lab Tasks

**Task 8.1:** Create a list of 10 IP addresses (e.g., "10.0.0.1" through "10.0.0.10"). Use a for loop to print each IP with its index number starting from 1.

**Task 8.2:** Loop through a list of device hostnames. Use `continue` to skip any hostname containing "test". Use `break` to stop when you encounter "STOP". Print all other hostnames.
```python
devices = ["rtr1", "sw1", "test-rtr", "fw1", "STOP", "rtr2"]
```

**Task 8.3:** Write a while loop that simulates a retry mechanism: attempt to "connect" (just print a message) up to 3 times, with a 1-second sleep between attempts. After 3 failures, print "Connection failed after 3 retries".

**Task 8.4:** Given a dictionary of devices, loop through it and print a formatted table:
```python
devices = {
    "rtr1": {"ip": "10.0.0.1", "vendor": "Cisco"},
    "sw1": {"ip": "10.0.0.2", "vendor": "Arista"},
    "fw1": {"ip": "10.0.0.3", "vendor": "Palo Alto"},
}
```

**Task 8.5:** Write nested loops that generate trunk interface configs for 3 interfaces across 2 switches, with allowed VLANs 10, 20, 30. The output should look like real Cisco IOS configuration.

---


# Chapter 9: Functions

## 9.1 Defining Functions

### LPTHW Style — Building Blocks

```python
def print_two(*args):
    arg1, arg2 = args
    print(f"arg1: {arg1}, arg2: {arg2}")

def print_one(arg1):
    print(f"arg1: {arg1}")

def print_none():
    print("I got nothing.")

print_two("Zed", "Shaw")
print_one("First!")
print_none()
```

### KByers Style — Network Functions

```python
#!/usr/bin/env python
from rich import print

def fw_func(name, ipaddr, os_version="R82"):
    print(f"{name=}")
    print(f"{ipaddr=}")
    print(f"{os_version=}")
    return f"{name}-{ipaddr}-{os_version}"

# Positional arguments
ret_val = fw_func("chkpnt-pod99", "3.77.44.109", "R81.20")
print(f"\n{ret_val=}\n")

# Named (keyword) arguments
ret_val = fw_func(
    os_version="R82",
    ipaddr="3.77.44.100",
    name="chkpnt-pod1",
)
print(f"\n{ret_val=}\n")

# Using default value
ret_val = fw_func(name="chkpnt-pod1", ipaddr="3.77.44.100")
print(f"\n{ret_val=}\n")
```

## 9.2 Return Values

```python
def check_interface_status(status, protocol):
    """Check if interface is fully operational."""
    if status == "up" and protocol == "up":
        return "operational"
    elif status == "up":
        return "layer2_issue"
    else:
        return "down"

result = check_interface_status("up", "up")
print(result)    # operational

# Functions without return statement return None
def greet(name):
    print(f"Hello {name}")

result = greet("Engineer")    # prints "Hello Engineer"
print(result)                  # None
```

## 9.3 Docstrings

```python
def calculate_subnet_hosts(prefix_length):
    """Calculate the number of usable hosts in a subnet.

    Args:
        prefix_length (int): CIDR prefix length (0-32)

    Returns:
        int: Number of usable host addresses

    Example:
        >>> calculate_subnet_hosts(24)
        254
    """
    if prefix_length < 0 or prefix_length > 32:
        raise ValueError(f"Invalid prefix: {prefix_length}")
    total = 2 ** (32 - prefix_length)
    return total - 2 if prefix_length < 31 else total
```

## 9.4 Functions as Reusable Modules

### KByers Style — API Helper Functions

```python
import requests
import json

def login(base_url, user, password, ssl_verify=False):
    """Login and return session headers."""
    url = base_url + "login"
    headers = {"Content-Type": "application/json"}
    login_payload = {"user": user, "password": password}
    response = requests.post(
        url, data=json.dumps(login_payload),
        headers=headers, verify=ssl_verify
    )
    return response

def api_call(base_url, endpoint, headers, payload=None, ssl_verify=False):
    """Make an API call with session headers."""
    if payload is None:
        payload = {}
    url = base_url + endpoint
    response = requests.post(
        url, data=json.dumps(payload),
        headers=headers, verify=ssl_verify
    )
    return response

def logout(base_url, headers, ssl_verify=False):
    """Logout and clean up session."""
    endpoint = "logout"
    response = api_call(base_url, endpoint, headers, ssl_verify=ssl_verify)
    if response.status_code == 200:
        if "X-chkp-sid" in headers:
            headers.pop("X-chkp-sid")
    return response
```

## 9.5 *args and **kwargs

```python
# *args — variable number of positional arguments
def configure_vlans(*vlans):
    for vlan in vlans:
        print(f" vlan {vlan}")

configure_vlans(10, 20, 30)

# **kwargs — variable number of keyword arguments
def create_device(**params):
    for key, value in params.items():
        print(f"  {key}: {value}")

create_device(hostname="rtr1", ip="10.0.0.1", vendor="Cisco")

# Dictionary unpacking with **
device = {"device_type": "cisco_ios", "host": "10.0.0.1", "username": "admin"}
# ConnectHandler(**device) unpacks the dict into keyword arguments
```

---

## Chapter 9 Lab Tasks

**Task 9.1:** Write a function `generate_hostname(site, role, number)` that returns a hostname like "NYC-RTR-01". Include a default value of "01" for number. Test with several calls.

**Task 9.2:** Write a function `validate_ip(ip_address)` that takes an IP address string and returns `True` if valid, `False` otherwise. Include a docstring explaining the function.

**Task 9.3:** Write two functions: `read_json(filename)` that reads a JSON file and returns the data structure, and `extract_fields(task)` that extracts specific fields from a dict. Call one from the other.

**Task 9.4:** Write a function that accepts `**kwargs` for device parameters (hostname, ip, vendor, model) and prints a formatted device summary. Handle missing keys with `.get()` defaults.

**Task 9.5:** Refactor the following code into a reusable function that can work for any device list:
```python
for device in devices:
    print(f"Connecting to {device['hostname']}...")
    print(f"  IP: {device['ip']}")
    print(f"  Vendor: {device['vendor']}")
```

---


# Chapter 10: Working with Files

## 10.1 Reading Files

### KByers Style — Multiple Methods

```python
#!/usr/bin/env python
from rich import print

# Method 1: read() — entire file as one string
f = open("my_file.txt", "r")
data = f.read()
print(data)
f.close()

# Method 2: readlines() — file as list of lines
f = open("my_file.txt", "r")
lines = f.readlines()
print(type(lines))     # <class 'list'>
print(lines)           # ['line1\n', 'line2\n', ...]
f.close()

# Method 3: iterate line by line
f = open("my_file.txt", "r")
for line in f:
    line = line.strip()    # remove trailing newline
    print(repr(line))
f.close()
```

## 10.2 Context Manager (with statement)

> **PyNEng & KByers:** Always use `with` to automatically close files.

```python
# Context manager automatically closes the file when done
with open("my_file.txt") as f:
    data = f.read()

print(data)
# File is already closed here — no need for f.close()
```

## 10.3 Writing Files

### KByers Style

```python
#!/usr/bin/env python

# Write (creates or overwrites)
with open("new_file.txt", "w") as f:
    f.write("--> hello world <--\n")
    f.write("something else\n")
    f.write("one last line\n")

# Append (adds to end of existing file)
with open("new_file.txt", "a") as f:
    f.write("appended line\n")
```

## 10.4 Reading JSON Files

```python
import json
from rich import print

# Read JSON
with open("gaia_api.json") as f:
    data = json.load(f)

print(type(data))    # <class 'dict'>
print(data)

# Write JSON
data = {
    "current-version": "1.8",
    "supported-versions": ["1", "1.1", "1.2", "1.3", "1.4", "1.5", "1.6", "1.7", "1.8"],
}

with open("gaia_api.json", "w") as f:
    json.dump(data, f, indent=4)
```

## 10.5 Reading YAML Files

```python
import yaml
from rich import print

# Read YAML
with open("gaia_api.yaml") as f:
    data = yaml.safe_load(f)

print(data)

# Write YAML
data = {
    "current-version": "1.8",
    "supported-versions": ["1", "1.1", "1.2", "1.3", "1.4", "1.5", "1.6", "1.7", "1.8"],
}

with open("gaia_api.yaml", "w") as f:
    yaml.dump(data, f, default_flow_style=False)
```

## 10.6 Read vs Load: String vs Data Structure

### KByers Style — Critical Distinction

```python
import json
from rich import print

filename = "network_objects.json"

# Read as TEXT (string)
with open(filename) as f:
    data = f.read()
print(f"Type: {type(data)}")       # <class 'str'>

# Read as DATA STRUCTURE (dict/list)
with open(filename) as f:
    data = json.load(f)
print(f"Type: {type(data)}")       # <class 'dict'>
print(f"Type of 'objects': {type(data['objects'])}")  # <class 'list'>
```

---

## Chapter 10 Lab Tasks

**Task 10.1:** Create a text file with 5 router hostnames (one per line). Read the file and print each hostname stripped of whitespace.

**Task 10.2:** Write a script that reads a JSON file containing a list of devices, loops through them, and prints each device's hostname and IP. Create the JSON file first.

**Task 10.3:** Create a YAML file with a list of firewall names and their management IPs. Read it back and print the data.

**Task 10.4:** Write a script that reads a config file line by line, counts the number of "interface" lines, and writes only those interface lines to a new file.

**Task 10.5:** Demonstrate the difference between `f.read()` (string), `json.load()` (data structure), and `f.readlines()` (list of strings) on the same JSON file. Print the type of each.

---


# Chapter 11: Working with CSV, JSON, and YAML

## 11.1 CSV Files

```python
import csv

# Read CSV
with open("devices.csv") as f:
    reader = csv.DictReader(f)
    for row in reader:
        print(f"{row['hostname']:15} {row['ip']:16} {row['vendor']}")

# Write CSV
devices = [
    {"hostname": "rtr1", "ip": "10.0.0.1", "vendor": "Cisco"},
    {"hostname": "sw1", "ip": "10.0.0.2", "vendor": "Arista"},
]

with open("devices.csv", "w", newline="") as f:
    fieldnames = ["hostname", "ip", "vendor"]
    writer = csv.DictWriter(f, fieldnames=fieldnames)
    writer.writeheader()
    writer.writerows(devices)
```

## 11.2 JSON — Deep Dive

```python
import json

# json.loads() — parse JSON STRING into Python object
json_string = '{"hostname": "rtr1", "ip": "10.0.0.1"}'
data = json.loads(json_string)
print(type(data))    # <class 'dict'>

# json.dumps() — convert Python object to JSON STRING
python_dict = {"hostname": "rtr1", "interfaces": ["Gi0/1", "Gi0/2"]}
json_str = json.dumps(python_dict, indent=2)
print(json_str)

# json.load() — read JSON from FILE
with open("data.json") as f:
    data = json.load(f)

# json.dump() — write Python object to JSON FILE
with open("output.json", "w") as f:
    json.dump(data, f, indent=4)
```

## 11.3 YAML — Deep Dive

```yaml
# devices.yaml
---
- hostname: rtr1
  ip: 10.0.0.1
  vendor: Cisco
  interfaces:
    - Gi0/1
    - Gi0/2
- hostname: sw1
  ip: 10.0.0.2
  vendor: Arista
```

```python
import yaml

with open("devices.yaml") as f:
    devices = yaml.safe_load(f)

for device in devices:
    print(f"{device['hostname']}: {device['ip']}")
```

---

## Chapter 11 Lab Tasks

**Task 11.1:** Create a CSV file with 5 devices (hostname, ip, vendor, model). Read it with `csv.DictReader` and print a formatted table.

**Task 11.2:** Convert this Python dictionary to a JSON string with indentation, then parse it back. Verify the round-trip.
```python
network = {"name": "HQ_LAN", "subnet": "10.0.0.0/8", "vlans": [10, 20, 30]}
```

**Task 11.3:** Create a YAML file representing 3 devices with nested interface lists. Read it and print each device's hostname and interface count.

**Task 11.4:** Write a script that reads a JSON file, adds a new field to each device object, and writes the modified data to a new JSON file.

**Task 11.5:** Convert a CSV device inventory to YAML format programmatically (read CSV, write YAML).

---

# Chapter 12: Error Handling (try/except)

## 12.1 Basic try/except

### KByers Style — Progressive Error Handling

```python
#!/usr/bin/env python
from rich import print

# Basic try/except
try:
    result = 10 / 0
except ZeroDivisionError:
    print("Cannot divide by zero!")

# Multiple exception types
try:
    data = {"key": "value"}
    print(data["missing_key"])
except KeyError as e:
    print(f"Key not found: {e}")
except TypeError as e:
    print(f"Type error: {e}")

# Generic exception (catch-all)
try:
    risky_operation()
except Exception as e:
    print(f"Something went wrong: {e}")

# try/except/else/finally
try:
    with open("config.json") as f:
        data = json.load(f)
except FileNotFoundError:
    print("Config file not found!")
    data = {}
except json.JSONDecodeError:
    print("Invalid JSON!")
    data = {}
else:
    print("Config loaded successfully")
finally:
    print("Cleanup complete")
```

## 12.2 Custom Exceptions

### KByers Style — Security Automation Exceptions

```python
class ChkPntConfigError(Exception):
    """Raised when Check Point configuration fails."""
    pass

class ChkPntPolicyInstallError(Exception):
    """Raised when firewall policy installation fails."""
    pass

class ChkptAuthError(Exception):
    """Raised when session ID is missing or expired."""
    pass

# Using custom exceptions
def api_call(url, headers, payload=None):
    if "X-chkp-sid" not in headers:
        msg = "Session ID not set, please call '.login()' first."
        raise ChkptAuthError(msg)
    # ... rest of implementation
```

---

## Chapter 12 Lab Tasks

**Task 12.1:** Write a script that tries to open a file that doesn't exist. Catch the `FileNotFoundError` and print a friendly message.

**Task 12.2:** Write a function that converts a string to an integer. Handle `ValueError` for non-numeric strings. Return `None` on failure.

**Task 12.3:** Create a custom exception `InvalidVlanError`. Write a function that raises it when a VLAN number is outside 1-4094.

**Task 12.4:** Write a try/except/else/finally block that reads a JSON file: handle missing file and invalid JSON separately, print "success" in `else`, and "done" in `finally`.

**Task 12.5:** Write a function that connects to a device (simulate with a dict lookup). If the device is not in the inventory, raise a custom `DeviceNotFoundError` with the hostname in the message.

---

# Chapter 13: Modules and Packages

## 13.1 Importing Modules

```python
# Import entire module
import os
print(os.getcwd())

# Import specific function
from os import path
print(path.exists("/etc/hosts"))

# Import with alias
import json as j
data = j.loads('{"key": "value"}')

# Import multiple items
from pathlib import Path
from rich import print
```

## 13.2 Creating Your Own Module

```python
# File: network_utils.py
def validate_ip(ip_address):
    octets = ip_address.split(".")
    if len(octets) != 4:
        return False
    return all(o.isdigit() and 0 <= int(o) <= 255 for o in octets)

def generate_hostname(site, role, number=1):
    return f"{site}-{role}-{number:02d}"
```

```python
# File: main.py
from network_utils import validate_ip, generate_hostname

print(validate_ip("10.0.0.1"))           # True
print(generate_hostname("NYC", "RTR"))    # NYC-RTR-01
```

## 13.3 The `if __name__ == "__main__"` Pattern

```python
# File: gaia_funcs.py
def login(url, username, password):
    """Login and return session ID."""
    # ... implementation

def logout(url, headers):
    """Logout from API."""
    # ... implementation

if __name__ == "__main__":
    # This code ONLY runs when script is executed directly
    # NOT when imported as a module
    print("Testing functions...")
    session_id = login("https://fw.example.com/api/", "admin", "pass")
    print(f"Got session: {session_id}")
```

---

## Chapter 13 Lab Tasks

**Task 13.1:** Create a module called `net_helpers.py` with 3 functions: `validate_ip()`, `mask_to_cidr()`, and `generate_hostname()`. Import and use them from a separate script.

**Task 13.2:** Demonstrate 3 different import styles (import, from...import, import...as) using the `json` module.

**Task 13.3:** Add `if __name__ == "__main__"` to your `net_helpers.py` module that runs test cases when executed directly.

**Task 13.4:** Create a package (folder with `__init__.py`) called `netauto` containing two modules: `devices.py` and `configs.py`. Import from both in a main script.

**Task 13.5:** Install the `rich` library and use `from rich import print` alongside `from rich.table import Table` to create a formatted device table.

---

# Chapter 14: Useful Built-in Functions

## 14.1 range()

```python
# Generate VLAN IDs
for vlan in range(10, 51, 10):   # start, stop, step
    print(f"vlan {vlan}")
# Output: vlan 10, vlan 20, vlan 30, vlan 40, vlan 50
```

## 14.2 enumerate()

```python
interfaces = ["Gi0/1", "Gi0/2", "Gi0/3"]
for idx, intf in enumerate(interfaces, start=1):
    print(f"{idx}. {intf}")
```

## 14.3 zip()

```python
hostnames = ["rtr1", "rtr2", "rtr3"]
ips = ["10.0.0.1", "10.0.0.2", "10.0.0.3"]
vendors = ["Cisco", "Cisco", "Juniper"]

for hostname, ip, vendor in zip(hostnames, ips, vendors):
    print(f"{hostname:10} {ip:15} {vendor}")
```

## 14.4 sorted(), map(), filter(), lambda

```python
# sorted() with key
devices = [
    {"name": "sw2", "ip": "10.0.0.2"},
    {"name": "rtr1", "ip": "10.0.0.1"},
    {"name": "fw1", "ip": "10.0.0.3"},
]
sorted_devices = sorted(devices, key=lambda d: d["name"])

# map() — apply function to every element
vlans = ["10", "20", "30"]
vlan_ints = list(map(int, vlans))    # [10, 20, 30]

# filter() — keep elements that pass test
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
evens = list(filter(lambda x: x % 2 == 0, numbers))  # [2, 4, 6, 8, 10]

# all() / any()
statuses = ["up", "up", "up"]
print(all(s == "up" for s in statuses))    # True

statuses = ["up", "down", "up"]
print(any(s == "down" for s in statuses))  # True
```

---

## Chapter 14 Lab Tasks

**Task 14.1:** Use `range()` to generate a list of IPs from 10.0.0.1 to 10.0.0.10. Print each.

**Task 14.2:** Use `zip()` to combine three lists (hostnames, IPs, VLANs) into a list of dictionaries.

**Task 14.3:** Use `sorted()` with a `lambda` key to sort a list of device dictionaries by IP address.

**Task 14.4:** Use `filter()` to extract only "up" interfaces from a list of interface status dicts.

**Task 14.5:** Use `all()` to verify every device in a list has the key "hostname" set to a non-empty string.

---

# Chapter 15: Regular Expressions

## 15.1 Basic Regex with re Module

```python
import re

# re.search() — find first match
line = "Interface GigabitEthernet0/0/0 is up, line protocol is up"
match = re.search(r"(\S+) is (up|down)", line)
if match:
    print(match.group(0))    # GigabitEthernet0/0/0 is up
    print(match.group(1))    # GigabitEthernet0/0/0
    print(match.group(2))    # up

# re.findall() — find ALL matches
config = """
ip route 10.0.0.0 255.0.0.0 192.168.1.1
ip route 172.16.0.0 255.240.0.0 192.168.1.1
ip route 0.0.0.0 0.0.0.0 192.168.1.254
"""
routes = re.findall(r"ip route (\S+) (\S+) (\S+)", config)
for dest, mask, nexthop in routes:
    print(f"Destination: {dest}/{mask} via {nexthop}")
```

## 15.2 Common Regex Patterns for Network Engineers

```python
import re

# IP address pattern
ip_pattern = r"\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}"

# MAC address pattern
mac_pattern = r"[0-9a-fA-F]{4}\.[0-9a-fA-F]{4}\.[0-9a-fA-F]{4}"

# Interface name pattern
intf_pattern = r"(Gi|Te|Fa|Lo|Vl)\S+"

# VLAN pattern
vlan_pattern = r"Vlan(\d+)"

text = "Interface Gi0/1 has IP 10.0.0.1 and MAC aabb.ccdd.eeff on Vlan100"
print(re.findall(ip_pattern, text))      # ['10.0.0.1']
print(re.findall(mac_pattern, text))     # ['aabb.ccdd.eeff']
print(re.findall(intf_pattern, text))    # ['Gi0/1']
print(re.findall(vlan_pattern, text))    # ['100']
```

## 15.3 re.sub() — Find and Replace

```python
import re

config = "interface GigabitEthernet0/1\n ip address 10.0.0.1 255.255.255.0"
new_config = re.sub(r"10\.0\.0\.1", "192.168.1.1", config)
print(new_config)
```

---

## Chapter 15 Lab Tasks

**Task 15.1:** Use `re.search()` to extract the IP address and subnet mask from: `"ip address 192.168.1.1 255.255.255.0"`.

**Task 15.2:** Use `re.findall()` to extract all IP addresses from a multi-line `show ip route` output string.

**Task 15.3:** Write a regex that matches Cisco interface names (GigabitEthernet, TenGigabitEthernet, FastEthernet, Loopback, Vlan). Test against a sample config.

**Task 15.4:** Use `re.sub()` to replace all occurrences of an old IP with a new IP in a config string.

**Task 15.5:** Parse the following line to extract hostname, IP, and status using named groups:
`"Device: rtr1, IP: 10.0.0.1, Status: up"`

---

# Chapter 16: List Comprehensions and Generators

## 16.1 List Comprehensions

```python
# Traditional loop
vlans = []
for i in range(10, 60, 10):
    vlans.append(i)

# List comprehension (same result, one line)
vlans = [i for i in range(10, 60, 10)]
print(vlans)    # [10, 20, 30, 40, 50]

# With condition
up_interfaces = [intf for intf in interfaces if intf["status"] == "up"]

# Transform + filter
hostnames = ["RTR1", "SW1", "FW1"]
lower_names = [name.lower() for name in hostnames]

# Network examples
ips = [f"10.0.0.{i}" for i in range(1, 11)]
print(ips)  # ['10.0.0.1', '10.0.0.2', ..., '10.0.0.10']

# From KByers — strip whitespace from file lines
with open("blocked_ips.txt") as f:
    blocked_ips = [ip.strip() for ip in f.readlines()]

# From KByers — generate host objects
blocked_ip_objs = [gen_host_object(ip) for ip in add_blocked_ips]
```

## 16.2 Dictionary Comprehensions

```python
# Create dict from two lists
hostnames = ["rtr1", "rtr2", "rtr3"]
ips = ["10.0.0.1", "10.0.0.2", "10.0.0.3"]

device_map = {host: ip for host, ip in zip(hostnames, ips)}
print(device_map)  # {'rtr1': '10.0.0.1', 'rtr2': '10.0.0.2', 'rtr3': '10.0.0.3'}
```

## 16.3 Generator Expressions

```python
# Generator — lazy evaluation, saves memory for large datasets
ip_gen = (f"10.0.0.{i}" for i in range(1, 1000001))

# Only generates values as needed
for ip in ip_gen:
    if ip == "10.0.0.5":
        print(f"Found: {ip}")
        break
```

---

## Chapter 16 Lab Tasks

**Task 16.1:** Use a list comprehension to create a list of 20 IPs from "192.168.1.1" to "192.168.1.20".

**Task 16.2:** Given a list of interface dicts, use a list comprehension to extract only interfaces where status is "up".

**Task 16.3:** Use a dictionary comprehension to invert a dictionary (swap keys and values).

**Task 16.4:** Read a file of IP addresses and use a list comprehension to strip whitespace and filter out comment lines (starting with #).

**Task 16.5:** Rewrite this loop as a list comprehension:
```python
results = []
for device in devices:
    if device["vendor"] == "Cisco":
        results.append(device["hostname"].upper())
```

---


# Chapter 17: Object-Oriented Programming — Basics

## 17.1 Why OOP for Network Automation?

Classes let you model network objects: a Router, a Firewall, an API Client. Each has attributes (hostname, IP) and methods (connect, send_command, logout).

## 17.2 Creating a Class

### KByers Style — Check Point API Class

```python
class ChkptAPI:
    def __init__(self, host, username, password, mode="web_api",
                 api_version=None, ssl_verify=False):
        self.host = host
        self.username = username
        self.password = password

        if api_version is None:
            if mode == "web_api":
                api_version = "2"
            elif mode == "gaia_api":
                api_version = "1.8"

        self.ssl_verify = ssl_verify
        self.headers = {"Content-Type": "application/json"}
        self.base_url = f"https://{host}/{mode}/v{api_version}/"

# Usage
api_client = ChkptAPI(
    host="chkpnt-pod99.lasthop.io",
    username="admin",
    password="testpass",
    mode="gaia_api"
)
print(api_client.base_url)
# https://chkpnt-pod99.lasthop.io/gaia_api/v1.8/
```

## 17.3 Methods

```python
import requests
import json

class ChkptAPI:
    def __init__(self, host, username, password, mode="web_api",
                 api_version=None, ssl_verify=False):
        self.host = host
        self.username = username
        self.password = password
        if api_version is None:
            api_version = "2" if mode == "web_api" else "1.8"
        self.ssl_verify = ssl_verify
        self.headers = {"Content-Type": "application/json"}
        self.base_url = f"https://{host}/{mode}/v{api_version}/"

    def login(self):
        """Authenticate and store session ID."""
        login_payload = {"user": self.username, "password": self.password}
        url = self.base_url + "login"
        response = requests.post(
            url, data=json.dumps(login_payload),
            headers=self.headers, verify=self.ssl_verify,
        )
        resp_struct = response.json()
        self.headers["X-chkp-sid"] = resp_struct["sid"]

    def call(self, endpoint, payload=None):
        """Make an API call."""
        url = self.base_url + endpoint
        if payload is None:
            payload = {}
        response = requests.post(
            url, data=json.dumps(payload),
            headers=self.headers, verify=self.ssl_verify
        )
        return response

    def logout(self):
        """Logout and remove session."""
        res = self.call("logout")
        if res.status_code == 200:
            self.headers.pop("X-chkp-sid", None)
```

### PyNEng Style — Simple Device Class

```python
class NetworkDevice:
    def __init__(self, hostname, ip, vendor):
        self.hostname = hostname
        self.ip = ip
        self.vendor = vendor
        self.interfaces = []

    def add_interface(self, name, ip=None):
        self.interfaces.append({"name": name, "ip": ip})

    def show_info(self):
        print(f"Device: {self.hostname} ({self.ip}) - {self.vendor}")
        for intf in self.interfaces:
            print(f"  {intf['name']}: {intf.get('ip', 'no ip')}")

# Usage
rtr = NetworkDevice("core-rtr-01", "10.0.0.1", "Cisco")
rtr.add_interface("Gi0/0", "10.0.0.1")
rtr.add_interface("Gi0/1", "10.0.1.1")
rtr.show_info()
```

---

## Chapter 17 Lab Tasks

**Task 17.1:** Create a `Router` class with attributes: hostname, ip, vendor, model. Add a `__init__` method and a `show_info()` method. Create 2 instances and call `show_info()` on each.

**Task 17.2:** Add an `add_interface()` method to your Router class that appends interface dicts to a list attribute. Add 3 interfaces and print the list.

**Task 17.3:** Create a `Firewall` class with a `login()` method that sets `self.authenticated = True` and a `logout()` method that sets it to `False`. Test the state transitions.

**Task 17.4:** Create an API client class with `__init__`, `login`, `call`, and `logout` methods (stubs that print messages). Chain them together in a test script.

**Task 17.5:** Create a class `VlanManager` that stores VLANs in a set. Add methods: `add_vlan()`, `remove_vlan()`, `list_vlans()`, and `common_vlans(other_manager)`.

---

# Chapter 18: OOP — Special Methods and Inheritance

## 18.1 Special (Dunder) Methods

```python
class IPAddress:
    def __init__(self, ip):
        self.ip = ip
        self.octets = [int(o) for o in ip.split(".")]

    def __str__(self):
        return self.ip

    def __repr__(self):
        return f"IPAddress('{self.ip}')"

    def __eq__(self, other):
        return self.ip == other.ip

    def __lt__(self, other):
        return self.octets < other.octets

ip1 = IPAddress("10.0.0.1")
ip2 = IPAddress("10.0.0.2")
print(ip1)              # 10.0.0.1
print(repr(ip1))        # IPAddress('10.0.0.1')
print(ip1 == ip2)       # False
print(ip1 < ip2)        # True
```

## 18.2 Inheritance

```python
class NetworkDevice:
    def __init__(self, hostname, ip):
        self.hostname = hostname
        self.ip = ip

    def connect(self):
        print(f"Connecting to {self.hostname} at {self.ip}")

class CiscoRouter(NetworkDevice):
    def __init__(self, hostname, ip, ios_version):
        super().__init__(hostname, ip)
        self.ios_version = ios_version
        self.vendor = "Cisco"

    def show_version(self):
        return f"{self.hostname} running IOS {self.ios_version}"

class AristaSwitch(NetworkDevice):
    def __init__(self, hostname, ip, eos_version):
        super().__init__(hostname, ip)
        self.eos_version = eos_version
        self.vendor = "Arista"

# Usage
rtr = CiscoRouter("rtr1", "10.0.0.1", "17.3.4a")
rtr.connect()                    # inherited from NetworkDevice
print(rtr.show_version())       # CiscoRouter method
```

---

## Chapter 18 Lab Tasks

**Task 18.1:** Add `__str__` and `__repr__` methods to your Router class from Chapter 17. Print an instance with both `print()` and `repr()`.

**Task 18.2:** Create a base class `NetworkDevice` and two subclasses `Router` and `Switch`. Each subclass should add vendor-specific methods.

**Task 18.3:** Create an `IPAddress` class with `__eq__` and `__lt__` so IP addresses can be compared and sorted. Sort a list of 5 IP objects.

**Task 18.4:** Demonstrate `super().__init__()` by creating a `CiscoFirewall` class that inherits from `NetworkDevice` and adds firewall-specific attributes.

**Task 18.5:** Create a context manager class `DeviceConnection` with `__enter__` and `__exit__` methods that simulate connecting and disconnecting from a device.

---

# Chapter 19: OS Interaction — subprocess, pathlib, os

## 19.1 subprocess

### KByers Style

```python
#!/usr/bin/env python
import subprocess

# subprocess.run() — recommended approach
command = ["ping", "-c", "4", "google.com"]
result = subprocess.run(command, capture_output=True, text=True)

print(result.stdout)
print(result.stderr)
print(result.returncode)      # 0 = success
```

## 19.2 pathlib

### KByers Style — Modern File Path Handling

```python
from pathlib import Path
import yaml

home = Path.home()
fw_file = home / "python_course" / "firewalls.yml"

print(f"Exists: {fw_file.exists()}")
print(f"Is file: {fw_file.is_file()}")
print(f"Parent dir: {fw_file.parent}")

# Create directories
work_dir = home / "tmp_work"
if not work_dir.exists():
    work_dir.mkdir(parents=True, exist_ok=True)

# Find all JSON files recursively
course_dir = home / "python_course"
for f in course_dir.rglob("*.json"):
    print(f)
```

## 19.3 os.system() vs subprocess

```python
import os

# os.system() — simple but limited (no output capture)
os.system("ping -c 4 google.com")

# subprocess — full control (preferred)
import subprocess
result = subprocess.run(["ping", "-c", "4", "google.com"],
                       capture_output=True, text=True)
print(result.stdout)
```

---

## Chapter 19 Lab Tasks

**Task 19.1:** Use `subprocess.run()` to execute `ping -c 3 8.8.8.8`. Print stdout, stderr, and the return code.

**Task 19.2:** Use `pathlib.Path` to check if `/etc/hosts` exists, print its parent directory, and read its first 5 lines.

**Task 19.3:** Use `pathlib` to find all `.py` files in your home directory (recursively). Count them and print the total.

**Task 19.4:** Write a function that takes a command as a list and uses `subprocess.Popen` to run it, returning stdout, stderr, and the return code.

**Task 19.5:** Use `pathlib` to create a directory structure: `~/lab/configs/`, `~/lab/logs/`, `~/lab/scripts/`. Verify each exists.

---

# Chapter 20: Connecting to Network Devices (Netmiko)

## 20.1 First Connection

### Netmiko Course Style

```python
import os
from getpass import getpass
from netmiko import ConnectHandler

password = os.getenv("NETMIKO_PASSWORD") if os.getenv("NETMIKO_PASSWORD") else getpass()

# Simple connection
net_connect = ConnectHandler(
    device_type="cisco_ios",
    host="cisco3.lasthop.io",
    username="pyclass",
    password=password,
)
print(net_connect.find_prompt())
net_connect.disconnect()
```

## 20.2 Using a Device Dictionary

```python
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

## 20.3 Context Manager (Auto-Disconnect)

```python
my_device = {
    "device_type": "cisco_ios",
    "host": "cisco3.lasthop.io",
    "username": "pyclass",
    "password": password,
}

with ConnectHandler(**my_device) as net_connect:
    print(net_connect.find_prompt())
# Automatically disconnected here
```

## 20.4 Session Logging

```python
my_device = {
    "device_type": "cisco_ios",
    "host": "cisco3.lasthop.io",
    "username": "pyclass",
    "password": password,
    "session_log": "cisco3.out",    # Logs everything to file
}

with ConnectHandler(**my_device) as net_connect:
    output = net_connect.send_command("show ip int brief")
    print(output)
```

## 20.5 Check Point Gaia Connections

### KByers Style

```python
from netmiko import ConnectHandler

chkpt_fw = {
    "host": "chkpnt-pod99.lasthop.io",
    "device_type": "checkpoint_gaia",
    "username": "admin",
    "use_keys": True,
    "key_file": "/home/user/.ssh/eu-sshkey.pem",
    "session_log": "output.log",
}

with ConnectHandler(**chkpt_fw) as nc:
    print(nc.find_prompt())
    data = nc.send_command("show version all")
    print(data)
```

---

## Chapter 20 Lab Tasks

**Task 20.1:** Write a Netmiko script that connects to a Cisco IOS device and prints the prompt. Use a device dictionary and context manager.

**Task 20.2:** Modify the script to enable session logging to a file. Verify the log file contents after running.

**Task 20.3:** Write a script that connects to an NX-OS device using a different `device_type`. Print the prompt.

**Task 20.4:** Create a function `connect_device(device_dict)` that handles the connection and returns the prompt. Handle `NetmikoAuthenticationException` and `NetmikoTimeoutException`.

**Task 20.5:** Write a script that reads device parameters from a YAML file and connects to each device, printing the prompt.

---

# Chapter 21: Sending Commands with Netmiko

## 21.1 send_command()

```python
from netmiko import ConnectHandler

with ConnectHandler(**device) as net_connect:
    # send_command() waits for the prompt before returning
    output = net_connect.send_command("show ip interface brief")
    print(output)

    # With TextFSM parsing
    output = net_connect.send_command("show ip int brief", use_textfsm=True)
    print(output)    # Returns list of dicts!
```

## 21.2 send_command_timing()

```python
# send_command_timing() uses time-based approach (no prompt detection)
output = net_connect.send_command_timing("show ip route")
print(output)
```

## 21.3 write_channel() and read_channel()

### Netmiko Course Style — Low-Level Control

```python
import time
from netmiko import ConnectHandler

with ConnectHandler(**my_device) as net_connect:
    # Send command directly to channel
    net_connect.write_channel("show ip int brief\n")
    time.sleep(1)
    output = net_connect.read_channel()
    print(output)
```

---

## Chapter 21 Lab Tasks

**Task 21.1:** Connect to a device and use `send_command()` to gather `show version`, `show ip route`, and `show interfaces`. Print each output.

**Task 21.2:** Use `send_command()` with `use_textfsm=True` to parse `show ip int brief` into structured data. Loop through the results.

**Task 21.3:** Write a script that sends a command and saves the output to a text file named `{hostname}_{command}.txt`.

**Task 21.4:** Use `write_channel()` and `read_channel()` to manually interact with a device. Send "show clock" and read the response.

**Task 21.5:** Write a function that takes a device dict and a list of commands, connects, runs all commands, and returns a dictionary mapping each command to its output.

---

# Chapter 22: Device Configuration with Netmiko

## 22.1 send_config_set()

```python
from netmiko import ConnectHandler

cfg_commands = [
    "logging buffered 20000",
    "logging console notifications",
    "no logging monitor",
]

with ConnectHandler(**device) as net_connect:
    output = net_connect.send_config_set(cfg_commands)
    print(output)
```

## 22.2 send_config_from_file()

```python
# File: changes.cfg
# interface Loopback99
#  ip address 10.99.99.1 255.255.255.255

with ConnectHandler(**device) as net_connect:
    output = net_connect.send_config_from_file("changes.cfg")
    print(output)
```

## 22.3 Enable Mode and Config Mode

### Netmiko Course Style

```python
with ConnectHandler(**device) as net_connect:
    # Enable mode
    net_connect.enable()
    print(net_connect.find_prompt())    # rtr1#

    # Enter config mode manually
    net_connect.config_mode()
    print(net_connect.find_prompt())    # rtr1(config)#

    # Exit config mode
    net_connect.exit_config_mode()
```

## 22.4 Save Configuration

```python
with ConnectHandler(**device) as net_connect:
    net_connect.send_config_set(["interface Lo99", "ip address 10.99.99.1 255.255.255.255"])
    net_connect.save_config()       # write memory / copy run start
```

## 22.5 Juniper Commit Operations

### Netmiko Course Style

```python
vmx = {
    "device_type": "juniper_junos",
    "host": "vmx1.lasthop.io",
    "username": "pyclass",
    "password": password,
}

with ConnectHandler(**vmx) as net_connect:
    cfg_commands = [
        "set system syslog archive size 110k files 3",
        "set system time-zone America/New_York",
    ]
    output = net_connect.send_config_set(cfg_commands)
    print(output)

    # Commit with comment
    output = net_connect.commit(
        comment="Configuration change using Netmiko"
    )
    print(output)
```

---

## Chapter 22 Lab Tasks

**Task 22.1:** Write a script that pushes 3 configuration commands to a Cisco IOS device using `send_config_set()`. Print the output.

**Task 22.2:** Create a config file with 5 interface commands. Use `send_config_from_file()` to apply them.

**Task 22.3:** Write a script that enters enable mode, verifies the privilege level, enters config mode, makes a change, exits, and saves.

**Task 22.4:** Write a reusable function `apply_config(device, commands)` that connects, pushes config, saves, and returns the output.

**Task 22.5:** Write a script for a Juniper device that sends configuration commands and commits with a comment. Verify the commit history.

---


# Chapter 23: REST APIs with Python (requests)

## 23.1 GET Requests

```python
import requests

# Simple GET
response = requests.get("https://api.ipify.org?format=json")
print(response.status_code)    # 200
print(response.json())         # {'ip': '203.0.113.5'}
```

## 23.2 POST Requests with Authentication

### KByers Style — Check Point API Authentication

```python
import requests
import json
import os
from dotenv import load_dotenv

load_dotenv()
host = "chkpnt-pod99.lasthop.io"
base_url = f"https://{host}/gaia_api/v1.8/"
user = "admin"
password = os.environ["CHKP_ADMIN"]

# Login (POST)
url = f"{base_url}login"
headers = {"Content-Type": "application/json"}
login_payload = {"user": user, "password": password}

response = requests.post(
    url, data=json.dumps(login_payload),
    headers=headers, verify=False
)

session_id = response.json()["sid"]
headers["X-chkp-sid"] = session_id

# Make API calls with session
url = f"{base_url}show-api-versions"
response = requests.post(url, data=json.dumps({}), headers=headers, verify=False)
print(response.json())

# Logout
url = f"{base_url}logout"
response = requests.post(url, data=json.dumps({}), headers=headers, verify=False)
```

## 23.3 Environment Variables and .env Files

```python
import os
from dotenv import load_dotenv

# .env file:
# CHKP_ADMIN=mysecretpassword
# CHKP_EXPERT=myexpertpassword

load_dotenv()
admin_pass = os.environ["CHKP_ADMIN"]
expert_pass = os.environ["CHKP_EXPERT"]
```

---

## Chapter 23 Lab Tasks

**Task 23.1:** Use `requests.get()` to fetch data from a public API (e.g., https://api.ipify.org?format=json). Print the response status code and JSON body.

**Task 23.2:** Write a function `api_login(base_url, username, password)` that performs a POST login and returns the session headers. Include error handling.

**Task 23.3:** Write a function `api_call(base_url, endpoint, headers, payload)` that makes a POST API call and returns the response. Test it.

**Task 23.4:** Create a `.env` file with credentials and use `python-dotenv` to load them. Verify they are accessible via `os.environ`.

**Task 23.5:** Write a complete script that logs in to an API, makes 2 API calls, and logs out. Structure it with functions and `if __name__ == "__main__"`.

---

# Chapter 24: Concurrent Connections — Threads and Processes

## 24.1 Why Concurrency?

Connecting to 100 devices sequentially takes minutes. Concurrency lets you connect to many devices simultaneously.

## 24.2 ThreadPoolExecutor

### KByers Style

```python
from concurrent.futures import ThreadPoolExecutor, as_completed
from datetime import datetime
from netmiko import ConnectHandler

def ssh_conn(device):
    net_connect = ConnectHandler(**device)
    return net_connect.find_prompt()

if __name__ == "__main__":
    start_time = datetime.now()
    max_threads = 4

    pool = ThreadPoolExecutor(max_threads)

    future_list = []
    for a_device in device_list:
        future = pool.submit(ssh_conn, a_device)
        future_list.append(future)

    for future in as_completed(future_list):
        print("Result: " + future.result())

    end_time = datetime.now()
    print(f"Elapsed time: {end_time - start_time}")
```

## 24.3 Context Manager Style

```python
from concurrent.futures import ThreadPoolExecutor, as_completed

with ThreadPoolExecutor(max_workers=4) as pool:
    future_list = []
    for device in device_list:
        future = pool.submit(ssh_conn, device)
        future_list.append(future)

    for future in as_completed(future_list):
        print("Result: " + future.result())
```

## 24.4 ProcessPoolExecutor

```python
from concurrent.futures import ProcessPoolExecutor, as_completed

# Same API, just swap ThreadPoolExecutor for ProcessPoolExecutor
with ProcessPoolExecutor(max_workers=4) as pool:
    future_list = []
    for device in device_list:
        future = pool.submit(ssh_conn, device)
        future_list.append(future)

    for future in as_completed(future_list):
        host, data = future.result()
        print(f"{host}: {data}")
```

## 24.5 Threads vs Processes

| Feature | ThreadPoolExecutor | ProcessPoolExecutor |
|---|---|---|
| Best for | I/O bound (SSH, API calls) | CPU bound (parsing) |
| GIL impact | Limited by GIL | Bypasses GIL |
| Memory | Shared | Separate per process |
| Use case | Network automation | Data processing |

---

## Chapter 24 Lab Tasks

**Task 24.1:** Write a function `ssh_conn(device)` that simulates an SSH connection (sleep 1 second, return hostname). Use ThreadPoolExecutor with 5 threads to connect to 10 "devices".

**Task 24.2:** Measure the time difference between sequential execution (for loop) and concurrent execution (ThreadPoolExecutor) for 10 simulated connections.

**Task 24.3:** Use `as_completed()` to process results as they finish. Print each result with a timestamp showing the order of completion.

**Task 24.4:** Add error handling to your concurrent function: catch exceptions from individual futures and print error messages without crashing the whole batch.

**Task 24.5:** Write a concurrent script that reads devices from a YAML file, connects to each in parallel, collects `show version`, and writes results to a JSON file.

---

# Chapter 25: Jinja2 Configuration Templates

## 25.1 Basic Templates

```python
from jinja2 import Environment, FileSystemLoader

env = Environment(loader=FileSystemLoader("templates"))
template = env.get_template("interface.j2")

# Template file: templates/interface.j2
# interface {{ interface_name }}
#  ip address {{ ip_address }} {{ subnet_mask }}
#  no shutdown

output = template.render(
    interface_name="GigabitEthernet0/1",
    ip_address="10.0.0.1",
    subnet_mask="255.255.255.0"
)
print(output)
```

## 25.2 Loops and Conditionals in Templates

```jinja2
{# templates/switch_config.j2 #}
hostname {{ hostname }}
!
{% for vlan in vlans %}
vlan {{ vlan.id }}
 name {{ vlan.name }}
{% endfor %}
!
{% for intf in interfaces %}
interface {{ intf.name }}
{% if intf.mode == "access" %}
 switchport mode access
 switchport access vlan {{ intf.vlan }}
{% elif intf.mode == "trunk" %}
 switchport mode trunk
 switchport trunk allowed vlan {{ intf.allowed_vlans }}
{% endif %}
 no shutdown
{% endfor %}
```

---

## Chapter 25 Lab Tasks

**Task 25.1:** Create a Jinja2 template for a router interface config. Render it with 3 different sets of variables.

**Task 25.2:** Create a template with a for loop that generates VLAN configurations from a list of VLAN dicts.

**Task 25.3:** Add conditional logic to a template: if interface mode is "access", configure access mode; if "trunk", configure trunk.

**Task 25.4:** Write a script that reads device variables from a YAML file and renders a Jinja2 template for each device, writing output to separate files.

**Task 25.5:** Create a complete switch configuration template with hostname, VLANs, interfaces, and SNMP settings. Render it with realistic data.

---

# Chapter 26: Parsing Output with TextFSM

## 26.1 Netmiko + TextFSM

```python
from netmiko import ConnectHandler

with ConnectHandler(**device) as net_connect:
    # Automatic TextFSM parsing
    output = net_connect.send_command(
        "show ip interface brief",
        use_textfsm=True
    )

    # Returns list of dicts
    for interface in output:
        print(f"{interface['intf']:25} {interface['ipaddr']:16} {interface['status']}")
```

## 26.2 TextFSM Template Syntax

```
# show_ip_int_brief.textfsm
Value INTF (\S+)
Value IPADDR (\S+)
Value STATUS (up|down|administratively down)
Value PROTO (up|down)

Start
  ^${INTF}\s+${IPADDR}\s+\w+\s+\w+\s+${STATUS}\s+${PROTO} -> Record
```

---

## Chapter 26 Lab Tasks

**Task 26.1:** Use `send_command()` with `use_textfsm=True` to parse `show ip int brief` output. Print results as a formatted table.

**Task 26.2:** Write a custom TextFSM template to parse `show ip route` output. Extract network, mask, and next-hop.

**Task 26.3:** Parse `show interfaces` output to extract interface name, status, MTU, and bandwidth.

**Task 26.4:** Write a script that collects parsed data from 3 devices and combines results into a single report.

**Task 26.5:** Export TextFSM-parsed data to a CSV file for import into a spreadsheet.

---

# Chapter 27: Testing with pytest

## 27.1 Basic Tests

```python
# test_network_utils.py
from network_utils import validate_ip, calculate_subnet_hosts

def test_valid_ip():
    assert validate_ip("10.0.0.1") == True

def test_invalid_ip():
    assert validate_ip("999.0.0.1") == False

def test_subnet_hosts_24():
    assert calculate_subnet_hosts(24) == 254

def test_subnet_hosts_30():
    assert calculate_subnet_hosts(30) == 2
```

Run: `pytest test_network_utils.py -v`

---

## Chapter 27 Lab Tasks

**Task 27.1:** Write 3 pytest test functions for a `validate_ip()` function. Test valid IPs, invalid IPs, and edge cases.

**Task 27.2:** Write tests for a `generate_hostname()` function. Test default values and custom parameters.

**Task 27.3:** Use `pytest.raises()` to test that your custom exception is raised when expected.

**Task 27.4:** Create a test file with a `@pytest.fixture` that provides sample device data to multiple test functions.

**Task 27.5:** Write a test that verifies a function correctly reads a JSON file and returns the expected data structure. Use `tmp_path` fixture.

---

# Chapter 28: Working with Databases (SQLite)

## 28.1 SQLite Basics

```python
import sqlite3

# Connect (creates file if not exists)
conn = sqlite3.connect("network_inventory.db")
cursor = conn.cursor()

# Create table
cursor.execute("""
    CREATE TABLE IF NOT EXISTS devices (
        id INTEGER PRIMARY KEY AUTOINCREMENT,
        hostname TEXT NOT NULL,
        ip TEXT NOT NULL,
        vendor TEXT,
        model TEXT,
        site TEXT
    )
""")

# Insert data
cursor.execute(
    "INSERT INTO devices (hostname, ip, vendor, model, site) VALUES (?, ?, ?, ?, ?)",
    ("rtr1", "10.0.0.1", "Cisco", "ISR4431", "NYC")
)
conn.commit()

# Query data
cursor.execute("SELECT hostname, ip, vendor FROM devices WHERE site = ?", ("NYC",))
rows = cursor.fetchall()
for row in rows:
    print(f"{row[0]:15} {row[1]:16} {row[2]}")

conn.close()
```

---

## Chapter 28 Lab Tasks

**Task 28.1:** Create a SQLite database with a `devices` table. Insert 5 devices and query all of them.

**Task 28.2:** Write a function `add_device(conn, hostname, ip, vendor)` and `get_all_devices(conn)` to abstract database operations.

**Task 28.3:** Query the database for all Cisco devices and print a formatted table.

**Task 28.4:** Write a script that reads devices from a YAML file and inserts them into a SQLite database.

**Task 28.5:** Create a second table `interfaces` linked to `devices` via foreign key. Insert interface data and join the tables in a query.

---

# Chapter 29: Building a Complete Network Automation Project

## 29.1 Project Structure

### KByers Style — Real-World Check Point Automation

```
firewall_automation/
├── .env                          # Credentials (never commit to git!)
├── .gitignore                    # Excludes .env, *.pyc, __pycache__
├── requirements.txt              # pip dependencies
├── main.py                       # Entry point
├── config/
│   ├── devices.yaml              # Device inventory
│   └── blocked_ips.txt           # IP blocklist
├── lib/
│   ├── __init__.py
│   ├── chkpt_api.py              # API client class
│   ├── object_funcs.py           # Host/network object functions
│   ├── policy_funcs.py           # Firewall rule functions
│   └── exceptions.py             # Custom exceptions
├── templates/
│   └── switch_config.j2          # Jinja2 templates
└── tests/
    ├── test_api.py
    └── test_objects.py
```

## 29.2 Putting It All Together

```python
#!/usr/bin/env python
"""Main automation script — complete workflow."""
import os
from dotenv import load_dotenv
from lib.chkpt_api import ChkptAPI
from lib.object_funcs import cfg_host_objects
from lib.policy_funcs import cfg_fw_rules, install_fw_policy
from lib.exceptions import ChkPntConfigError

def main():
    load_dotenv()
    host = "chkpnt-pod99.lasthop.io"
    username = "admin"
    password = os.environ["CHKP_ADMIN"]

    api_client = ChkptAPI(host=host, username=username, password=password)

    try:
        api_client.login()
        print("[1/4] Configuring host objects...")
        cfg_host_objects(api_client, host_objects)
        print("[2/4] Configuring firewall rules...")
        cfg_fw_rules(api_client, fw_rules)
        print("[3/4] Publishing changes...")
        api_client.call("publish")
        print("[4/4] Installing policy...")
        install_fw_policy(api_client)
        print("Automation complete!")
    except ChkPntConfigError as e:
        print(f"Configuration failed: {e}")
    finally:
        api_client.logout()

if __name__ == "__main__":
    main()
```

---

## Chapter 29 Lab Tasks

**Task 29.1:** Create a project directory structure as shown above. Initialize a git repo and create a `.gitignore` that excludes `.env`, `__pycache__`, and `*.pyc`.

**Task 29.2:** Write a `requirements.txt` with all packages needed for the project. Use `pip freeze` as a starting point, then clean it up.

**Task 29.3:** Create a complete automation script that: reads devices from YAML, connects via Netmiko, collects show commands, and writes results to JSON.

**Task 29.4:** Add error handling, logging (using `logging` module), and a retry mechanism to your script.

**Task 29.5:** Write pytest tests for at least 3 functions in your project. Run them and verify all pass.

---


# Appendix A: Lab Task Answers

---

## Chapter 1 Answers

**1.1:**
```bash
python3 -m venv ~/netauto
source ~/netauto/bin/activate
pip install netmiko requests pyyaml rich
pip list
```

**1.2:**
```python
# my_info.py
# This script displays my network engineer info
name = "John Smith"
role = "Network Engineer"
device_count = 150
print(f"Name: {name}")
print(f"Role: {role}")
print(f"Devices managed: {device_count}")
```

**1.3:**
```python
>>> 255 * 255        # 65025 (int)
>>> 10 / 3           # 3.3333... (float - division always returns float)
>>> 2 ** 32          # 4294967296 (int)
```

**1.4:**
```bash
mkdir ~/my_project && cd ~/my_project
git init
echo 'print("Hello!")' > hello.py
git add hello.py
git commit -m "first commit"
git log
```

**1.5:**
```python
from rich import print
print("[bold green]Router connected![/bold green]")
print("[bold red]Firewall blocked![/bold red]")
```

---

## Chapter 2 Answers

**2.1:**
```python
hostname = "core-rtr-01"
ip_address = "10.10.10.1"
model = "ISR4431"
ios_version = "17.3.4a"
uptime_days = 365
print(f"Hostname: {hostname}")
print(f"IP: {ip_address}")
print(f"Model: {model}")
print(f"IOS: {ios_version}")
print(f"Uptime: {uptime_days} days")
```

**2.2:**
```python
for prefix in [24, 16, 8]:
    hosts = 2 ** (32 - prefix) - 2
    print(f"/{prefix}: {hosts} usable hosts")
# /24: 254, /16: 65534, /8: 16777214
```

**2.3:**
```python
print(bin(192))              # 0b11000000
print(hex(192))              # 0xc0
decimal = int("C0A80001", 16)
print(decimal)                # 3232235521
# That's 192.168.0.1 (C0=192, A8=168, 00=0, 01=1)
```

**2.4:**
```python
sent = 1000
received = 987
lost = sent - received
loss_pct = round((lost / sent) * 100, 2)
print(f"Packet loss: {loss_pct}%")   # 1.3%
```

**2.5:**
```python
bandwidth_gbps = 10.0
utilization = 0.73
used_gbps = bandwidth_gbps * utilization     # 7.3 Gbps
used_mbps = used_gbps * 1000                  # 7300 Mbps
bits_per_sec = used_gbps * 1_000_000_000      # 7,300,000,000 bps
bytes_in_60s = (bits_per_sec * 60) / 8
megabytes = bytes_in_60s / 1_000_000
print(f"Used: {used_mbps} Mbps")
print(f"Data in 60s: {megabytes:,.0f} MB")    # ~54,750 MB
```

---

## Chapter 3 Answers

**3.1:**
```python
show_ip = "Interface Gi0/1, IP 192.168.1.1/24, Status up"
parts = show_ip.split(", ")
interface = parts[0].split(" ")[1]
ip_mask = parts[1].split(" ")[1]
ip_address, mask = ip_mask.split("/")
status = parts[2].split(" ")[1]
print(f"Interface: {interface}")
print(f"IP: {ip_address}")
print(f"Mask: /{mask}")
print(f"Status: {status}")
```

**3.2:**
```python
commands = [
    "interface GigabitEthernet0/1",
    " switchport mode access",
    " switchport access vlan 10",
    " spanning-tree portfast",
    " no shutdown"
]
config_block = "\n".join(commands)
print(config_block)
```

**3.3:**
```python
ipv6 = "2001:0db8:0000:0042:0000:0000:0000:0001"
hextets = ipv6.split(":")
compressed = [h.lstrip("0") or "0" for h in hextets]
result = ":".join(compressed)
print(result)    # 2001:db8:0:42:0:0:0:1
```

**3.4:**
```python
print(f"{'Hostname':<20} {'IP Address':<16} {'Status':^10}")
print(f"{'-'*20} {'-'*16} {'-'*10}")
print(f"{'core-rtr-01':<20} {'10.0.0.1':<16} {'up':^10}")
print(f"{'sw-access-01':<20} {'10.0.0.2':<16} {'up':^10}")
print(f"{'fw-edge-01':<20} {'10.0.0.3':<16} {'down':^10}")
```

**3.5:**
```python
intf = "GigabitEthernet0/0/0"
print(intf.startswith("Gig"))     # True
print("0/0" in intf)              # True
print(intf.endswith("/0"))        # True
```

---

## Chapter 4 Answers

**4.1:**
```python
interfaces = [f"Gi0/{i}" for i in range(8)]
print(f"Third: {interfaces[2]}")
print(f"Last: {interfaces[-1]}")
print(f"Total: {len(interfaces)}")
```

**4.2:**
```python
vlans = [10, 20, 30, 40, 50, 60]
vlans.append(70);            print(vlans)
vlans.insert(0, 5);          print(vlans)
vlans.remove(30);            print(vlans)
vlans.sort();                print(vlans)
# Final: [5, 10, 20, 40, 50, 60, 70]
```

**4.3:**
```python
core = ["rtr1", "rtr2"]
access = ["sw1", "sw2", "sw3"]
all_devices_1 = core + access
all_devices_2 = core.copy()
all_devices_2.extend(access)
print(all_devices_1)
print(all_devices_2)
```

**4.4:**
```python
ips = ["10.0.0.1", "10.0.0.2", "10.0.0.3", "10.0.0.4", "10.0.0.5"]
first = ips.pop(0)
last = ips.pop()
print(f"Removed: {first}, {last}")
print(f"Remaining: {ips}")
```

**4.5:**
```python
config_lines = ["interface Gi0/1", "switchport mode access", "switchport access vlan 10", "no shutdown"]
reversed_lines = config_lines[::-1]
print(reversed_lines)
```

---

## Chapter 5 Answers

**5.1:**
```python
device = {
    "hostname": "rtr1", "ip": "10.0.0.1", "vendor": "Cisco",
    "model": "ISR4431", "os_version": "17.3.4a", "site": "NYC"
}
for key in device:
    print(f"{key}: {device[key]} | get: {device.get(key)}")
```

**5.2:**
```python
fw_rule = {
    "name": "Allow_Web",
    "source": {"type": "host", "ip": "10.0.0.5"},
    "destination": {"type": "network", "ip": "192.168.1.0", "mask": "/24"},
    "action": "permit"
}
dest_ip = fw_rule["destination"]["ip"]
print(f"Destination: {dest_ip}")    # 192.168.1.0
```

**5.3:**
```python
rtr1 = {"hostname": "rtr1", "ip": "10.0.0.1", "vendor": "Cisco"}
rtr2 = {"hostname": "rtr2", "ip": "10.0.0.2", "vendor": "Juniper"}
inventory = {rtr1["hostname"]: rtr1, rtr2["hostname"]: rtr2}
print(inventory)
```

**5.4:**
```python
device = {"hostname": "rtr1", "ip": "10.0.0.1", "vendor": "Cisco", "model": "ISR4431"}
for key, value in device.items():
    print(f"{key:>12}: {value}")
```

**5.5:**
```python
device = {"device_type": "arista_eos", "host": "10.0.0.1", "username": "admin", "password": "secret"}
device["session_log"] = "arista.log"
device["device_type"] = "arista_eos_ssh"
device.pop("session_log")
print(device)
```

---

## Chapter 6 Answers

**6.1:**
```python
dns = ("8.8.8.8", "8.8.4.4", "1.1.1.1")
# dns[0] = "9.9.9.9"  # TypeError: 'tuple' object does not support item assignment
primary, secondary, tertiary = dns
print(f"Primary: {primary}, Secondary: {secondary}, Tertiary: {tertiary}")
```

**6.2:**
```python
sw1 = {10, 20, 30, 40, 50}
sw2 = {30, 40, 50, 60, 70}
print(f"All: {sw1 | sw2}")
print(f"Common: {sw1 & sw2}")
print(f"Only sw1: {sw1 - sw2}")
print(f"Unique to one: {sw1 ^ sw2}")
```

**6.3:**
```python
dupes = [10, 20, 30, 10, 20, 40]
unique_set = set(dupes)
print(unique_set)                    # {10, 20, 30, 40}
sorted_list = sorted(unique_set)
print(sorted_list)                   # [10, 20, 30, 40]
```

**6.4:**
```python
values = [0, "", [], {}, None, "hello", [1], 42]
for v in values:
    print(f"{str(v):>10} -> {bool(v)}")
```

**6.5:**
```python
current = {"permit_web", "permit_ssh", "deny_telnet"}
desired = {"permit_web", "permit_ssh", "permit_dns"}
to_add = desired - current
to_remove = current - desired
print(f"Add: {to_add}")        # {'permit_dns'}
print(f"Remove: {to_remove}")  # {'deny_telnet'}
```

---

## Chapters 7-29 Answers (Selected Key Solutions)

**7.1:**
```python
vlan = int(input("Enter VLAN: "))
if vlan == 1:
    print("Default VLAN — do not use")
elif 2 <= vlan <= 1000:
    print("Standard VLAN")
elif 1001 <= vlan <= 4094:
    print("Extended VLAN")
else:
    print("Invalid VLAN")
```

**8.1:**
```python
ips = [f"10.0.0.{i}" for i in range(1, 11)]
for idx, ip in enumerate(ips, start=1):
    print(f"{idx}. {ip}")
```

**9.1:**
```python
def generate_hostname(site, role, number="01"):
    return f"{site}-{role}-{number}"

print(generate_hostname("NYC", "RTR"))         # NYC-RTR-01
print(generate_hostname("LAX", "SW", "05"))    # LAX-SW-05
```

**12.3:**
```python
class InvalidVlanError(Exception):
    pass

def validate_vlan(vlan_id):
    if not 1 <= vlan_id <= 4094:
        raise InvalidVlanError(f"VLAN {vlan_id} is outside valid range 1-4094")
    return True

try:
    validate_vlan(5000)
except InvalidVlanError as e:
    print(e)
```

**16.1:**
```python
ips = [f"192.168.1.{i}" for i in range(1, 21)]
print(ips)
```

**17.1:**
```python
class Router:
    def __init__(self, hostname, ip, vendor, model):
        self.hostname = hostname
        self.ip = ip
        self.vendor = vendor
        self.model = model

    def show_info(self):
        print(f"{self.hostname} ({self.ip}) - {self.vendor} {self.model}")

rtr1 = Router("core-rtr-01", "10.0.0.1", "Cisco", "ISR4431")
rtr2 = Router("edge-rtr-01", "10.0.0.2", "Juniper", "MX204")
rtr1.show_info()
rtr2.show_info()
```

**20.1:**
```python
from netmiko import ConnectHandler
from getpass import getpass

device = {
    "device_type": "cisco_ios",
    "host": "192.168.1.1",
    "username": "admin",
    "password": getpass(),
}

with ConnectHandler(**device) as nc:
    print(nc.find_prompt())
```

**24.1:**
```python
from concurrent.futures import ThreadPoolExecutor, as_completed
import time

def ssh_conn(device):
    time.sleep(1)
    return f"Connected to {device['hostname']}"

devices = [{"hostname": f"rtr{i}"} for i in range(1, 11)]

with ThreadPoolExecutor(max_workers=5) as pool:
    futures = [pool.submit(ssh_conn, d) for d in devices]
    for future in as_completed(futures):
        print(future.result())
```

**29.3:**
```python
import yaml
import json
from netmiko import ConnectHandler

with open("devices.yaml") as f:
    devices = yaml.safe_load(f)

results = {}
for device in devices:
    hostname = device["hostname"]
    with ConnectHandler(**device) as nc:
        results[hostname] = {
            "prompt": nc.find_prompt(),
            "version": nc.send_command("show version"),
        }

with open("results.json", "w") as f:
    json.dump(results, f, indent=2)

print(f"Collected data from {len(results)} devices")
```

---

*End of Lab Guide*

**Sources:** LPTHW (Zed Shaw), PyNEng (Natasha Samoylenko), Python Course & Netmiko Course (Kirk Byers)

**Total Chapters:** 29 + Appendix | **Total Lab Tasks:** 145 with answers
