# Python for Network Engineers: The Complete Lab Guide

**From First Script to AI-Powered Network Automation**

---

## About This Book

This book teaches Python programming through the lens of network engineering. Every example uses real networking scenarios — IP addresses instead of "Hello World," device inventories instead of shopping lists, and SSH automation instead of web scrapers.

This book is designed for network engineers, security architects, and infrastructure professionals who want to automate their daily work with Python. No prior programming experience is required.


### How to Read This Book

Each chapter follows this structure:

1. **Introduction** — what the chapter covers and why it matters for network engineers
2. **Concepts with examples** — every concept is demonstrated with networking-relevant code
3. **Note/Warning/Tip blocks** — extra context, common gotchas, and best practices
4. **Section summaries** — brief recap after each major section
5. **Tasks** — hands-on lab exercises with clear descriptions (answers in the Appendix)

All examples use real networking scenarios — IP addresses, device inventories, SSH connections, and API calls. The code progresses from simple interactive examples to production-ready automation scripts.

---

## Table of Contents

### Part I. Python Fundamentals

- [1. Preparing the Working Environment](#1-preparing-the-working-environment)
- [2. Variables and Data Types: Numbers](#2-variables-and-data-types-numbers)
- [3. Strings](#3-strings)
- [4. Lists](#4-lists)
- [5. Dictionaries](#5-dictionaries)
- [6. Tuples, Sets, and Booleans](#6-tuples-sets-and-booleans)
- [7. Control Structures: if/elif/else](#7-control-structures-ifelifelse)
- [8. Control Structures: Loops](#8-control-structures-loops)

### Part II. Code Reuse and Organization

- [9. Functions](#9-functions)
- [10. Working with Files](#10-working-with-files)
- [11. Data Serialization: CSV, JSON, YAML](#11-data-serialization-csv-json-yaml)
- [12. Exception Handling](#12-exception-handling)
- [13. Modules and Packages](#13-modules-and-packages)
- [14. Useful Built-in Functions](#14-useful-built-in-functions)

### Part III. Text Processing and Data Manipulation

- [15. Regular Expressions](#15-regular-expressions)
- [16. List Comprehensions and Generators](#16-list-comprehensions-and-generators)

### Part IV. Object-Oriented Programming

- [17. OOP Basics: Classes and Objects](#17-oop-basics-classes-and-objects)
- [18. Special Methods and Inheritance](#18-special-methods-and-inheritance)

### Part V. System and OS Interaction

- [19. OS Interaction: subprocess, pathlib, os](#19-os-interaction-subprocess-pathlib-os)

### Part VI. Network Device Automation

- [20. Connecting to Network Devices with Netmiko](#20-connecting-to-network-devices-with-netmiko)
- [21. Sending Show Commands](#21-sending-show-commands)
- [22. Sending Configuration Commands](#22-sending-configuration-commands)
- [23. REST APIs with Python](#23-rest-apis-with-python)
- [24. Concurrent Connections to Multiple Devices](#24-concurrent-connections-to-multiple-devices)

### Part VII. Templates and Parsing

- [25. Jinja2 Configuration Templates](#25-jinja2-configuration-templates)
- [26. Parsing Command Output with TextFSM](#26-parsing-command-output-with-textfsm)

### Part VIII. Quality and Storage

- [27. Testing with pytest](#27-testing-with-pytest)
- [28. Working with Databases](#28-working-with-databases)

### Part IX. Capstone Projects

- [29. Building a Complete Automation Project](#29-building-a-complete-automation-project)
- [30. Capstone: Progressive Network Automation Scripts](#30-capstone-progressive-network-automation-scripts)
- [31. Real-World Package Analysis: cisco_support](#31-real-world-package-analysis-cisco_support)

### Part X. AI-Powered Network Automation

- [32. Building a Netmiko AI Agent with OpenAI](#32-building-a-netmiko-ai-agent-with-openai)
- [33. Building an MCP Server for Claude](#33-building-an-mcp-server-for-claude)

### Appendix

- [Appendix A: Task Answers](#appendix-a-task-answers)

---

# Part I. Python Fundamentals

---

# 1. Preparing the Working Environment

This chapter covers:

- Why Python is the language of choice for network automation
- Installing Python and setting up a virtual environment
- Installing essential network automation packages
- Writing and running your first script
- Version control with Git

## Why Python for Network Engineers?

Python has become the standard language for network automation across the industry. Every major network vendor — Cisco, Arista, Juniper, Palo Alto, Cisco firewall, Fortinet — provides Python libraries or APIs for their platforms.

> **Note:** Python is the most common choice for network automation because it is a relatively simple language to learn, with rich library support for working with network equipment. The ecosystem includes Netmiko for SSH, NAPALM for multi-vendor abstraction, Nornir for orchestration, and pyATS/Genie for testing.

What you will automate with Python:

- SSH connections to routers and switches to collect show commands
- Configuration changes pushed to hundreds of devices simultaneously
- Parsing unstructured CLI output into structured data (JSON, CSV)
- REST API interactions with controllers (Cisco DNA Center, Meraki, firewall management APIs)
- Configuration generation from Jinja2 templates
- Compliance auditing and reporting

## Installing Python

Python 3.10 or later is required for all examples in this book.

**On Linux (Ubuntu/Debian):**

```bash
sudo apt update
sudo apt install -y python3 python3-pip python3-venv git
python3 --version
```

**On macOS:**

```bash
brew install python3
```

**On Windows:**

Download the installer from python.org. During installation, check the box that says "Add Python to PATH."

> **Tip:** It is important to get a working terminal and text editor before writing any code. Spend the time to set up properly — it will save you hours later.

## Virtual Environments

A virtual environment is an isolated Python installation where you can install packages without affecting your system Python. This is essential when working on multiple projects with different package requirements.

> **Note:** Virtual environments allow different projects to have different sets of installed packages. This is especially important because Python packages are updated frequently and different projects may need different versions.

```bash
# Create a virtual environment
python3 -m venv ~/netauto_venv

# Activate it
source ~/netauto_venv/bin/activate # Linux/macOS

# Your prompt changes to show the active environment:
# (netauto_venv) user@host:~$

# Install network automation packages
pip install netmiko paramiko requests pyyaml jinja2 rich textfsm
pip install python-dotenv ipdb
```

The `pip install` command downloads packages from PyPI (Python Package Index) and installs them into your virtual environment. These packages will not be available outside this environment.

> **Note:** The `rich` library provides colorful terminal output: `from rich import print`. It makes debugging easier by highlighting data structures with colors.

## Your First Script

Create a file called `first_script.py`:

```python
#!/usr/bin/env python
"""
My first network automation script.
This script demonstrates basic Python output.
"""

print("=" * 50)
print(" Network Automation with Python")
print("=" * 50)
print()
print("Devices to manage: 150")
print("Protocol: SSH (port 22)")
print("Status: Ready")
```

Run it from the terminal:

```bash
python3 first_script.py
```

Output:

```
==================================================
 Network Automation with Python
==================================================

Devices to manage: 150
Protocol: SSH (port 22)
Status: Ready
```

The `print()` function sends text to the terminal. The `"=" * 50` expression creates a string of 50 equal signs — a quick way to create visual separators. The `print()` with no arguments creates a blank line.

> **Tip:** "Type the code exactly. Run it. See what happens." Repetition builds muscle memory.

> **Tip:** The Rich library provides enhanced output. Install it with `pip install rich` and use `from rich import print` for automatic syntax highlighting of data structures in the terminal.

## The Python Interactive Interpreter

The interactive interpreter lets you test individual Python expressions without creating a file. This is extremely useful for experimenting with string methods, testing small code fragments, or exploring how a library works.

```bash
# Start IPython (enhanced interpreter)
pip install ipython
ipython
```

```python
In [1]: 2 + 2
Out[1]: 4

In [2]: print("Hello, Network Engineer!")
Hello, Network Engineer!

In [3]: "GigabitEthernet0/1".split("/")
Out[3]: ['GigabitEthernet0', '1']

In [4]: exit()
```

> **Note:** IPython is recommended over the standard Python interpreter because it provides tab-completion, syntax highlighting, and the `?` help system. For example, typing `str.split?` in IPython shows the full documentation for the split method.

The numbers after `In` and `Out` are sequential command numbers in the current session. `Out` only appears when a command returns a value — `print()` displays text but returns `None`, so there is no `Out` line.

## Version Control with Git

> **Note:** [Chapter 1] covers Git in detail: "Git is a distributed version control system. Even if you work alone, git can be useful."

Every automation script you write should be tracked in Git. This gives you version history, the ability to undo mistakes, and collaboration capabilities.

```bash
# Initial setup (one time)
git config --global user.name "Your Name"
git config --global user.email "your_email@example.com"

# Create a repository for your automation scripts
mkdir ~/network_automation
cd ~/network_automation
git init

# Create your first script, add it, and commit
echo 'print("Hello")' > hello.py
git add hello.py
git commit -m "Add first script"

# View history
git log --oneline
```

> **Warning:** Never commit credentials (passwords, API keys, .env files) to Git. Always add `.env` and credential files to your `.gitignore` file.

### Section Summary

You now have a working Python development environment with a virtual environment, essential packages installed, the ability to write and run scripts, and Git for version control. Every subsequent chapter in this book builds on this foundation.

---

### Tasks

**Task 1.1**

Install Python 3 on your system. Create a virtual environment called `netauto`. Activate it and install the packages `netmiko`, `requests`, `pyyaml`, and `rich`. Run `pip list` to verify the installation.

**Task 1.2**

Write a script called `my_info.py` that prints your name, your role, and the number of devices you manage. Use at least one comment and one blank line for readability.

**Task 1.3**

Open IPython and perform these calculations: `255 * 255`, `10 / 3`, `2 ** 32`. Note the data type that Python returns for each result. What is the difference between `10 / 3` and `10 // 3`?

**Task 1.4**

Initialize a Git repository. Create a file called `hello.py`, add it, and commit with the message "first commit." Run `git log` and note the commit hash.

**Task 1.5**

Create a script that uses the `rich` library to print "Router connected!" in bold green and "Firewall blocked!" in bold red. Hint: `from rich import print` and use `[bold green]...[/bold green]` markup.

---

# 2. Variables and Data Types: Numbers

This chapter covers:

- Creating and naming variables
- Integer and float data types
- Mathematical operations
- Type conversions between numbers and strings
- Binary and hexadecimal conversions (essential for networking)
- Comparison operators

## Variables

A variable is a name that refers to a value stored in memory. In Python, you create a variable by assigning a value to it with the `=` sign. Python automatically determines the variable type based on the value assigned.

> **Note:** In Python, a variable is simply a name that refers to a value. Variables do not need to be declared and their type is determined dynamically.

```python
hostname = "core-rtr-01" # str (string)
interface_count = 48 # int (integer)
cpu_load = 23.7 # float (decimal number)
is_active = True # bool (boolean)
```

To check the type of a variable, use the built-in `type()` function:

```python
In [1]: hostname = "core-rtr-01"

In [2]: type(hostname)
Out[2]: str

In [3]: interface_count = 48

In [4]: type(interface_count)
Out[4]: int
```

> **Note:** Python 3.8+ debug formatting is extremely useful: `print(f"{hostname=}")` produces `hostname='core-rtr-01'`. This is extremely useful for debugging — it prints both the variable name and its value in one expression.

### Variable Naming Rules

Python has specific rules for variable names:

- Must start with a letter or underscore
- Can contain letters, numbers, and underscores
- Are case-sensitive (`vlan` and `VLAN` are different variables)
- Cannot be Python reserved words (`if`, `for`, `class`, etc.)

The Python community follows a naming convention called **snake_case** for variable and function names:

```python
# GOOD: descriptive snake_case names
interface_name = "GigabitEthernet0/1"
vlan_id = 100
subnet_mask = "255.255.255.0"
bgp_as_number = 65001

# BAD: avoid these patterns
x = "GigabitEthernet0/1" # too short, meaningless
InterfaceName = "Gi0/1" # PascalCase is for class names
# 2nd_vlan = 200 # cannot start with a number (SyntaxError)
```

> **Note:** The Python community follows PEP 8 — Python's official style guide. PEP 8 recommends snake_case for variables and functions, UPPER_CASE for constants, and PascalCase for class names.

## Numbers

Python has two main numeric types that network engineers use constantly: **int** (integers, whole numbers) and **float** (decimal numbers).

### Integer and Float Operations

```python
In [1]: vlans_per_switch = 4094
In [2]: switches = 5
In [3]: total_vlans = vlans_per_switch * switches
In [4]: total_vlans
Out[4]: 20470

In [5]: bandwidth_gbps = 10.0
In [6]: utilization = 0.73
In [7]: used_bandwidth = bandwidth_gbps * utilization
In [8]: used_bandwidth
Out[8]: 7.3
```

> **Note:** Division of integers always returns float, even when dividing evenly: `10 / 2` returns `5.0`, not `5`.

### Mathematical Operators

```python
In [1]: 10 / 3 # Division (always returns float)
Out[1]: 3.3333333333333335

In [2]: 10 // 3 # Floor division (rounds down to int)
Out[2]: 3

In [3]: 10 % 3 # Modulo (remainder)
Out[3]: 1

In [4]: 2 ** 32 # Exponentiation (2 to the power of 32)
Out[4]: 4294967296

In [5]: round(10/3, 2) # Round to 2 decimal places
Out[5]: 3.33
```

The exponentiation operator `**` is particularly useful for network calculations. For example, `2 ** 32` gives the total IPv4 address space (4,294,967,296), and `2 ** (32 - prefix)` calculates the number of addresses in a subnet.

### Binary and Hexadecimal Conversions

Network engineers work with binary (for subnet masks) and hexadecimal (for MAC addresses, IPv6) regularly. Python makes these conversions straightforward.

```python
In [1]: bin(255) # Decimal to binary
Out[1]: '0b11111111'

In [2]: hex(255) # Decimal to hex
Out[2]: '0xff'

In [3]: int('ff', 16) # Hex to decimal
Out[3]: 255

In [4]: int('11111111', 2) # Binary to decimal
Out[4]: 255

In [5]: bin(int('C0', 16)) # Hex C0 → decimal → binary
Out[5]: '0b11000000'
```

> **Note:** The `int()` function allows converting to int type. The second argument can specify the number system.

These conversions are essential for understanding subnet masks. For example, a /24 mask is `255.255.255.0`, and in binary each `255` is `11111111` — eight 1-bits:

```python
In [6]: f"{255:08b}.{255:08b}.{255:08b}.{0:08b}"
Out[6]: '11111111.11111111.11111111.00000000'
```

The format specifier `{:08b}` means: format as binary (`b`), pad with zeros to 8 digits (`08`).

### Type Conversion

```python
In [1]: vlan_str = "100" # This is a string
In [2]: vlan_int = int(vlan_str) # Convert to integer
In [3]: type(vlan_int)
Out[3]: int

In [4]: port = 22
In [5]: port_str = str(port) # Convert to string
In [6]: type(port_str)
Out[6]: str

In [7]: int(3.9) # Float to int (truncates, does NOT round)
Out[7]: 3
```

> **Warning:** `int()` truncates (removes the decimal part), it does not round. `int(3.9)` returns `3`, not `4`. Use `round()` if you need rounding behavior.

### Comparison Operators

Comparison operators return boolean values (`True` or `False`) and are used in conditional statements (Chapter 7).

```python
In [1]: packets_sent = 1000
In [2]: packets_received = 985

In [3]: packets_sent > packets_received
Out[3]: True

In [4]: packets_sent == packets_received
Out[4]: False

In [5]: packets_sent != packets_received
Out[5]: True

In [6]: packets_sent >= 1000
Out[6]: True
```

> **Note:** Equality is checked by double `==`. A single `=` is for assignment — confusing the two is a common beginner mistake.

### Section Summary

Numbers in Python are either `int` (whole numbers) or `float` (decimals). Division always returns float. Python natively supports binary and hexadecimal conversions, which are essential for subnet calculations, MAC address handling, and IPv6 work. Variables are created by assignment and follow snake_case naming conventions.

---

### Tasks

**Task 2.1**

Create variables for a network device: `hostname`, `ip_address`, `model`, `ios_version`, `uptime_days`. Print all of them using f-strings with the debug format (`f"{variable=}"`).

**Task 2.2**

Calculate the total number of usable IP addresses in a /24, /16, and /8 subnet using the formula `2^(32 - prefix) - 2`. Print each result with a descriptive label.

**Task 2.3**

Convert the decimal number 192 to binary and hexadecimal. Then convert the hex string "C0A80001" to decimal. What IPv4 address does that decimal number represent? (Hint: C0=192, A8=168, 00=0, 01=1)

**Task 2.4**

You sent 1000 packets and received 987. Calculate the packet loss percentage, rounded to 2 decimal places. Store each step in a separate variable.

**Task 2.5**

A 10 Gbps link runs at 73% utilization. Calculate the used bandwidth in Mbps. Then calculate how many megabytes of data can be transferred in 60 seconds at that rate (1 byte = 8 bits).


---

# 3. Strings and Text Processing

This chapter covers:

- Creating strings with single quotes, double quotes, and triple quotes
- Essential string methods for network engineers: split, join, strip, replace
- String formatting with f-strings
- String indexing and slicing
- Escape characters and raw strings

Strings are the most frequently used data type in network automation. Every IP address, hostname, interface name, command, and piece of CLI output is a string. Mastering string manipulation is the single most important skill for parsing network device output.


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
print(len(hostname)) # 11

# Concatenation
domain = "example.com"
fqdn = hostname + "." + domain
print(fqdn) # core-rtr-01.example.com

# Repetition
divider = "-" * 40
print(divider) # ----------------------------------------

# Membership test
print("rtr" in hostname) # True
print("sw" in hostname) # False
```

## 3.3 String Methods (Essential for Network Engineers)

### Combined Approach

```python
# .split() — Break strings apart (CRITICAL for parsing CLI output)
ip_address = "198.51.100.0/24"
network, mask = ip_address.split("/")
print(f"Network: {network}") # Network: 198.51.100.0
print(f"Mask: {mask}") # Mask: 24

octets = network.split(".")
print(octets) # ['198', '51', '100', '0']

# .join() — Combine list into string
commands = ['interface Gi0/1', 'switchport mode access', 'switchport access vlan 10']
config_block = "\n".join(commands)
print(config_block)
```

### Security Automation Approach — IPv4 and IPv6 Parsing

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
line = " Interface GigabitEthernet0/1 is up, line protocol is up "

# .strip() — Remove whitespace (critical for file/CLI output parsing)
print(line.strip())

# .upper() / .lower()
print("vlan100".upper()) # VLAN100
print("OSPF".lower()) # ospf

# .startswith() / .endswith()
if line.strip().startswith("Interface"):
 print("This is an interface line")

# .replace()
new_line = line.replace("up", "down")
print(new_line)

# .count()
config = "permit ip any any\npermit tcp any any\ndeny ip any any"
print(config.count("permit")) # 2

# .find() — returns index, or -1 if not found
print(line.find("up")) # first index where "up" occurs

# .isdigit()
vlan = "100"
print(vlan.isdigit()) # True
print("vlan100".isdigit()) # False
```

## 3.5 String Formatting (f-strings)

> **Note:** F-strings are the most convenient way of string formatting in Python 3.6+ and are the recommended approach throughout this book.

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
print(f"{hostname=}") # hostname='sw-access-01'
print(f"{vlan=}") # vlan=100
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


---

# 4. Lists

This chapter covers:

- Creating and modifying lists
- Indexing, slicing, and iterating over lists
- Essential list methods: append, pop, sort, extend
- Lists of device dictionaries as the standard multi-device pattern

Lists are ordered, mutable collections. In network automation, lists hold device inventories, command sequences, interface names, and parsed output lines.


Lists are ordered, mutable collections. In network automation, lists hold device inventories, command sets, interface names, and parsed output lines.

## 4.1 Creating Lists

```python
# Empty list
my_devices = []

# List with values
vlans = [10, 20, 30, 40, 50]
hostnames = ["rtr1", "rtr2", "sw1", "sw2", "fw1"]
mixed = ["rtr1", 48, True, 3.14] # mixed types allowed but not recommended

# List from string
show_output = "Gi0/1 10.0.0.1 up\nGi0/2 10.0.0.2 down"
lines = show_output.splitlines()
print(lines) # ['Gi0/1 10.0.0.1 up', 'Gi0/2 10.0.0.2 down']
```

## 4.2 Indexing and Slicing

```python
devices = ["rtr1", "rtr2", "sw1", "sw2", "fw1"]

# Indexing (0-based)
print(devices[0]) # rtr1 (first)
print(devices[-1]) # fw1 (last)
print(devices[2]) # sw1

# Slicing [start:stop:step]
print(devices[0:2]) # ['rtr1', 'rtr2'] (stop is exclusive)
print(devices[:3]) # ['rtr1', 'rtr2', 'sw1']
print(devices[2:]) # ['sw1', 'sw2', 'fw1']
print(devices[::-1]) # ['fw1', 'sw2', 'sw1', 'rtr2', 'rtr1'] (reversed)
```

## 4.3 List Methods

### Approach: Firewall Device Lists

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
city1 = locations.pop(0) # remove first
city_n = locations.pop() # remove last (default)
print(f"{city1=}")
print(f"{city_n=}")
print(f"{locations=}")
```

### Approach: More List Methods

```python
vlans = [10, 30, 20, 50, 40]

# .sort() — sort in-place
vlans.sort()
print(vlans) # [10, 20, 30, 40, 50]

# sorted() — returns new sorted list (original unchanged)
original = [50, 20, 40, 10]
new_sorted = sorted(original)
print(original) # [50, 20, 40, 10] (unchanged)
print(new_sorted) # [10, 20, 30, 40, 50]

# .insert(index, value)
vlans.insert(0, 1)
print(vlans) # [1, 10, 20, 30, 40, 50]

# .remove(value) — removes first occurrence
vlans.remove(30)
print(vlans) # [1, 10, 20, 40, 50]

# .extend() — add all elements from another list
vlans.extend([60, 70])
print(vlans) # [1, 10, 20, 40, 50, 60, 70]

# .index(value) — find position
print(vlans.index(40)) # 3

# Check membership
print(20 in vlans) # True
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


---

# 5. Dictionaries

This chapter covers:

- Creating dictionaries with key-value pairs
- Accessing values by key, including nested dictionaries
- Essential dictionary methods: get, keys, values, items, update, pop
- The Netmiko device dictionary pattern
- Dictionary unpacking with **

Dictionaries are the natural way to represent network device data. A router has a hostname (key) and an IP (value). An interface has a name (key) and a status (value). Netmiko requires device parameters as a dictionary.


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

### Approach: Firewall Service Object

```python
#!/usr/bin/env python
from rich import print

ftp_service = {
 "uid": "97aeb3d0-9aea-11d5-bd16-0090272ccb30",
 "name": "ftp",
 "type": "service-tcp",
 "domain": {
 "uid": "a0bbbc99-adef-4ef8-bb6d-defdefdefdef",
 "name": "Firewall Data",
 "domain-type": "data domain",
 },
 "port": "21",
 "icon": "Protocols/FTP",
 "color": "forest green",
}

# Access values
print(ftp_service["name"]) # ftp
print(ftp_service["port"]) # 21

# Nested dictionary access
print(ftp_service["domain"]["name"]) # Firewall Data
```

## 5.2 Dictionary Operations

### Approach: Network Object Manipulation

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
print(list(device.keys())) # ['hostname', 'ip', 'vendor']
print(list(device.values())) # ['sw1', '10.0.0.1', 'Cisco']

for key, value in device.items():
 print(f"{key}: {value}")

# .get() — safe access (returns None if key missing, no error)
model = device.get("model")
print(model) # None
model = device.get("model", "Unknown")
print(model) # Unknown

# .update() — merge dictionaries
extra_info = {"model": "C9300", "ports": 48}
device.update(extra_info)
print(device)

# .setdefault() — set value only if key does NOT exist
device.setdefault("vendor", "Arista") # no change, "Cisco" already exists
device.setdefault("site", "HQ") # adds "site": "HQ"

# Check membership (checks KEYS by default)
print("hostname" in device) # True
print("sw1" in device) # False (that's a value, not a key)
```

## 5.4 Netmiko Device Dictionaries

> **Note:** In Netmiko, device parameters are always passed as dictionaries.

```python
from netmiko import ConnectHandler

# Standard Netmiko device dictionary
cisco_device = {
 "device_type": "cisco_ios",
 "host": "cisco3.lab.io",
 "username": "pyclass",
 "password": "secret123",
}

# Dictionary unpacking with **
net_connect = ConnectHandler(**cisco_device)
# This is equivalent to:
# ConnectHandler(device_type="cisco_ios", host="cisco3.lab.io", ...)
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


---

# 6. Tuples, Sets, and Booleans

## 6.1 Tuples

Tuples are immutable lists. They are used when data should not change (e.g., a fixed set of SNMP community strings, or coordinates).

```python
# Create tuples
dns_servers = ("8.8.8.8", "8.8.4.4")
credentials = ("admin", "secret123")

# Indexing (same as lists)
print(dns_servers[0]) # 8.8.8.8

# Unpacking
primary, secondary = dns_servers
print(primary) # 8.8.8.8

# Tuples are IMMUTABLE
# dns_servers[0] = "1.1.1.1" # TypeError!

# Single element tuple requires trailing comma
single = ("only_one",)
not_a_tuple = ("only_one") # This is just a string!
```

## 6.2 Sets

Sets are unordered collections of unique elements. They are excellent for comparing configurations, finding differences in VLAN lists, etc.

```python
# Create sets
vlans_sw1 = {10, 20, 30, 40, 50}
vlans_sw2 = {30, 40, 50, 60, 70}

# Union — all VLANs across both switches
all_vlans = vlans_sw1 | vlans_sw2
print(all_vlans) # {10, 20, 30, 40, 50, 60, 70}

# Intersection — VLANs on BOTH switches
common = vlans_sw1 & vlans_sw2
print(common) # {30, 40, 50}

# Difference — VLANs on sw1 but NOT sw2
only_sw1 = vlans_sw1 - vlans_sw2
print(only_sw1) # {10, 20}

# Symmetric difference — VLANs on one OR the other but NOT both
unique = vlans_sw1 ^ vlans_sw2
print(unique) # {10, 20, 60, 70}

# Practical: Find blocked IPs to add/remove
current_blocked = {"1.2.3.4", "5.6.7.8", "9.10.11.12"}
new_blocked = {"5.6.7.8", "9.10.11.12", "13.14.15.16"}

add_ips = new_blocked - current_blocked
remove_ips = current_blocked - new_blocked
print(f"Add: {add_ips}") # Add: {'13.14.15.16'}
print(f"Remove: {remove_ips}") # Remove: {'1.2.3.4'}
```

### Approach: Set Comparison for Blocked IPs

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

### Approach: Truthiness in Python

```python
#!/usr/bin/env python
from rich import print

# Strings: empty string is False
some_str = ""
print(bool(some_str)) # False
print(bool("hello")) # True

# Numbers: 0 is False
some_int = 0
print(bool(some_int)) # False
print(bool(42)) # True

# Lists: empty list is False
some_list = []
print(bool(some_list)) # False
print(bool([1, 2])) # True

# Dict: empty dict is False
some_dict = {}
print(bool(some_dict)) # False
```

### Short-Circuit Evaluation

```python
# and: if first condition is False, skip second
check_cond = False
if check_cond and some_function(): # some_function() never called
 print("Never printed")

# or: if first condition is True, skip second
skip_func = True
if skip_func or some_function(): # some_function() never called
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


---

# 7. Conditionals (if/elif/else)

## 7.1 Basic if/elif/else

> **Note:** The `if/elif/else` statement allows branching during program execution, directing the flow based on conditions.

### Approach: Simple Decisions

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

### Approach: Firewall Pod Selection

```python
#!/usr/bin/env python
from rich import print

pod_numb = input("Enter pod number: ")
fw_name = f"fw-lab{pod_numb}"

if fw_name == "fw-lab1":
 print("Found pod1")
elif fw_name == "fw-lab99":
 print("Found pod99")
else:
 print("Not my pod")
```

## 7.2 Compound Conditions (and, or, not)

### Approach: API Version Checking

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

### Network-Focused Approach

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

### Approach: Service Matching with JSON

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

# password handling
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


---

# 8. Loops (for and while)

## 8.1 for Loops

### Approach: Iterating Over Firewalls

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

### Approach: Generating Config

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

### Security Automation Approach

```python
from rich import print

my_firewalls = [
 "pod1-gaia", "pod2-gaia", "pod3-gaia",
 "pod4-gaia", "pod5-gaia", "pod98-gaia", "pod99-gaia",
]

for fw in my_firewalls:
 if fw == "pod4-gaia":
 continue # Skip pod4, go to next iteration
 if fw == "pod98-gaia":
 break # Stop the entire loop
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

### Approach: Wait with Timeout

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

### Approach: User Input Loop

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


---

# 9. Functions

## 9.1 Defining Functions

### Approach: Building Blocks

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

### Approach: Network Functions

```python
#!/usr/bin/env python
from rich import print

def fw_func(name, ipaddr, os_version="R82"):
 print(f"{name=}")
 print(f"{ipaddr=}")
 print(f"{os_version=}")
 return f"{name}-{ipaddr}-{os_version}"

# Positional arguments
ret_val = fw_func("fw-lab99", "3.77.44.109", "R81.20")
print(f"\n{ret_val=}\n")

# Named (keyword) arguments
ret_val = fw_func(
 os_version="R82",
 ipaddr="3.77.44.100",
 name="fw-lab1",
)
print(f"\n{ret_val=}\n")

# Using default value
ret_val = fw_func(name="fw-lab1", ipaddr="3.77.44.100")
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
print(result) # operational

# Functions without return statement return None
def greet(name):
 print(f"Hello {name}")

result = greet("Engineer") # prints "Hello Engineer"
print(result) # None
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

### Approach: API Helper Functions

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
 if "X-session-id" in headers:
 headers.pop("X-session-id")
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
 print(f" {key}: {value}")

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
 print(f" IP: {device['ip']}")
 print(f" Vendor: {device['vendor']}")
```

---


---

# 10. Working with Files

## 10.1 Reading Files

### Approach: Multiple Methods

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
print(type(lines)) # <class 'list'>
print(lines) # ['line1\n', 'line2\n', ...]
f.close()

# Method 3: iterate line by line
f = open("my_file.txt", "r")
for line in f:
 line = line.strip() # remove trailing newline
 print(repr(line))
f.close()
```

## 10.2 Context Manager (with statement)

> **& KByers:** Always use `with` to automatically close files.

```python
# Context manager automatically closes the file when done
with open("my_file.txt") as f:
 data = f.read()

print(data)
# File is already closed here — no need for f.close()
```

## 10.3 Writing Files

### Security Automation Approach

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

print(type(data)) # <class 'dict'>
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

### Approach: Critical Distinction

```python
import json
from rich import print

filename = "network_objects.json"

# Read as TEXT (string)
with open(filename) as f:
 data = f.read()
print(f"Type: {type(data)}") # <class 'str'>

# Read as DATA STRUCTURE (dict/list)
with open(filename) as f:
 data = json.load(f)
print(f"Type: {type(data)}") # <class 'dict'>
print(f"Type of 'objects': {type(data['objects'])}") # <class 'list'>
```

---

## Chapter 10 Lab Tasks

**Task 10.1:** Create a text file with 5 router hostnames (one per line). Read the file and print each hostname stripped of whitespace.

**Task 10.2:** Write a script that reads a JSON file containing a list of devices, loops through them, and prints each device's hostname and IP. Create the JSON file first.

**Task 10.3:** Create a YAML file with a list of firewall names and their management IPs. Read it back and print the data.

**Task 10.4:** Write a script that reads a config file line by line, counts the number of "interface" lines, and writes only those interface lines to a new file.

**Task 10.5:** Demonstrate the difference between `f.read()` (string), `json.load()` (data structure), and `f.readlines()` (list of strings) on the same JSON file. Print the type of each.

---


---

# 11. Working with CSV, JSON, and YAML

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
print(type(data)) # <class 'dict'>

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


---

# 12. Error Handling (try/except)

## 12.1 Basic try/except

### Approach: Progressive Error Handling

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

### Approach: Security Automation Exceptions

```python
class FwConfigError(Exception):
 """Raised when firewall configuration fails."""
 pass

class FwPolicyInstallError(Exception):
 """Raised when firewall policy installation fails."""
 pass

class FwAuthError(Exception):
 """Raised when session ID is missing or expired."""
 pass

# Using custom exceptions
def api_call(url, headers, payload=None):
 if "X-session-id" not in headers:
 msg = "Session ID not set, please call '.login()' first."
 raise FwAuthError(msg)
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


---

# 13. Modules and Packages

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

print(validate_ip("10.0.0.1")) # True
print(generate_hostname("NYC", "RTR")) # NYC-RTR-01
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


---

# 14. Useful Built-in Functions

## 14.1 range()

```python
# Generate VLAN IDs
for vlan in range(10, 51, 10): # start, stop, step
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
vlan_ints = list(map(int, vlans)) # [10, 20, 30]

# filter() — keep elements that pass test
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
evens = list(filter(lambda x: x % 2 == 0, numbers)) # [2, 4, 6, 8, 10]

# all() / any()
statuses = ["up", "up", "up"]
print(all(s == "up" for s in statuses)) # True

statuses = ["up", "down", "up"]
print(any(s == "down" for s in statuses)) # True
```

---

## Chapter 14 Lab Tasks

**Task 14.1:** Use `range()` to generate a list of IPs from 10.0.0.1 to 10.0.0.10. Print each.

**Task 14.2:** Use `zip()` to combine three lists (hostnames, IPs, VLANs) into a list of dictionaries.

**Task 14.3:** Use `sorted()` with a `lambda` key to sort a list of device dictionaries by IP address.

**Task 14.4:** Use `filter()` to extract only "up" interfaces from a list of interface status dicts.

**Task 14.5:** Use `all()` to verify every device in a list has the key "hostname" set to a non-empty string.

---


---

# 15. Regular Expressions

## 15.1 Basic Regex with re Module

```python
import re

# re.search() — find first match
line = "Interface GigabitEthernet0/0/0 is up, line protocol is up"
match = re.search(r"(\S+) is (up|down)", line)
if match:
 print(match.group(0)) # GigabitEthernet0/0/0 is up
 print(match.group(1)) # GigabitEthernet0/0/0
 print(match.group(2)) # up

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
print(re.findall(ip_pattern, text)) # ['10.0.0.1']
print(re.findall(mac_pattern, text)) # ['aabb.ccdd.eeff']
print(re.findall(intf_pattern, text)) # ['Gi0/1']
print(re.findall(vlan_pattern, text)) # ['100']
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


---

# 16. List Comprehensions and Generators

## 16.1 List Comprehensions

```python
# Traditional loop
vlans = []
for i in range(10, 60, 10):
 vlans.append(i)

# List comprehension (same result, one line)
vlans = [i for i in range(10, 60, 10)]
print(vlans) # [10, 20, 30, 40, 50]

# With condition
up_interfaces = [intf for intf in interfaces if intf["status"] == "up"]

# Transform + filter
hostnames = ["RTR1", "SW1", "FW1"]
lower_names = [name.lower() for name in hostnames]

# Network examples
ips = [f"10.0.0.{i}" for i in range(1, 11)]
print(ips) # ['10.0.0.1', '10.0.0.2', ..., '10.0.0.10']

# strip whitespace from file lines
with open("blocked_ips.txt") as f:
 blocked_ips = [ip.strip() for ip in f.readlines()]

# generate host objects
blocked_ip_objs = [gen_host_object(ip) for ip in add_blocked_ips]
```

## 16.2 Dictionary Comprehensions

```python
# Create dict from two lists
hostnames = ["rtr1", "rtr2", "rtr3"]
ips = ["10.0.0.1", "10.0.0.2", "10.0.0.3"]

device_map = {host: ip for host, ip in zip(hostnames, ips)}
print(device_map) # {'rtr1': '10.0.0.1', 'rtr2': '10.0.0.2', 'rtr3': '10.0.0.3'}
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


---

# 17. Object-Oriented Programming — Basics

## 17.1 Why OOP for Network Automation?

Classes let you model network objects: a Router, a Firewall, an API Client. Each has attributes (hostname, IP) and methods (connect, send_command, logout).

## 17.2 Creating a Class

### Approach: Firewall API Class

```python
class FirewallAPI:
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
api_client = FirewallAPI(
 host="fw-lab99.lab.io",
 username="admin",
 password="testpass",
 mode="gaia_api"
)
print(api_client.base_url)
# https://fw-lab99.lab.io/gaia_api/v1.8/
```

## 17.3 Methods

```python
import requests
import json

class FirewallAPI:
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
 self.headers["X-session-id"] = resp_struct["sid"]

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
 self.headers.pop("X-session-id", None)
```

### Approach: Simple Device Class

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
 print(f" {intf['name']}: {intf.get('ip', 'no ip')}")

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


---

# 18. OOP — Special Methods and Inheritance

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
print(ip1) # 10.0.0.1
print(repr(ip1)) # IPAddress('10.0.0.1')
print(ip1 == ip2) # False
print(ip1 < ip2) # True
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
rtr.connect() # inherited from NetworkDevice
print(rtr.show_version()) # CiscoRouter method
```

---

## Chapter 18 Lab Tasks

**Task 18.1:** Add `__str__` and `__repr__` methods to your Router class from Chapter 17. Print an instance with both `print()` and `repr()`.

**Task 18.2:** Create a base class `NetworkDevice` and two subclasses `Router` and `Switch`. Each subclass should add vendor-specific methods.

**Task 18.3:** Create an `IPAddress` class with `__eq__` and `__lt__` so IP addresses can be compared and sorted. Sort a list of 5 IP objects.

**Task 18.4:** Demonstrate `super().__init__()` by creating a `CiscoFirewall` class that inherits from `NetworkDevice` and adds firewall-specific attributes.

**Task 18.5:** Create a context manager class `DeviceConnection` with `__enter__` and `__exit__` methods that simulate connecting and disconnecting from a device.

---


---

# 19. OS Interaction — subprocess, pathlib, os

## 19.1 subprocess

### Security Automation Approach

```python
#!/usr/bin/env python
import subprocess

# subprocess.run() — recommended approach
command = ["ping", "-c", "4", "google.com"]
result = subprocess.run(command, capture_output=True, text=True)

print(result.stdout)
print(result.stderr)
print(result.returncode) # 0 = success
```

## 19.2 pathlib

### Approach: Modern File Path Handling

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


---

# 20. Connecting to Network Devices (Netmiko)

## 20.1 First Connection

### Netmiko Approach

```python
import os
from getpass import getpass
from netmiko import ConnectHandler

password = os.getenv("NETMIKO_PASSWORD") if os.getenv("NETMIKO_PASSWORD") else getpass()

# Simple connection
net_connect = ConnectHandler(
 device_type="cisco_ios",
 host="cisco3.lab.io",
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
 "host": "cisco3.lab.io",
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
 "host": "cisco3.lab.io",
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
 "host": "cisco3.lab.io",
 "username": "pyclass",
 "password": password,
 "session_log": "cisco3.out", # Logs everything to file
}

with ConnectHandler(**my_device) as net_connect:
 output = net_connect.send_command("show ip int brief")
 print(output)
```

## 20.5 Firewall SSH Connections

### Security Automation Approach

```python
from netmiko import ConnectHandler

cisco_fw = {
 "host": "fw-lab99.lab.io",
 "device_type": "cisco_ftd",
 "username": "admin",
 "use_keys": True,
 "key_file": "/home/user/.ssh/eu-sshkey.pem",
 "session_log": "output.log",
}

with ConnectHandler(**cisco_fw) as nc:
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


---

# 21. Sending Commands with Netmiko

## 21.1 send_command()

```python
from netmiko import ConnectHandler

with ConnectHandler(**device) as net_connect:
 # send_command() waits for the prompt before returning
 output = net_connect.send_command("show ip interface brief")
 print(output)

 # With TextFSM parsing
 output = net_connect.send_command("show ip int brief", use_textfsm=True)
 print(output) # Returns list of dicts!
```

## 21.2 send_command_timing()

```python
# send_command_timing() uses time-based approach (no prompt detection)
output = net_connect.send_command_timing("show ip route")
print(output)
```

## 21.3 write_channel() and read_channel()

### Netmiko Approach — Low-Level Control

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


---

# 22. Device Configuration with Netmiko

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
# ip address 10.99.99.1 255.255.255.255

with ConnectHandler(**device) as net_connect:
 output = net_connect.send_config_from_file("changes.cfg")
 print(output)
```

## 22.3 Enable Mode and Config Mode

### Netmiko Approach

```python
with ConnectHandler(**device) as net_connect:
 # Enable mode
 net_connect.enable()
 print(net_connect.find_prompt()) # rtr1#

 # Enter config mode manually
 net_connect.config_mode()
 print(net_connect.find_prompt()) # rtr1(config)#

 # Exit config mode
 net_connect.exit_config_mode()
```

## 22.4 Save Configuration

```python
with ConnectHandler(**device) as net_connect:
 net_connect.send_config_set(["interface Lo99", "ip address 10.99.99.1 255.255.255.255"])
 net_connect.save_config() # write memory / copy run start
```

## 22.5 Juniper Commit Operations

### Netmiko Approach

```python
vmx = {
 "device_type": "juniper_junos",
 "host": "vmx1.lab.io",
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


---

# 23. REST APIs with Python (requests)

## 23.1 GET Requests

```python
import requests

# Simple GET
response = requests.get("https://api.ipify.org?format=json")
print(response.status_code) # 200
print(response.json()) # {'ip': '203.0.113.5'}
```

## 23.2 POST Requests with Authentication

### Approach: Firewall API Authentication

```python
import requests
import json
import os
from dotenv import load_dotenv

load_dotenv()
host = "fw-lab99.lab.io"
base_url = f"https://{host}/gaia_api/v1.8/"
user = "admin"
password = os.environ["CISCO_FW_ADMIN"]

# Login (POST)
url = f"{base_url}login"
headers = {"Content-Type": "application/json"}
login_payload = {"user": user, "password": password}

response = requests.post(
 url, data=json.dumps(login_payload),
 headers=headers, verify=False
)

session_id = response.json()["sid"]
headers["X-session-id"] = session_id

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
# CISCO_FW_ADMIN=mysecretpassword
# CISCO_FW_EXPERT=myexpertpassword

load_dotenv()
admin_pass = os.environ["CISCO_FW_ADMIN"]
expert_pass = os.environ["CISCO_FW_EXPERT"]
```

---

## Chapter 23 Lab Tasks

**Task 23.1:** Use `requests.get()` to fetch data from a public API (e.g., https://api.ipify.org?format=json). Print the response status code and JSON body.

**Task 23.2:** Write a function `api_login(base_url, username, password)` that performs a POST login and returns the session headers. Include error handling.

**Task 23.3:** Write a function `api_call(base_url, endpoint, headers, payload)` that makes a POST API call and returns the response. Test it.

**Task 23.4:** Create a `.env` file with credentials and use `python-dotenv` to load them. Verify they are accessible via `os.environ`.

**Task 23.5:** Write a complete script that logs in to an API, makes 2 API calls, and logs out. Structure it with functions and `if __name__ == "__main__"`.

---


---

# 24. Concurrent Connections — Threads and Processes

## 24.1 Why Concurrency?

Connecting to 100 devices sequentially takes minutes. Concurrency lets you connect to many devices simultaneously.

## 24.2 ThreadPoolExecutor

### Security Automation Approach

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


---

# 25. Jinja2 Configuration Templates

## 25.1 Basic Templates

```python
from jinja2 import Environment, FileSystemLoader

env = Environment(loader=FileSystemLoader("templates"))
template = env.get_template("interface.j2")

# Template file: templates/interface.j2
# interface {{ interface_name }}
# ip address {{ ip_address }} {{ subnet_mask }}
# no shutdown

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


---

# 26. Parsing Output with TextFSM

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


---

# 27. Testing with pytest

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


---

# 28. Working with Databases (SQLite)

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


---

# 29. Building a Complete Network Automation Project

## 29.1 Project Structure

### Approach: Real-World Cisco firewall Automation

```
firewall_automation/
├── .env # Credentials (never commit to git!)
├── .gitignore # Excludes .env, *.pyc, __pycache__
├── requirements.txt # pip dependencies
├── main.py # Entry point
├── config/
│ ├── devices.yaml # Device inventory
│ └── blocked_ips.txt # IP blocklist
├── lib/
│ ├── __init__.py
│ ├── fw_api.py # API client class
│ ├── object_funcs.py # Host/network object functions
│ ├── policy_funcs.py # Firewall rule functions
│ └── exceptions.py # Custom exceptions
├── templates/
│ └── switch_config.j2 # Jinja2 templates
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
from lib.fw_api import FirewallAPI
from lib.object_funcs import cfg_host_objects
from lib.policy_funcs import cfg_fw_rules, install_fw_policy
from lib.exceptions import FwConfigError

def main():
 load_dotenv()
 host = "fw-lab99.lab.io"
 username = "admin"
 password = os.environ["CISCO_FW_ADMIN"]

 api_client = FirewallAPI(host=host, username=username, password=password)

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
 except FwConfigError as e:
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
>>> 255 * 255 # 65025 (int)
>>> 10 / 3 # 3.3333... (float - division always returns float)
>>> 2 ** 32 # 4294967296 (int)
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
print(bin(192)) # 0b11000000
print(hex(192)) # 0xc0
decimal = int("C0A80001", 16)
print(decimal) # 3232235521
# That's 192.168.0.1 (C0=192, A8=168, 00=0, 01=1)
```

**2.4:**
```python
sent = 1000
received = 987
lost = sent - received
loss_pct = round((lost / sent) * 100, 2)
print(f"Packet loss: {loss_pct}%") # 1.3%
```

**2.5:**
```python
bandwidth_gbps = 10.0
utilization = 0.73
used_gbps = bandwidth_gbps * utilization # 7.3 Gbps
used_mbps = used_gbps * 1000 # 7300 Mbps
bits_per_sec = used_gbps * 1_000_000_000 # 7,300,000,000 bps
bytes_in_60s = (bits_per_sec * 60) / 8
megabytes = bytes_in_60s / 1_000_000
print(f"Used: {used_mbps} Mbps")
print(f"Data in 60s: {megabytes:,.0f} MB") # ~54,750 MB
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
print(result) # 2001:db8:0:42:0:0:0:1
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
print(intf.startswith("Gig")) # True
print("0/0" in intf) # True
print(intf.endswith("/0")) # True
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
vlans.append(70); print(vlans)
vlans.insert(0, 5); print(vlans)
vlans.remove(30); print(vlans)
vlans.sort(); print(vlans)
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
print(f"Destination: {dest_ip}") # 192.168.1.0
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
# dns[0] = "9.9.9.9" # TypeError: 'tuple' object does not support item assignment
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
print(unique_set) # {10, 20, 30, 40}
sorted_list = sorted(unique_set)
print(sorted_list) # [10, 20, 30, 40]
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
print(f"Add: {to_add}") # {'permit_dns'}
print(f"Remove: {to_remove}") # {'deny_telnet'}
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

print(generate_hostname("NYC", "RTR")) # NYC-RTR-01
print(generate_hostname("LAX", "SW", "05")) # LAX-SW-05
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


---

# 30. Capstone Project — Progressive Network Automation Scripts

This capstone project walks you through 10 progressive real-world network automation scripts from a progressive network automation lab. Each script builds on the previous one, taking you from a simple `show` command all the way to a full inventory report with CSV export. This is exactly the kind of progression you would follow in production.

**Lab Structure:** 10 scripts that build on each other progressively

**Lab Topology:**
- **csr1** — Cisco IOS-XE router at `198.18.1.11`
- **csr2** — Cisco IOS-XE router at `198.18.1.12`
- Credentials: `cisco / cisco`

---

## 30.1 Supporting Files

Before diving into the scripts, create these supporting files that the scripts depend on.

### device_list (IP inventory file)

```
198.18.1.11
198.18.1.12
```

### show_command (Show commands to verify config)

```
show runn | in logging
show runn | in ntp
show runn | in snmp
show ip access-lists TEST_ACL
show ip ospf neighbor
show ip ospf interface brief
show ip interface brief
```

### config_commands (Configuration to push)

```
logging console
logging host 10.1.1.3
ntp server 10.1.1.4
ip name-server 10.1.1.5
no ip http server
no ip http secure-server
snmp-server community cisco_public RO
snmp-server community cisco_private RW
snmp-server location dCloud
ip access-list extended TEST_ACL
permit ip 1.1.1.0 0.0.0.255 any
permit ip 2.2.2.0 0.0.0.255 any
permit ip 3.3.3.0 0.0.0.255 any
interface loopback 10
description "Created by Python"
router ospf 10
network 0.0.0.0 0.0.0.0 area 0
```

### reset_config (Undo all changes — lab cleanup)

```
no logging console
no logging host 10.1.1.1
no logging host 10.1.1.2
no logging host 10.1.1.3
no ntp server 10.1.1.4
no ip name-server 10.1.1.5
no snmp-server community cisco_public RO
no snmp-server community cisco_private RW
no snmp-server location dCloud
no ip access-list extended TEST_ACL
no interface loopback 10
no router ospf 10
```

---

## 30.2 Scripts 1–4: Foundation Building (Quick Review)

Scripts 1 through 4 build your foundation. Refer to the detailed walkthrough in the main guide for these.

| Script | One-line summary |
|---|---|
| **1** | SSH to one device, run `show version` |
| **2** | Push one config command to one device |
| **3** | Loop over two devices with a list of dicts |
| **4** | Read IPs from file, read commands from file, prompt for credentials |

---

## 30.5 Script 5 — Production Error Handling (Deep Dive)

This script is where you stop writing "lab code" and start writing "production code." Every concept from the first 12 chapters of this guide converges here.

### The Full Script

```python
#!/usr/bin/env python
from getpass import getpass
from netmiko import ConnectHandler
from netmiko import NetmikoAuthenticationException
from netmiko import NetmikoTimeoutException
from paramiko.ssh_exception import SSHException

# Collect login credentials
username = input('Enter your SSH username: ')
password = getpass('Enter your password: ')

# Sending device ip's stored in a file
with open('device_list') as f:
 device_list = f.read().splitlines()

# Iterate through device list and configure the devices
for devices in device_list:
 print('Connecting to device ' + devices)
 ip_address_of_device = devices
 ios_device = {
 'device_type': 'cisco_ios',
 'ip': ip_address_of_device,
 'username': username,
 'password': password
 }
 # Error handling parameters
 try:
 net_connect = ConnectHandler(**ios_device)
 except NetmikoAuthenticationException:
 print('Authentication failure: ' + ip_address_of_device)
 continue
 except NetmikoTimeoutException:
 print('Timeout to device: ' + ip_address_of_device)
 continue
 except EOFError:
 print("End of file while attempting device " + ip_address_of_device)
 continue
 except SSHException:
 print('SSH Issue. Are you sure SSH is enabled? ' + ip_address_of_device)
 continue
 except Exception as unknown_error:
 print('Some other error: ' + str(unknown_error))
 continue

 # Configure the device and save config
 output = net_connect.send_config_from_file('config_commands')
 output += net_connect.save_config()
 net_connect.disconnect()
 print(output)
```

### Line-by-Line Concept Mapping to Book References

**Lines 1–5: Imports**

> **Note (Chapter 13):** "Module import. Python has several ways to import a module: `import module`, `from module import something`."

> **Note:** Demonstrates `sys.path` and how Python finds modules to import.

```python
from getpass import getpass # Standard library — Chapter 13
from netmiko import ConnectHandler # Third-party — Chapter 20
from netmiko import NetmikoAuthenticationException # Exception classes — Chapter 12
from netmiko import NetmikoTimeoutException
from paramiko.ssh_exception import SSHException # From netmiko's dependency
```

This script imports from three sources: the standard library (`getpass`), netmiko, and paramiko. The `from X import Y` syntax brings specific names into scope so you don't need to type `netmiko.ConnectHandler` every time.

**Lines 7–8: Credential Collection**

> **Note:** "Asking Questions" — `input()` and `raw_input()` for getting user data interactively.

> **Note (Chapter 7):** User input with `input()` for building interactive scripts.

```python
username = input('Enter your SSH username: ') # Returns string — Chapter 2 (variables)
password = getpass('Enter your password: ') # Like input() but hides typing
```

`getpass()` is the network engineer's best friend — it prevents the password from being visible on-screen or in shell history.

**Lines 10–12: File Reading**

> **Note (Chapter 10):** "When working with network equipment, files can be configurations, templates, or connection options."

> **Note:** `with open("my_file.txt") as f: data = f.read()`

```python
with open('device_list') as f: # Context manager — Chapter 10
 device_list = f.read().splitlines() # String method — Chapter 3
```

The `.splitlines()` method (Chapter 3 string methods) splits on newlines AND strips them — cleaner than `.readlines()` which keeps trailing `\n` characters.

**Lines 14–24: Loop and Device Dictionary**

> **Note (Chapter 7):** "for loop repeats actions for each element."

> **Note (Chapter 3):** "Dictionary is a mutable, unordered data type consisting of key-value pairs."

> **Note:** The standard device dictionary pattern.

```python
for devices in device_list: # For loop — Chapter 8
 ip_address_of_device = devices # Variable assignment — Chapter 2
 ios_device = { # Dictionary — Chapter 5
 'device_type': 'cisco_ios',
 'ip': ip_address_of_device,
 'username': username,
 'password': password
 }
```

The device dictionary is constructed inside the loop, using the loop variable for the IP and the outer-scope variables for credentials. This is the pattern from Netmiko Course class1.

**Lines 25–42: Exception Handling (The Core of Script 5)**

> **Note (Chapter 7):** "try/except is used to handle exceptions... the code in the except block is executed if there is an exception in the try block."

> **Note:** Eight progressive examples of error handling.

> **Note:** "Exceptions are another kind of function... they tell you that something went wrong."

```python
 try:
 net_connect = ConnectHandler(**ios_device) # ** dict unpacking — Chapter 9
 except NetmikoAuthenticationException:
 print('Authentication failure: ' + ip_address_of_device)
 continue # Skip to next device — Chapter 8
 except NetmikoTimeoutException:
 print('Timeout to device: ' + ip_address_of_device)
 continue
 except EOFError:
 print("End of file while attempting device " + ip_address_of_device)
 continue
 except SSHException:
 print('SSH Issue. Are you sure SSH is enabled? ' + ip_address_of_device)
 continue
 except Exception as unknown_error: # Generic catch-all — Chapter 12
 print('Some other error: ' + str(unknown_error))
 continue
```

The exception hierarchy goes from **most specific** to **most generic**:

```
Exception (generic catch-all)
├── SSHException (paramiko-level SSH problem)
├── EOFError (connection dropped mid-stream)
├── NetmikoTimeoutException (device unreachable)
└── NetmikoAuthenticationException (wrong creds)
```

Each `except` block ends with `continue` (Chapter 8 — loops), which skips to the next iteration of the for loop. This means: if device #3 out of 100 fails, the script continues with devices #4–#100 instead of crashing.

**Lines 43–47: Configuration and Save**

> **Note:** Sending configuration commands and saving.

> **Note:** `data = ssh_conn.send_config_set(cmd); data += ssh_conn.save_config()`

```python
 output = net_connect.send_config_from_file('config_commands') # Chapter 22
 output += net_connect.save_config() # += string concat — Chapter 3
 net_connect.disconnect()
 print(output)
```

The `+=` operator (Chapter 3 — string concatenation) appends the save_config output to the existing output string, creating a complete log of everything that happened on the device.

---

## 30.6 Script 6 — Environment Variables for CI/CD

### The Full Script

```python
#!/usr/bin/env python
import os
from getpass import getpass
from netmiko import ConnectHandler
from netmiko import NetmikoAuthenticationException
from netmiko import NetmikoTimeoutException
from paramiko.ssh_exception import SSHException

# Check environment variable for login credentials, if that fails, use getpass().
username = os.getenv("NETMIKO_USERNAME") if os.getenv("NETMIKO_USERNAME") else input('Enter username: ')
password = os.getenv("NETMIKO_PASSWORD") if os.getenv("NETMIKO_PASSWORD") else getpass()

# [...rest identical to Script 5...]
```

### What Changed and Why — Deep Book References

**The only change is lines 9–10.** Everything else is identical to Script 5.

> **Note (Chapter 13):** The `os` module provides interaction with the operating system, including environment variables.

> **Note:** `os.system()`, `subprocess`, and `os.environ` for OS interaction.

> **Note:** `password = os.getenv("NETMIKO_PASSWORD") if os.getenv("NETMIKO_PASSWORD") else getpass()` — this exact pattern.

```python
username = os.getenv("NETMIKO_USERNAME") if os.getenv("NETMIKO_USERNAME") else input('Enter username: ')
password = os.getenv("NETMIKO_PASSWORD") if os.getenv("NETMIKO_PASSWORD") else getpass()
```

This is a **ternary expression** (Chapter 7 — conditionals):
```python
# Ternary form: value_if_true if condition else value_if_false
result = A if condition else B
```

> **Note (Chapter 7):** "Python has a ternary expression... `a if condition else b`"

**Why this matters for CI/CD:**

In Jenkins, GitHub Actions, or GitLab CI, you set environment variables in the pipeline config — the script never prompts for input interactively. In local development, the environment variables aren't set, so it falls back to `getpass()`. One script works in both scenarios.

```bash
# CI/CD pipeline sets these before running:
export NETMIKO_USERNAME=cisco
export NETMIKO_PASSWORD=cisco
python 6-netmiko-final.py # runs without any prompts

# Local developer runs without env vars:
python 6-netmiko-final.py # prompts for credentials
```

---

## 30.7 Script 7 — Verification: Show Commands After Config

### The Full Script

```python
#!/usr/bin/env python
import os
from getpass import getpass
from netmiko import ConnectHandler
from netmiko import NetmikoAuthenticationException
from netmiko import NetmikoTimeoutException
from paramiko.ssh_exception import SSHException

username = os.getenv("NETMIKO_USERNAME") if os.getenv("NETMIKO_USERNAME") else input('Enter username: ')
password = os.getenv("NETMIKO_PASSWORD") if os.getenv("NETMIKO_PASSWORD") else getpass()

# Sending device ip's stored in a file
with open('device_list') as f:
 device_list = f.read().splitlines()

# Sending list of show commands stored in a file
with open('show_command') as f:
 show_commands = f.readlines()

for devices in device_list:
 print('Connecting to device ' + devices)
 ip_address_of_device = devices
 ios_device = {
 'device_type': 'cisco_ios',
 'ip': ip_address_of_device,
 'username': username,
 'password': password
 }
 try:
 net_connect = ConnectHandler(**ios_device)
 except NetmikoAuthenticationException:
 print('Authentication failure: ' + ip_address_of_device)
 continue
 except NetmikoTimeoutException:
 print('Timeout to device: ' + ip_address_of_device)
 continue
 except EOFError:
 print("End of file while attempting device " + ip_address_of_device)
 continue
 except SSHException:
 print('SSH Issue. Are you sure SSH is enabled? ' + ip_address_of_device)
 continue
 except Exception as unknown_error:
 print('Some other error: ' + str(unknown_error))
 continue

 # Iterate through command list and print the output
 net_connect = ConnectHandler(**ios_device)
 for command in show_commands:
 output = net_connect.send_command(command)
 print(command + output + '\n')
 net_connect.disconnect()
```

### New Concepts with Book References

**Dual File Reading — Two with blocks:**

> **Note (Chapter 10):** "In real life, you need to work with multiple files simultaneously."

> **Note:** Reading different file formats in the same script.

```python
with open('device_list') as f:
 device_list = f.read().splitlines() # .splitlines() strips \n — Chapter 3

with open('show_command') as f:
 show_commands = f.readlines() # .readlines() keeps \n — Chapter 10
```

Note the subtle difference: `splitlines()` vs `readlines()`. Here `readlines()` is used and the newlines don't matter because `send_command()` strips them internally.

**Nested Loops — Outer (devices) × Inner (commands):**

> **Note (Chapter 7):** "Nested for loops... the inner loop executes completely for each iteration of the outer loop."

> **Note:** Loops and nested iterations.

```python
 for command in show_commands: # Inner loop — Chapter 8
 output = net_connect.send_command(command) # send_command — Chapter 21
 print(command + output + '\n') # String concat — Chapter 3
```

For 2 devices × 7 commands = 14 total SSH command executions. This is the **configure-then-verify** workflow used in every production change window.

---

## 30.8 Script 8 — Automated Configuration Backup

### The Full Script

```python
#!/usr/bin/env python
import os, time
from datetime import datetime
from getpass import getpass
from netmiko import ConnectHandler

print(datetime.now())
password = os.getenv("NETMIKO_PASSWORD") if os.getenv("NETMIKO_PASSWORD") else getpass()
username = os.getenv("NETMIKO_USERNAME") if os.getenv("NETMIKO_USERNAME") else input('Enter username: ')

# Create backup folder
if not os.path.exists('backup/'):
 os.mkdir('backup')

with open('device_list') as f:
 device_list = f.read().splitlines()

for devices in device_list:
 print('Connecting to device ' + devices)
 ip_address_of_device = devices
 ios_device = {
 'device_type': 'cisco_ios',
 'ip': ip_address_of_device,
 'username': username,
 'password': password
 }

 net_connect = ConnectHandler(**ios_device)

 # Getting hostname and storing it as filename variable
 hostname = net_connect.find_prompt()[:-1]

 print(f'Initiating config backup on {hostname}..')
 output = net_connect.send_command("show run")

 # Saving running config to file
 with open(f'backup/{hostname}.cfg', 'w') as file:
 file.write(output)

 print('Finished config backup \n')
 net_connect.disconnect()
 time.sleep(3)

print(datetime.now())
```

### New Concepts with Deep Book References

**Directory Creation with os:**

> **Note (Chapter 13):** The `os` module for filesystem operations.

> **Note:** `Path("./test1/2026/check_point").mkdir(parents=True, exist_ok=True)` — pathlib equivalent.

```python
if not os.path.exists('backup/'): # Conditional check — Chapter 7
 os.mkdir('backup') # Create directory — Chapter 19
```

The `not` keyword inverts the boolean (Chapter 6 — truthiness). Only creates the folder if it does not already exist — **idempotent** behavior (safe to run multiple times).

**Hostname Extraction via Slicing:**

> **Note (Chapter 3):** "Slicing — getting a subsection of a string using `[start:stop]`."

> **Note:** String indexing and slicing fundamentals.

```python
hostname = net_connect.find_prompt()[:-1]
# ^^^^^^^^^^^^^^^^^^^^^^^^ ^^^^
# returns "csr1#" slice: everything except last char
# Result: "csr1"
```

`[:-1]` is negative slicing (Chapter 3 — strings, Chapter 4 — lists): it means "everything up to but not including the last character." This strips the `#` from the prompt to get a clean hostname for the filename.

**f-string in File Path:**

> **Note (Chapter 3):** "F-strings are the most convenient way of string formatting in Python 3.6+."

```python
with open(f'backup/{hostname}.cfg', 'w') as file: # f-string — Chapter 3
 file.write(output) # File write — Chapter 10
```

The f-string dynamically builds the filepath: if `hostname = "csr1"`, the path becomes `backup/csr1.cfg`.

**Timing with datetime:**

> **Note (Chapter 13):** `datetime` for timestamps.

```python
from datetime import datetime # Module import — Chapter 13
print(datetime.now()) # Start time
# ... script runs ...
print(datetime.now()) # End time
```

Printing `datetime.now()` at start and end gives you execution time — critical for measuring whether your automation is actually faster than manual work.

**Sleep Between Devices:**

```python
time.sleep(3) # Pause 3 seconds between devices
```

> **Note:** `time.sleep(1)` in wait loops.

This prevents flooding the network or hitting SSH rate limits on management interfaces.

---

## 30.9 Script 9 — Structured Parsing with Genie

### The Full Script

```python
#!/usr/bin/env python
from netmiko import ConnectHandler
from pprint import pprint

ios1 = {
 'device_type': 'cisco_ios',
 'ip': '198.18.1.11',
 'username': 'cisco',
 'password': 'cisco',
}

net_connect = ConnectHandler(**ios1)
output = net_connect.send_command('show version', use_genie=True)
net_connect.disconnect()
print(output)

print()
pprint(output)
print()
```

### Structured Data — The Bridge to APIs

**`use_genie=True` transforms raw CLI text into a Python dictionary:**

> **Note (Chapter 3):** "Dictionary is an unordered data type consisting of key-value pairs."

> **Note (Chapter 26):** "On network devices that do not support a software interface, show command output is returned as a string. It has to be processed to get Python objects."

> **Note:** Working with deeply nested dictionaries from JSON/API responses.

Without Genie:
```
Cisco IOS XE Software, Version 17.3.4a
cisco CSR1000V (VXE) processor with 2076020K bytes of physical memory.
... (raw text, hard to parse)
```

With `use_genie=True`:
```python
{
 "version": {
 "hostname": "csr1",
 "chassis": "CSR1000V",
 "chassis_sn": "9ABCDEF1234",
 "os": "iosxe",
 "version": "17.3.4a",
 "uptime": "3 days, 5 hours",
 ...
 }
}
```

Now you can access any field programmatically:
```python
output["version"]["hostname"] # Nested dict access — Chapter 5
output["version"]["chassis_sn"] # Same pattern as KByers JSON exercises
```

**pprint — Pretty Print for Debugging:**

> **Note (Chapter 14):** "`print` has been used many times... but its full syntax has not been discussed."

```python
from pprint import pprint # Standard library — Chapter 13
pprint(output) # Formats nested dicts with indentation
```

The `pprint` module is to debugging what `rich.print` is to production output — it makes complex data structures readable.

---

## 30.10 Script 10 — Full Inventory Report with CSV Export

### The Full Script

```python
#!/usr/bin/env python
import os
import csv
from getpass import getpass
from netmiko import ConnectHandler
from pprint import pprint
from tabulate import tabulate

password = os.getenv("NETMIKO_PASSWORD") if os.getenv("NETMIKO_PASSWORD") else getpass()
username = os.getenv("NETMIKO_USERNAME") if os.getenv("NETMIKO_USERNAME") else input('Enter username: ')

# Creating a list for storing inventory data
inventory = []
title = ["Hostname", "Chassis", "Serial No", "os", "version"]
inventory.append(title)

with open('device_list') as f:
 device_list = f.read().splitlines()

for devices in device_list:
 print('Connecting to device ' + devices)
 ip_address_of_device = devices
 ios_device = {
 'device_type': 'cisco_ios',
 'ip': ip_address_of_device,
 'username': username,
 'password': password
 }

 net_connect = ConnectHandler(**ios_device)
 output = net_connect.send_command('show version', use_genie=True)
 net_connect.disconnect()

 # Extracting output fields that are parsed by genie
 hostname = output["version"]["hostname"]
 chassis = output["version"]["chassis"]
 serial = output["version"]["chassis_sn"]
 os = output["version"]["os"]
 version = output["version"]["version"]

 device_details = [hostname, chassis, serial, os, version]
 inventory.append(device_details)

# Printing the inventory list to table
print(tabulate(inventory, headers="firstrow", tablefmt="grid"))

# Store the inventory data to files
with open("inventory.csv", "w", newline="") as f:
 writer = csv.writer(f)
 writer.writerows(inventory)
```

### Complete Concept Map — Everything Comes Together

**Building a 2D list (list of lists):**

> **Note (Chapter 3):** Lists can contain other lists — creating a table-like data structure.

> **Note:** Navigating complex nested data structures.

```python
inventory = [] # Empty list — Chapter 4
title = ["Hostname", "Chassis", "Serial No", "os", "version"] # Header row
inventory.append(title) # .append() — Chapter 4
# After loop, inventory looks like:
# [
# ["Hostname", "Chassis", "Serial No", "os", "version"], # Row 0 (header)
# ["csr1", "CSR1000V", "9ABC...", "iosxe", "17.3.4a"], # Row 1
# ["csr2", "CSR1000V", "9DEF...", "iosxe", "17.3.4a"], # Row 2
# ]
```

**Nested Dictionary Key Access:**

> **Note:** `domain_uid = network_obj["domain"]["uid"]`

> **Note:** `lock = task["meta-info"]["lock"]` — extracting from deeply nested structures.

```python
hostname = output["version"]["hostname"] # Two-level nested access — Chapter 5
chassis = output["version"]["chassis"]
serial = output["version"]["chassis_sn"]
```

This is the exact same pattern used in the KByers course for navigating Firewall API JSON responses.

**tabulate — Professional Terminal Output:**

```python
from tabulate import tabulate # Third-party module — Chapter 13
print(tabulate(inventory, headers="firstrow", tablefmt="grid"))
```

Output:
```
+------------+-----------+-------------+-------+-----------+
| Hostname | Chassis | Serial No | os | version |
+============+===========+=============+=======+===========+
| csr1 | CSR1000V | 9ABCDEF1234 | iosxe | 17.3.4a |
+------------+-----------+-------------+-------+-----------+
| csr2 | CSR1000V | 9ABCDEF5678 | iosxe | 17.3.4a |
+------------+-----------+-------------+-------+-----------+
```

**CSV Export:**

> **Note (Chapter 11):** "CSV — a text format for presenting tabular data."

```python
import csv # Standard library — Chapter 11
with open("inventory.csv", "w", newline="") as f: # Write mode — Chapter 10
 writer = csv.writer(f) # CSV writer object
 writer.writerows(inventory) # Write ALL rows at once
```

The `newline=""` parameter prevents double-spacing on Windows. `writerows()` takes the entire 2D list and writes it in one call.

---

## 30.11 The Complete Progression Map

| Script | What You Learn | Key Netmiko Method | Chapters Used |
|---|---|---|---|
| **1** | First SSH connection | `send_command()` | Chapter 2, 5, 20 |
| **2** | First config push | `send_config_set()` | Chapter 5, 22 |
| **3** | Multi-device loop | Same | Chapter 4, 5, 8 |
| **4** | External files | `send_config_from_file()` | Chapter 3, 8, 10 |
| **5** | Error handling | Same | Chapter 7, 8, 9, 10, 12, 13, 20 |
| **6** | Environment variables | Same | Chapter 7, 12, 13, 19 |
| **7** | Config verification | `send_command()` loop | Chapter 3, 8, 10, 21 |
| **8** | Config backup | `find_prompt()`, file write | Chapter 3, 7, 10, 13, 19 |
| **9** | Structured parsing | `use_genie=True` | Chapter 5, 11, 13, 26 |
| **10** | Full inventory report | `use_genie=True` + CSV | Chapter 4, 5, 7, 10, 11, 13, 19 |

---

## 30.12 Capstone Lab Tasks

**Task 30.1 — Reproduce the Full Pipeline:**
Clone the repository, set up your environment, and run Scripts 1 through 10 in order against your own lab devices (or use a Cisco DevNet sandbox). Document the output of each script.

**Task 30.2 — Add Timestamps to the Backup Script:**
Modify Script 8 so that backup filenames include a timestamp, e.g., `backup/csr1_2026-03-13_1430.cfg`.

**Task 30.3 — Add Concurrency to the Inventory Report:**
Refactor Script 10 to use `ThreadPoolExecutor` (Chapter 24) so all devices are queried in parallel.

**Task 30.4 — Add Error Handling to Scripts 8–10:**
Scripts 8, 9, and 10 lack error handling. Add the full `try/except` pattern from Script 5 to all three.

**Task 30.5 — Build a Combined Automation Workflow:**
Create a single master script that performs backup → configure → verify → report. Structure with functions and a `main()` entry point.

---


---

# 31. Real-World Python Package Deep Dive — cisco_support

This chapter dissects a **real, published Python package** on PyPI: [`cisco_support`](https://github.com/rothdennis/cisco_support) which wraps the Cisco Support APIs (Bug, EoX, Case, Serial Number, etc.) in clean Python classes. We will break down every design decision and map it back to what you learned in Chapters 1–30.

**Repository:** `https://github.com/rothdennis/cisco_support.git`

---

## 31.1 Project Architecture Overview

```
cisco_support/
├── .github/workflows/
│ └── publish-to-test-pypi.yml ← CI/CD: auto-publish to PyPI
├── .gitignore ← Git ignore rules
├── LICENSE ← Open source license
├── README.md ← Documentation
├── pyproject.toml ← Package metadata + build config
├── requirements.txt ← Build dependencies
└── src/
 └── cisco_support/ ← The actual Python package
 ├── __init__.py ← Package entry point (re-exports)
 ├── auth.py ← OAuth2 token generation
 ├── bug.py ← Bug API class
 ├── case.py ← TAC Case API class
 ├── eox.py ← End-of-Life API class
 ├── product_information.py ← Product Info API class
 ├── serial_number.py ← Serial Number API class
 ├── service_order_return.py ← RMA API class
 ├── software_suggestion.py ← Software Suggestion API class
 └── automated_software_distribution.py ← ASD API class
```

### Mapping to Book Concepts

| Project Component | Chapter Reference |
|---|---|
| `src/cisco_support/` directory | **Chapter 13** (Modules & Packages) — a Python package with `__init__.py` |
| `__init__.py` with `from .X import *` | **Chapter 13** — controlling what gets exported from a package |
| `auth.py` as shared utility | **Chapter 9** (Functions) + **Chapter 13** (Modules) — shared helper function |
| Each API class (Bug, EoX, etc.) | **Chapter 17** (OOP Basics) — class with `__init__`, methods |
| `requests.get()` / `requests.post()` | **Chapter 23** (REST APIs) — HTTP requests |
| `response.json()` | **Chapter 11** (JSON) — parsing JSON responses |
| `pyproject.toml` | **Chapter 29** (Project structure) — modern Python packaging |
| GitHub Actions CI/CD | **Chapter 29** — automated testing and deployment |

---

## 31.2 The Authentication Module (auth.py) — Functions as Building Blocks

```python
import requests

def generate_access_token(client_id, client_secret):
 url = 'https://id.cisco.com/oauth2/default/v1/token'
 headers = {
 'Content-Type': 'application/x-www-form-urlencoded'
 }
 data = {
 'client_id': client_id,
 'client_secret': client_secret,
 'grant_type': 'client_credentials'
 }

 response = requests.post(url, headers=headers, data=data)

 try:
 return response.json()['access_token']
 except:
 raise Exception(response.json()['errorSummary'])
```

### Concept Breakdown

**This is a standalone function, not a class** — and that's intentional.

> **Note (Chapter 9):** "Function has a name to run this code block as many times as you want."

> **Note:** The `login()`, `api_call()`, `logout()` pattern — shared utility functions that multiple scripts import.

**Why a function and not a class?** Authentication is a single action (get token), not a stateful object. Every API class calls this same function in its `__init__`. This is the **DRY principle** (Don't Repeat Yourself) — write auth logic once, use it everywhere.

**OAuth2 Client Credentials Flow:**

```python
data = {
 'client_id': client_id, # Dictionary — Chapter 5
 'client_secret': client_secret,
 'grant_type': 'client_credentials'
}
response = requests.post(url, headers=headers, data=data) # POST — Chapter 23
```

> **Note:** Same pattern — POST a login payload, extract a session token from the JSON response.

**Error handling with try/except:**

```python
try:
 return response.json()['access_token'] # Dict key access — Chapter 5
except:
 raise Exception(response.json()['errorSummary']) # Custom exception — Chapter 12
```

> **Note (Chapter 7):** "try/except is used to handle exceptions."

The bare `except:` is a code smell (should catch specific exceptions), but the intent is clear: if the response doesn't contain `access_token`, something went wrong — raise an error with the API's error message.

---

## 31.3 The Class Pattern — EoX as a Complete Example

```python
import requests
from . import auth

class EoX:
 def __init__(self, client_id, client_secret, proxies=None, verify=True):
 self.access_token = auth.generate_access_token(client_id, client_secret)
 self.base_url = "https://apix.cisco.com/supporttools/eox/rest/5"
 self.headers = {
 'Authorization': f'Bearer {self.access_token}'
 }
 self.proxies = proxies
 self.verify = verify

 def get_by_dates(self, start_date, end_date, page_index=1):
 url = f"{self.base_url}/EOXByDates/{page_index}/{start_date}/{end_date}?responseencoding=json"
 response = requests.get(url, headers=self.headers, verify=self.verify, proxies=self.proxies)
 return response.json()

 def get_by_product_ids(self, product_ids, page_index=1):
 url = f"{self.base_url}/EOXByProductID/{page_index}/{','.join(product_ids)}?responseencoding=json"
 response = requests.get(url, headers=self.headers, verify=self.verify, proxies=self.proxies)
 return response.json()

 def get_by_serial_numbers(self, serial_numbers, page_index=1):
 url = f"{self.base_url}/EOXBySerialNumber/{page_index}/{','.join(serial_numbers)}?responseencoding=json"
 response = requests.get(url, headers=self.headers, verify=self.verify, proxies=self.proxies)
 return response.json()

 def get_by_software_release_strings(self, softwares, page_index=1):
 sw = []
 for i, software in enumerate(softwares):
 sw.append(f"input{i+1}={software}")
 url = f"{self.base_url}/EOXBySWReleaseString/{page_index}?{'&'.join(sw)}&responseencoding=json"
 response = requests.get(url, headers=self.headers, verify=self.verify, proxies=self.proxies)
 return response.json()
```

### Line-by-Line Teaching

**Relative Import:**

```python
from . import auth # The dot means "from this same package"
```

> **Note (Chapter 13):** "from module import something" — the `.` means relative import within the same package.

**The `__init__` Method — Object Construction:**

> **Note (Chapter 17):** "The `__init__` method is called when creating an instance of a class."

> **Note:** Nearly identical pattern — `self.base_url = f"https://{host}/{mode}/v{api_version}/"`

```python
def __init__(self, client_id, client_secret, proxies=None, verify=True):
 self.access_token = auth.generate_access_token(client_id, client_secret)
 self.base_url = "https://apix.cisco.com/supporttools/eox/rest/5"
 self.headers = {
 'Authorization': f'Bearer {self.access_token}' # f-string — Chapter 3
 }
 self.proxies = proxies # Default params — Chapter 9
 self.verify = verify
```

**What `self` stores (instance attributes):** Each `EoX` object carries its own access token, base URL, and headers. When you create `eox = EoX(...)`, these live inside that specific object.

**Default parameters** `proxies=None, verify=True` — (Chapter 9, functions): allows optional arguments. Most users won't need a proxy, so it defaults to `None`.

**API Methods — The Consistent Pattern:**

Every method follows this exact structure:

```
1. Build the URL (f-string + string joining)
2. Make the HTTP request (requests.get)
3. Return parsed JSON (response.json())
```

**`','.join(product_ids)` — String Join from a List:**

> **Note (Chapter 3):** `"separator".join(list)` combines list elements into a string.

> **Note:** String splitting and joining for IP addresses.

```python
product_ids = ["WS-C3850-24T", "ISR4431"]
url_part = ','.join(product_ids) # "WS-C3850-24T,ISR4431"
```

The Cisco API expects comma-separated values in the URL. `.join()` handles this cleanly.

**`enumerate()` in `get_by_software_release_strings`:**

> **Note (Chapter 14):** "enumerate allows iterating with both index and element."

> **Note:** `for idx, fw in enumerate(my_firewalls)`

```python
sw = []
for i, software in enumerate(softwares): # enumerate — Chapter 14
 sw.append(f"input{i+1}={software}") # f-string — Chapter 3
url = f"...?{'&'.join(sw)}&responseencoding=json"
```

This builds query parameters like `?input1=IOS15.2&input2=IOS17.3` dynamically based on however many software versions are passed in.

**Dictionary Comprehension for Parameter Filtering:**

> **Note (Chapter 3):** Dictionary comprehensions for creating filtered dicts.

> **Chapter 16 (List Comprehensions):** The same `{k: v for k, v in ...}` pattern.

```python
# From bug.py — remove None values before sending to API
params = {k: v for k, v in params.items() if v is not None}
```

This is used in Bug, Case, and ServiceOrderReturn classes to strip out optional parameters that the user didn't provide. The API would reject `None` values, so they must be removed before the request.

---

## 31.4 The `__init__.py` — Package Re-Exports

```python
from .automated_software_distribution import *
from .bug import *
from .case import *
from .eox import *
from .product_information import *
from .serial_number import *
from .service_order_return import *
from .software_suggestion import *
```

> **Note (Chapter 13):** "from module import *" imports everything from a module.

This file is what makes `from cisco_support import Bug` work. Without it, you would need `from cisco_support.bug import Bug`. The `__init__.py` re-exports all classes at the package level for a clean user API.

---

## 31.5 Class Inheritance Diagram — How All Classes Relate

Every API class in this package follows the same pattern. Here is the structural relationship:

```
auth.py (standalone function)
│
│ generate_access_token(client_id, client_secret)
│ └── Called by every class __init__
│
├── Bug(client_id, client_secret)
│ ├── __init__ → gets token, sets base_url + headers
│ ├── get_by_ids(bug_ids)
│ ├── get_by_product_id(product_id, ...)
│ ├── get_by_pid_and_software_release(pid, release, ...)
│ ├── get_by_keywords(keywords, ...)
│ └── ...4 more methods
│
├── Case(client_id, client_secret)
│ ├── __init__ → gets token, sets base_url + headers
│ ├── get_summary_by_ids(case_ids)
│ ├── get_details_by_id(case_id)
│ ├── get_by_contract_ids(contract_ids, ...)
│ └── get_by_user_ids(user_ids, ...)
│
├── EoX(client_id, client_secret, proxies, verify)
│ ├── __init__ → gets token, sets base_url + headers + proxy/ssl
│ ├── get_by_dates(start_date, end_date)
│ ├── get_by_product_ids(product_ids)
│ ├── get_by_serial_numbers(serial_numbers)
│ └── get_by_software_release_strings(softwares)
│
├── ProductInformation(client_id, client_secret)
│ ├── __init__ → gets token, sets base_url + headers
│ ├── get_by_serial_numbers(serial_numbers)
│ ├── get_by_product_ids(product_ids)
│ └── get_mdf_by_ids(product_ids)
│
├── SerialNumberInformation(client_id, client_secret)
│ ├── __init__ → gets token, sets base_url + headers
│ ├── get_coverage_status_by_serial_numbers(sns)
│ ├── get_coverage_summary_by_serial_numbers(sns)
│ ├── get_coverage_status_by_instance_numbers(ins)
│ ├── get_orderable_product_ids_by_serial_numbers(sns)
│ └── get_owner_coverage_status_by_serial_numbers(sns)
│
├── ServiceOrderReturn(client_id, client_secret)
│ ├── __init__ → gets token, sets base_url + headers
│ ├── get_by_rma_number(rma_number)
│ └── get_by_user_id(user_id, ...)
│
├── SoftwareSuggestion(client_id, client_secret)
│ ├── __init__ → gets token, sets base_url + headers
│ ├── get_suggested_releases_and_images_by_pid(pids)
│ ├── get_suggested_releases_by_pid(pids)
│ ├── get_compatible_and_suggested_software_release_by_pid(pid, ...)
│ └── ...3 more methods
│
└── AutomatedSoftwareDistribution(client_id, client_secret)
 ├── __init__ → gets token, sets base_url + headers
 └── get_software_release_by_pid_and_release(pid, ...) ← uses POST
```

### The Repeating Pattern (every class follows this):

```python
class APIClassName:
 def __init__(self, client_id, client_secret):
 # 1. Authenticate (calls shared auth function)
 self.access_token = auth.generate_access_token(client_id, client_secret)
 # 2. Set the base URL for this specific API
 self.base_url = 'https://apix.cisco.com/...'
 # 3. Build auth headers
 self.headers = {'Authorization': f'Bearer {self.access_token}'}

 def get_by_something(self, param, optional_param=None):
 # 4. Build URL using f-strings and .join()
 url = f"{self.base_url}/endpoint/{param}"
 # 5. Make HTTP request
 response = requests.get(url, headers=self.headers)
 # 6. Return parsed JSON
 return response.json()
```

> **Note:** The `FirewallAPI` class follows this exact same pattern with `__init__`, `login`, `call`, `logout`.

---

## 31.6 Usage Example — Putting It All Together

Here is how you would use this library in a real network operations script:

```python
#!/usr/bin/env python
"""
Check End-of-Life status for network devices.
Combines: cisco_support library + Netmiko inventory collection.
"""
import os
import csv
from datetime import datetime
from netmiko import ConnectHandler
from cisco_support import EoX, SerialNumberInformation
from tabulate import tabulate

# --- PHASE 1: Collect device serial numbers via SSH (Script 10 pattern) ---
devices = [
 {"device_type": "cisco_ios", "ip": "10.0.0.1",
 "username": "admin", "password": os.getenv("NET_PASSWORD")},
 {"device_type": "cisco_ios", "ip": "10.0.0.2",
 "username": "admin", "password": os.getenv("NET_PASSWORD")},
]

serials = []
for device in devices:
 with ConnectHandler(**device) as nc: # Chapter 20
 output = nc.send_command("show version", use_genie=True) # Chapter 26
 serial = output["version"]["chassis_sn"] # Chapter 5
 pid = output["version"].get("pid", "Unknown")
 hostname = output["version"]["hostname"]
 serials.append({"hostname": hostname, "serial": serial, "pid": pid})

print(f"Collected serials from {len(serials)} devices") # Chapter 3

# --- PHASE 2: Check EoX status via Cisco Support API ---
client_id = os.getenv("CISCO_API_CLIENT_ID") # Chapter 19
client_secret = os.getenv("CISCO_API_CLIENT_SECRET")

eox = EoX(client_id=client_id, client_secret=client_secret) # Chapter 17

serial_list = [d["serial"] for d in serials] # List comp — Chapter 16
eox_data = eox.get_by_serial_numbers(serial_list) # API call — Chapter 23

# --- PHASE 3: Build report ---
report = [["Hostname", "Serial", "PID", "EoL Announced", "End of Support"]]

for record in eox_data.get("EOXRecord", []): # .get() safe access — Chapter 5
 serial = record.get("EOXInputValue", "")
 eol_date = record.get("EndOfSaleDate", {}).get("value", "N/A")
 eos_date = record.get("LastDateOfSupport", {}).get("value", "N/A")

 # Match serial to hostname
 device = next((d for d in serials if d["serial"] == serial), None) # Generator — Chapter 16
 hostname = device["hostname"] if device else "Unknown"
 pid = device["pid"] if device else "Unknown"

 report.append([hostname, serial, pid, eol_date, eos_date])

print(tabulate(report, headers="firstrow", tablefmt="grid"))

with open(f"eox_report_{datetime.now():%Y%m%d}.csv", "w", newline="") as f:
 csv.writer(f).writerows(report) # Chapter 11

print("Report saved.")
```

**This single script uses concepts from 15+ chapters:**

| Line(s) | Concept | Chapter |
|---|---|---|
| `import os` | Modules | Chapter 13 |
| `os.getenv()` | Environment variables | Chapter 19 |
| `ConnectHandler(**device)` | Dict unpacking, Netmiko | Chapter 9, 20 |
| `with ... as nc:` | Context manager | Chapter 10 |
| `use_genie=True` | Structured parsing | Chapter 26 |
| `output["version"]["chassis_sn"]` | Nested dict access | Chapter 5 |
| `.get("key", default)` | Safe dict access | Chapter 5 |
| `[d["serial"] for d in serials]` | List comprehension | Chapter 16 |
| `EoX(client_id=...)` | OOP instantiation | Chapter 17 |
| `eox.get_by_serial_numbers()` | Method calls | Chapter 17 |
| `for record in data:` | Loops | Chapter 8 |
| `next((d for d in ...))` | Generator expression | Chapter 16 |
| `tabulate()` | Third-party library | Chapter 13 |
| `csv.writer().writerows()` | CSV export | Chapter 11 |
| f-string with datetime format | String formatting | Chapter 3 |

---

## 31.7 Chapter 31 Lab Tasks

**Task 31.1 — Read and Map the Code:**
Clone the `cisco_support` repo. Read each `.py` file and create a handwritten diagram showing how `__init__.py` connects to each class, and how each class connects to `auth.py`.

**Task 31.2 — Identify the Pattern:**
List every method across all classes that uses `{','.join(some_list)}` in the URL construction. What Python concept from Chapter 3 is being used? Why is this needed?

**Task 31.3 — Refactor with a Base Class:**
All 8 classes share the same `__init__` pattern (auth + base_url + headers). Create a `CiscoSupportBase` class with a shared `__init__`, and refactor `Bug` and `EoX` to inherit from it. (Hint: Chapter 18 — Inheritance)

**Task 31.4 — Build Your Own API Wrapper:**
Using the `cisco_support` repo as a template, create a Python class called `MerakiDashboard` that wraps the Meraki Dashboard API (or any public REST API). It should have: `__init__` with API key, `get_organizations()`, `get_networks(org_id)`. Follow the exact same pattern.

**Task 31.5 — End-to-End Automation:**
Write a complete script that: (1) connects to lab devices with Netmiko to collect serial numbers, (2) uses the `cisco_support.EoX` class to check EoL status, and (3) exports a CSV report. Use error handling, environment variables, and functions. This combines Chapters 5, 8, 9, 10, 11, 12, 13, 17, 19, 20, 23, and 29.

---

## Appendix A (continued): Chapter 30–31 Answers

**30.2:**
```python
from datetime import datetime
timestamp = datetime.now().strftime("%Y-%m-%d_%H%M")
with open(f'backup/{hostname}_{timestamp}.cfg', 'w') as file:
 file.write(output)
```

**30.3:**
```python
from concurrent.futures import ThreadPoolExecutor, as_completed

def collect_inventory(ip):
 ios_device = {'device_type': 'cisco_ios', 'ip': ip, 'username': username, 'password': password}
 nc = ConnectHandler(**ios_device)
 output = nc.send_command('show version', use_genie=True)
 nc.disconnect()
 v = output["version"]
 return [v["hostname"], v["chassis"], v["chassis_sn"], v["os"], v["version"]]

with ThreadPoolExecutor(max_workers=5) as pool:
 futures = {pool.submit(collect_inventory, ip): ip for ip in device_list}
 for future in as_completed(futures):
 try:
 inventory.append(future.result())
 except Exception as e:
 print(f"Error on {futures[future]}: {e}")
```

**31.3:**
```python
import requests
from . import auth

class CiscoSupportBase:
 """Base class for all Cisco Support API wrappers."""
 def __init__(self, client_id, client_secret, base_url):
 self.access_token = auth.generate_access_token(client_id, client_secret)
 self.base_url = base_url
 self.headers = {'Authorization': f'Bearer {self.access_token}'}

 def _get(self, endpoint, params=None):
 """Shared GET request method."""
 url = f"{self.base_url}/{endpoint}"
 if params:
 params = {k: v for k, v in params.items() if v is not None}
 response = requests.get(url, headers=self.headers, params=params)
 return response.json()


class Bug(CiscoSupportBase):
 def __init__(self, client_id, client_secret):
 super().__init__(client_id, client_secret,
 'https://apix.cisco.com/bug/v2.0/bugs')

 def get_by_ids(self, bug_ids):
 return self._get(f"bug_ids/{','.join(bug_ids)}")


class EoX(CiscoSupportBase):
 def __init__(self, client_id, client_secret, proxies=None, verify=True):
 super().__init__(client_id, client_secret,
 'https://apix.cisco.com/supporttools/eox/rest/5')
 self.proxies = proxies
 self.verify = verify

 def get_by_serial_numbers(self, serial_numbers, page_index=1):
 endpoint = f"EOXBySerialNumber/{page_index}/{','.join(serial_numbers)}?responseencoding=json"
 return self._get(endpoint)
```


---


---

# 32. Building a Netmiko AI Agent with the OpenAI Python SDK

This chapter brings together everything from Chapters 1–31 into a single, cutting-edge project: an AI-powered network automation agent. The agent uses OpenAI's function calling (tool use) to let a large language model decide which Netmiko operations to perform based on natural language commands.

**What you will build:** A conversational AI agent where you type things like *"Back up the config on router 10.0.0.1"* or *"Check the EoL status of serial number FTX1234ABCD"* and the agent translates your intent into actual Netmiko SSH sessions, API calls, and file operations — automatically.

---

## 32.1 Architecture Overview

```
┌─────────────────────────────────────────────────────────┐
│ YOU (Network Engineer) │
│ "Show me the running config of rtr1" │
└──────────────────────────┬──────────────────────────────┘
 │ Natural language
 ▼
┌─────────────────────────────────────────────────────────┐
│ OpenAI Chat Completions API │
│ (gpt-4o / gpt-4.1) │
│ │
│ The LLM reads your request + tool definitions. │
│ It decides WHICH tool to call and WITH WHAT arguments. │
│ It returns a tool_call with structured JSON args. │
└──────────────────────────┬──────────────────────────────┘
 │ tool_call: send_show_command(
 │ device_ip="10.0.0.1",
 │ command="show running-config")
 ▼
┌─────────────────────────────────────────────────────────┐
│ YOUR PYTHON AGENT (this script) │
│ │
│ 1. Receives the tool_call from OpenAI │
│ 2. Executes the REAL function (Netmiko SSH / API call) │
│ 3. Sends the output BACK to OpenAI │
│ 4. OpenAI summarizes the result in plain English │
└──────────────────────────┬──────────────────────────────┘
 │
 ┌────────────────┼────────────────┐
 ▼ ▼ ▼
 ┌────────────┐ ┌────────────┐ ┌────────────────┐
 │ Netmiko │ │ Cisco │ │ File System │
 │ SSH to │ │ Support │ │ (backup/ │
 │ devices │ │ APIs │ │ reports) │
 └────────────┘ └────────────┘ └────────────────┘
```

**Key insight:** The AI does NOT directly SSH into your devices. Your Python code does. The AI just decides which function to call and with what parameters. You maintain full control.

---

## 32.2 Installation and Setup

### Step 1: Install Required Packages

```bash
# Create and activate a virtual environment (Chapter 1)
python3 -m venv ~/ai_netauto_venv
source ~/ai_netauto_venv/bin/activate

# Install all dependencies
pip install openai netmiko python-dotenv pyyaml tabulate cisco-support rich
```

**Package purposes:**

| Package | Purpose | Chapter Reference |
|---|---|---|
| `openai` | OpenAI API SDK — the AI brain | New (Chapter 32) |
| `netmiko` | SSH to network devices | Chapter 20–22 |
| `python-dotenv` | Load `.env` credentials | Chapter 19, 23 |
| `pyyaml` | Read device inventory YAML | Chapter 11 |
| `tabulate` | Pretty terminal tables | Chapter 30 (Script 10) |
| `cisco-support` | Cisco EoX/Bug/Serial APIs | Chapter 31 |
| `rich` | Colored terminal output | Chapter 1 (KByers style) |

### Step 2: Get Your OpenAI API Key

1. Go to **https://platform.openai.com/api-keys**
2. Click **"Create new secret key"**
3. Copy the key (starts with `sk-...`)
4. **Never put this key in your code or commit it to git**

### Step 3: Create Your .env File

> **Note (Chapter 10):** "File .gitignore contains file and directory patterns that Git should ignore."

> **Note:** `load_dotenv(); admin_pass = os.environ["CISCO_FW_ADMIN"]`

```bash
# Create .env file (NEVER commit this to git)
cat > .env << 'EOF'
OPENAI_API_KEY=sk-proj-your-key-here
DEVICE_USERNAME=cisco
DEVICE_PASSWORD=cisco
CISCO_CLIENT_ID=your-cisco-api-client-id
CISCO_CLIENT_SECRET=your-cisco-api-client-secret
EOF

# Add to .gitignore immediately
echo ".env" >> .gitignore
```

### Step 4: Create Device Inventory (YAML)

> **Note (Chapter 11):** "YAML is often used for storing configuration parameters."

```yaml
# devices.yaml
---
- hostname: rtr1
 device_type: cisco_ios
 ip: 198.18.1.11
- hostname: rtr2
 device_type: cisco_ios
 ip: 198.18.1.12
```

---

## 32.3 The Network Tools — Functions the AI Can Call

These are regular Python functions. Each one does real work: SSH connections, file I/O, API calls. The AI will choose which to call based on your request.

> **Note (Chapter 9):** "Function has a name to run this code block as many times as you want."

> **Note:** Functions as reusable building blocks (`login`, `api_call`, `logout`).

```python
# network_tools.py
"""
Network automation tools that the AI agent can invoke.
Each function performs a real operation via SSH or API.
"""
import os
import json
import csv
import yaml
from datetime import datetime
from netmiko import ConnectHandler # Chapter 20
from netmiko import NetmikoAuthenticationException # Chapter 12
from netmiko import NetmikoTimeoutException
from dotenv import load_dotenv # Chapter 19

load_dotenv()
USERNAME = os.getenv("DEVICE_USERNAME", "cisco") # Chapter 19 (env vars)
PASSWORD = os.getenv("DEVICE_PASSWORD", "cisco")


def _connect(device_ip, device_type="cisco_ios"):
 """Internal helper: create a Netmiko connection.

 > KByers Netmiko Course class1/simple_conn_dict.py — device dict pattern.
 > Chapter 20 — Connection to network devices.
 """
 device = { # Chapter 5 (dicts)
 "device_type": device_type,
 "ip": device_ip,
 "username": USERNAME,
 "password": PASSWORD,
 }
 return ConnectHandler(**device) # Chapter 9 (**unpacking)


# ── Tool 1: Send Show Command ──────────────────────────────────
def send_show_command(device_ip: str, command: str,
 device_type: str = "cisco_ios") -> str:
 """SSH to a device and execute a show command.

 """
 try: # Chapter 12 (try/except)
 nc = _connect(device_ip, device_type)
 output = nc.send_command(command) # Chapter 21
 nc.disconnect()
 return output
 except NetmikoAuthenticationException:
 return f"ERROR: Authentication failed for {device_ip}"
 except NetmikoTimeoutException:
 return f"ERROR: Timeout connecting to {device_ip}"
 except Exception as e:
 return f"ERROR: {str(e)}"


# ── Tool 2: Send Config Commands ───────────────────────────────
def send_config_commands(device_ip: str, commands: list,
 device_type: str = "cisco_ios") -> str:
 """SSH to a device and push configuration commands.

 > Netmiko Course class5 — send_config_set()
 """
 try:
 nc = _connect(device_ip, device_type)
 output = nc.send_config_set(commands) # Chapter 22
 output += nc.save_config()
 nc.disconnect()
 return output
 except Exception as e:
 return f"ERROR: {str(e)}"


# ── Tool 3: Backup Running Config ──────────────────────────────
def backup_config(device_ip: str,
 device_type: str = "cisco_ios") -> str:
 """Backup running config to a timestamped file.

 — file writing with context manager
 """
 try:
 nc = _connect(device_ip, device_type)
 hostname = nc.find_prompt()[:-1] # Chapter 3 (slicing)
 output = nc.send_command("show running-config")
 nc.disconnect()

 os.makedirs("backup", exist_ok=True) # Chapter 19 (os)
 timestamp = datetime.now().strftime("%Y%m%d_%H%M%S")
 filename = f"backup/{hostname}_{timestamp}.cfg"

 with open(filename, "w") as f: # Chapter 10 (files)
 f.write(output)

 return f"Config saved to {filename} ({len(output)} bytes)"
 except Exception as e:
 return f"ERROR: {str(e)}"


# ── Tool 4: Get Device Inventory ───────────────────────────────
def get_device_inventory(device_ip: str,
 device_type: str = "cisco_ios") -> str:
 """Collect structured inventory (hostname, serial, model, version).

 — nested dict navigation
 """
 try:
 nc = _connect(device_ip, device_type)
 output = nc.send_command("show version", use_genie=True) # Chapter 26
 nc.disconnect()

 if isinstance(output, dict):
 v = output.get("version", {}) # Chapter 5 (.get)
 info = {
 "hostname": v.get("hostname", "N/A"),
 "chassis": v.get("chassis", "N/A"),
 "serial": v.get("chassis_sn", "N/A"),
 "os": v.get("os", "N/A"),
 "version": v.get("version", "N/A"),
 "uptime": v.get("uptime", "N/A"),
 }
 return json.dumps(info, indent=2) # Chapter 11 (JSON)
 else:
 return f"Genie parsing not available. Raw output:\n{output[:500]}"
 except Exception as e:
 return f"ERROR: {str(e)}"


# ── Tool 5: Check EoL Status via Cisco Support API ────────────
def check_eol_status(serial_numbers: list) -> str:
 """Query Cisco EoX API for End-of-Life status.

 > Chapter 31 — cisco_support library (EoX class)
 — REST API patterns
 """
 try:
 from cisco_support import EoX # Chapter 31

 client_id = os.getenv("CISCO_CLIENT_ID")
 client_secret = os.getenv("CISCO_CLIENT_SECRET")

 if not client_id or not client_secret:
 return "ERROR: CISCO_CLIENT_ID and CISCO_CLIENT_SECRET not set in .env"

 eox = EoX(client_id=client_id, client_secret=client_secret)
 result = eox.get_by_serial_numbers(serial_numbers)

 records = result.get("EOXRecord", []) # Chapter 5
 if not records:
 return "No EoL records found for the given serial numbers."

 summary = []
 for rec in records:
 summary.append({
 "serial": rec.get("EOXInputValue", "N/A"),
 "product_id": rec.get("EOLProductID", "N/A"),
 "end_of_sale": rec.get("EndOfSaleDate", {}).get("value", "N/A"),
 "end_of_support": rec.get("LastDateOfSupport", {}).get("value", "N/A"),
 })
 return json.dumps(summary, indent=2)
 except Exception as e:
 return f"ERROR: {str(e)}"


# ── Tool 6: Check Bug Details ──────────────────────────────────
def check_bugs(bug_ids: list) -> str:
 """Look up Cisco bug details by bug IDs.

 > Chapter 31 — cisco_support library (Bug class)
 """
 try:
 from cisco_support import Bug

 client_id = os.getenv("CISCO_CLIENT_ID")
 client_secret = os.getenv("CISCO_CLIENT_SECRET")

 if not client_id or not client_secret:
 return "ERROR: CISCO_CLIENT_ID and CISCO_CLIENT_SECRET not set"

 bug = Bug(client_id=client_id, client_secret=client_secret)
 result = bug.get_by_ids(bug_ids)

 bugs = result.get("bugs", [])
 summary = []
 for b in bugs:
 summary.append({
 "bug_id": b.get("bug_id"),
 "headline": b.get("headline"),
 "severity": b.get("severity"),
 "status": b.get("status"),
 "product": b.get("product"),
 })
 return json.dumps(summary, indent=2)
 except Exception as e:
 return f"ERROR: {str(e)}"
```

---

## 32.4 Defining Tools for OpenAI — The JSON Schema

The AI needs to know what tools are available. You describe each tool as a JSON schema. The AI reads these schemas and decides which tool to call based on your natural language request.

> **Note (Chapter 7):** Nested dictionaries for structured data.

> **Chapter 31 (cisco_support):** Same pattern — each API method has defined parameters.

```python
# tool_definitions.py
"""
OpenAI function calling tool definitions.
These JSON schemas tell the AI what tools are available
and what parameters each tool accepts.
"""

TOOLS = [
 {
 "type": "function",
 "function": {
 "name": "send_show_command",
 "description": "SSH to a Cisco network device and run a show command. Use for any read-only CLI command like 'show version', 'show ip route', 'show interfaces', 'show running-config', etc.",
 "parameters": {
 "type": "object",
 "properties": {
 "device_ip": {
 "type": "string",
 "description": "IP address of the device"
 },
 "command": {
 "type": "string",
 "description": "The IOS show command to execute"
 },
 "device_type": {
 "type": "string",
 "description": "Netmiko device type",
 "enum": ["cisco_ios", "cisco_nxos", "cisco_xe",
 "arista_eos", "juniper_junos"],
 }
 },
 "required": ["device_ip", "command"],
 "additionalProperties": False
 },
 "strict": True
 }
 },
 {
 "type": "function",
 "function": {
 "name": "send_config_commands",
 "description": "SSH to a device and push configuration changes. The device config will be saved automatically after changes. Use for any configuration task.",
 "parameters": {
 "type": "object",
 "properties": {
 "device_ip": {
 "type": "string",
 "description": "IP address of the device"
 },
 "commands": {
 "type": "array",
 "items": {"type": "string"},
 "description": "List of IOS config commands"
 },
 "device_type": {
 "type": "string",
 "description": "Netmiko device type",
 "enum": ["cisco_ios", "cisco_nxos", "cisco_xe",
 "arista_eos", "juniper_junos"],
 }
 },
 "required": ["device_ip", "commands"],
 "additionalProperties": False
 },
 "strict": True
 }
 },
 {
 "type": "function",
 "function": {
 "name": "backup_config",
 "description": "Backup the running configuration of a device to a local timestamped file.",
 "parameters": {
 "type": "object",
 "properties": {
 "device_ip": {
 "type": "string",
 "description": "IP address of the device"
 },
 "device_type": {
 "type": "string",
 "description": "Netmiko device type",
 "enum": ["cisco_ios", "cisco_nxos", "cisco_xe",
 "arista_eos", "juniper_junos"],
 }
 },
 "required": ["device_ip"],
 "additionalProperties": False
 },
 "strict": True
 }
 },
 {
 "type": "function",
 "function": {
 "name": "get_device_inventory",
 "description": "Collect structured device inventory info (hostname, serial number, model, OS version, uptime) via SSH.",
 "parameters": {
 "type": "object",
 "properties": {
 "device_ip": {
 "type": "string",
 "description": "IP address of the device"
 },
 "device_type": {
 "type": "string",
 "description": "Netmiko device type",
 "enum": ["cisco_ios", "cisco_nxos", "cisco_xe",
 "arista_eos", "juniper_junos"],
 }
 },
 "required": ["device_ip"],
 "additionalProperties": False
 },
 "strict": True
 }
 },
 {
 "type": "function",
 "function": {
 "name": "check_eol_status",
 "description": "Check Cisco End-of-Life / End-of-Support status for one or more device serial numbers using the Cisco Support API.",
 "parameters": {
 "type": "object",
 "properties": {
 "serial_numbers": {
 "type": "array",
 "items": {"type": "string"},
 "description": "List of Cisco serial numbers"
 }
 },
 "required": ["serial_numbers"],
 "additionalProperties": False
 },
 "strict": True
 }
 },
 {
 "type": "function",
 "function": {
 "name": "check_bugs",
 "description": "Look up Cisco bug details by bug IDs (e.g., CSCxx12345) using the Cisco Support API.",
 "parameters": {
 "type": "object",
 "properties": {
 "bug_ids": {
 "type": "array",
 "items": {"type": "string"},
 "description": "List of Cisco bug IDs"
 }
 },
 "required": ["bug_ids"],
 "additionalProperties": False
 },
 "strict": True
 }
 },
]
```

---

## 32.5 The Agent Loop — Bringing It All Together

This is the main script. It implements the **OpenAI function calling loop**: send a message → AI decides on a tool → execute the tool → send result back → AI summarizes.

```python
#!/usr/bin/env python
"""
netmiko_ai_agent.py — AI-powered network automation agent.

Combines: OpenAI function calling + Netmiko SSH + Cisco Support APIs.
Uses concepts from ALL chapters of this guide.
"""
import os
import json
from openai import OpenAI # NEW: OpenAI SDK
from dotenv import load_dotenv # Chapter 19
from rich.console import Console # Chapter 1 (KByers)
from rich.markdown import Markdown
from network_tools import ( # Chapter 13 (modules)
 send_show_command,
 send_config_commands,
 backup_config,
 get_device_inventory,
 check_eol_status,
 check_bugs,
)
from tool_definitions import TOOLS # Chapter 13

# ── Setup ──────────────────────────────────────────────────────
load_dotenv()
console = Console()

# Initialize OpenAI client
# The SDK automatically reads OPENAI_API_KEY from environment
client = OpenAI(
 api_key=os.environ.get("OPENAI_API_KEY"), # Chapter 19 (env vars)
)

# Map tool names to actual Python functions (Chapter 5 — dict as dispatch table)
TOOL_DISPATCH = {
 "send_show_command": send_show_command,
 "send_config_commands": send_config_commands,
 "backup_config": backup_config,
 "get_device_inventory": get_device_inventory,
 "check_eol_status": check_eol_status,
 "check_bugs": check_bugs,
}

# System prompt — tells the AI who it is and how to behave
SYSTEM_PROMPT = """You are a senior network automation engineer AI assistant.
You have access to tools that can SSH into Cisco network devices,
push configurations, back up configs, collect inventory, and query
Cisco Support APIs for End-of-Life and bug information.

Guidelines:
- Always confirm BEFORE pushing configuration changes.
- When showing command output, summarize key findings.
- For inventory requests, present data in a clean table format.
- If a tool returns an error, explain what went wrong and suggest fixes.
- For EoL checks, highlight any devices past End-of-Support date.
- Be concise but thorough.
"""


# ── The Agent Loop ─────────────────────────────────────────────
def execute_tool_call(tool_name, tool_args):
 """Execute a tool and return its output.

 > Chapter 9 (Functions) — callable dispatch
 > Chapter 5 (Dictionaries) — dict as function lookup table
 """
 func = TOOL_DISPATCH.get(tool_name) # Chapter 5 (.get)
 if func is None:
 return f"ERROR: Unknown tool '{tool_name}'"

 try: # Chapter 12 (try/except)
 result = func(**tool_args) # Chapter 9 (**unpacking)
 return result
 except Exception as e:
 return f"ERROR executing {tool_name}: {str(e)}"


def chat(user_message, conversation_history):
 """Send a message and handle the full tool-calling loop.

 This implements the OpenAI function calling flow:
 1. Send user message + tool definitions to the API
 2. If AI wants to call a tool → execute it → send result back
 3. Repeat until AI gives a final text response
 4. Return the response

 > Chapter 8 (while loop) — loop until AI gives final answer
 > Chapter 12 (error handling) — handle API and tool failures
 """
 # Add user message to history
 conversation_history.append({ # Chapter 4 (lists)
 "role": "user",
 "content": user_message
 })

 # Circuit breaker to prevent infinite loops
 max_iterations = 10
 iteration = 0

 while iteration < max_iterations: # Chapter 8 (while)
 iteration += 1

 # Call OpenAI Chat Completions API
 response = client.chat.completions.create(
 model="gpt-4o",
 messages=conversation_history,
 tools=TOOLS,
 )

 message = response.choices[0].message

 # Check if the AI wants to call tool(s)
 if message.tool_calls:
 # Add AI's response (with tool calls) to history
 conversation_history.append(message)

 # Execute each tool call
 for tool_call in message.tool_calls: # Chapter 8 (for loop)
 tool_name = tool_call.function.name
 tool_args = json.loads( # Chapter 11 (JSON)
 tool_call.function.arguments
 )

 console.print(
 f"[bold yellow]⚡ Calling tool:[/bold yellow] "
 f"{tool_name}({json.dumps(tool_args, indent=2)})"
 )

 # Execute the actual function
 result = execute_tool_call(tool_name, tool_args)

 # Send tool result back to the AI
 conversation_history.append({ # Chapter 4 (.append)
 "role": "tool",
 "tool_call_id": tool_call.id,
 "content": str(result),
 })

 else:
 # No tool calls — this is the final response
 conversation_history.append({
 "role": "assistant",
 "content": message.content
 })
 return message.content

 return "ERROR: Maximum iterations reached. The agent may be stuck in a loop."


# ── Main Interactive Loop ──────────────────────────────────────
def main():
 """Interactive chat loop.

 > Chapter 8 (while True with break)
 """
 console.print("[bold green]╔════════════════════════════════════════╗[/bold green]")
 console.print("[bold green]║ Netmiko AI Agent — Network Copilot ║[/bold green]")
 console.print("[bold green]╚════════════════════════════════════════╝[/bold green]")
 console.print("Type your network automation request. Type 'quit' to exit.\n")

 conversation_history = [ # Chapter 4 (lists)
 {"role": "system", "content": SYSTEM_PROMPT} # Chapter 5 (dicts)
 ]

 while True: # Chapter 8 (infinite loop)
 user_input = input("[bold cyan]You:[/bold cyan] ").strip()

 if user_input.lower() in ("quit", "exit", "q"): # Chapter 7 (conditionals)
 console.print("[dim]Goodbye![/dim]")
 break # Chapter 8 (break)

 if not user_input: # Chapter 6 (truthiness)
 continue # Chapter 8 (continue)

 try:
 response = chat(user_input, conversation_history)
 console.print(f"\n[bold green]Agent:[/bold green] {response}\n")
 except Exception as e: # Chapter 12
 console.print(f"[bold red]Error:[/bold red] {str(e)}\n")


if __name__ == "__main__": # Chapter 13
 main()
```

---

## 32.6 Running the Agent — Example Session

```bash
# Set environment variables
export OPENAI_API_KEY=sk-proj-your-key-here
export DEVICE_USERNAME=cisco
export DEVICE_PASSWORD=cisco

# Run the agent
python netmiko_ai_agent.py
```

**Example conversation:**

```
╔════════════════════════════════════════╗
║ Netmiko AI Agent — Network Copilot ║
╚════════════════════════════════════════╝
Type your network automation request. Type 'quit' to exit.

You: Show me the interfaces on 198.18.1.11

⚡ Calling tool: send_show_command({
 "device_ip": "198.18.1.11",
 "command": "show ip interface brief"
})

Agent: Here's the interface summary for 198.18.1.11:

| Interface | IP Address | Status | Protocol |
|-----------------|-------------|--------|----------|
| GigabitEthernet1 | 198.18.1.11 | up | up |
| GigabitEthernet2 | unassigned | down | down |
| Loopback0 | 10.0.0.1 | up | up |

All critical interfaces are operational. GigabitEthernet2 is
administratively down — this may be expected for an unused port.

You: Back up the config on that device

⚡ Calling tool: backup_config({
 "device_ip": "198.18.1.11"
})

Agent: Configuration backup completed successfully.
Saved to: backup/rtr1_20260313_143022.cfg (15,847 bytes)

You: Configure a new loopback interface on 198.18.1.11
 with IP 10.99.99.1/32 and description "Created by AI Agent"

⚡ Calling tool: send_config_commands({
 "device_ip": "198.18.1.11",
 "commands": [
 "interface Loopback99",
 "description Created by AI Agent",
 "ip address 10.99.99.1 255.255.255.255",
 "no shutdown"
 ]
})

Agent: Configuration applied and saved. I created Loopback99 with
IP 10.99.99.1/32 on 198.18.1.11. The config was saved to startup.

You: Check the EoL status for serial number FTX1234ABCD

⚡ Calling tool: check_eol_status({
 "serial_numbers": ["FTX1234ABCD"]
})

Agent: EoL Status for FTX1234ABCD:
- Product ID: WS-C3850-24T
- End of Sale: 2022-10-31
- End of Support: 2027-10-31

⚠️ This device is past End-of-Sale but still within support
until October 2027. I recommend planning a hardware refresh
within the next 18 months.

You: quit
Goodbye!
```

---

## 32.7 Complete Concept Map — Every Chapter in One Project

| Component | Chapters Used | What It Demonstrates |
|---|---|---|
| `python3 -m venv` | Chapter 1 | Environment setup |
| `.env` + `load_dotenv()` | Chapter 10, 19 | File I/O, environment variables |
| `devices.yaml` | Chapter 11 | YAML structured data |
| `device = {...}` | Chapter 5 | Dictionaries |
| `ConnectHandler(**device)` | Chapter 9, 20 | Functions, dict unpacking, Netmiko |
| `try/except` blocks | Chapter 12 | Error handling |
| `nc.send_command()` | Chapter 21 | Show commands |
| `nc.send_config_set()` | Chapter 22 | Config push |
| `nc.find_prompt()[:-1]` | Chapter 3 | String slicing |
| `use_genie=True` | Chapter 26 | Structured parsing |
| `json.loads()` / `json.dumps()` | Chapter 11 | JSON processing |
| `from network_tools import ...` | Chapter 13 | Modules and packages |
| `TOOL_DISPATCH = {...}` | Chapter 5, 9 | Dict as function dispatch table |
| `func(**tool_args)` | Chapter 9 | kwargs unpacking |
| `for tool_call in ...` | Chapter 8 | Loops |
| `while iteration < max` | Chapter 8 | While loop with circuit breaker |
| `conversation_history.append()` | Chapter 4 | List operations |
| `if __name__ == "__main__"` | Chapter 13 | Module entry point |
| `EoX(client_id=...)` | Chapter 17, 31 | OOP, Cisco Support APIs |
| `os.makedirs(..., exist_ok=True)` | Chapter 19 | OS interaction |
| `with open(...) as f:` | Chapter 10 | Context manager |
| f-strings everywhere | Chapter 3 | String formatting |
| `input().strip().lower()` | Chapter 3 | String methods chaining |

---

## 32.8 Chapter 32 Lab Tasks

**Task 32.1 — Install and Verify:**
Install all required packages. Create a `.env` file with your OpenAI API key. Write a 5-line test script that calls `client.chat.completions.create()` with a simple message and prints the response. Verify it works.

**Task 32.2 — Add a New Tool:**
Add a 7th tool called `get_arp_table` that SSHes to a device and runs `show arp`. Write the function in `network_tools.py`, add the JSON schema to `tool_definitions.py`, and register it in `TOOL_DISPATCH`. Test it by asking the agent "Show me the ARP table on 198.18.1.11."

**Task 32.3 — Add Conversation Memory:**
Modify the agent to save conversation history to a JSON file after each session and reload it at startup. This gives the agent memory across sessions. (Hint: use `json.dump()` and `json.load()` from Chapter 11.)

**Task 32.4 — Add Multi-Device Support:**
Add a tool called `run_on_all_devices` that reads `devices.yaml`, loops through all devices (Chapter 8), runs a given show command on each using `ThreadPoolExecutor` (Chapter 24), and returns a combined report.

**Task 32.5 — Full Production Agent:**
Combine everything into a production-ready project with this structure:
```
ai_netauto/
├── .env
├── .gitignore
├── requirements.txt
├── devices.yaml
├── network_tools.py
├── tool_definitions.py
├── netmiko_ai_agent.py
└── tests/
 └── test_tools.py
```
Add pytest tests (Chapter 27) for at least 3 tool functions. Add a `--no-confirm` flag to skip config change confirmations in CI/CD mode. Document everything with docstrings (Chapter 9).

---

## Appendix A (continued): Chapter 32 Answers

**32.1:**
```python
import os
from openai import OpenAI
from dotenv import load_dotenv

load_dotenv()
client = OpenAI(api_key=os.environ.get("OPENAI_API_KEY"))

response = client.chat.completions.create(
 model="gpt-4o",
 messages=[{"role": "user", "content": "Say hello in 5 words."}]
)
print(response.choices[0].message.content)
```

**32.2 — The new tool function:**
```python
# Add to network_tools.py
def get_arp_table(device_ip: str, device_type: str = "cisco_ios") -> str:
 """Collect the ARP table from a device."""
 try:
 nc = _connect(device_ip, device_type)
 output = nc.send_command("show arp")
 nc.disconnect()
 return output
 except Exception as e:
 return f"ERROR: {str(e)}"
```

**32.2 — The JSON schema (add to TOOLS list):**
```python
{
 "type": "function",
 "function": {
 "name": "get_arp_table",
 "description": "Retrieve the ARP table from a network device.",
 "parameters": {
 "type": "object",
 "properties": {
 "device_ip": {"type": "string", "description": "Device IP"},
 "device_type": {
 "type": "string",
 "description": "Netmiko device type",
 "enum": ["cisco_ios", "cisco_nxos", "cisco_xe",
 "arista_eos", "juniper_junos"],
 }
 },
 "required": ["device_ip"],
 "additionalProperties": False
 },
 "strict": True
 }
}
```

**32.2 — Register in dispatch:**
```python
TOOL_DISPATCH["get_arp_table"] = get_arp_table
```

---


---

# 33. Building a Netmiko MCP Server for Claude — From Scratch

This is the grand finale of the guide. You will build a **Model Context Protocol (MCP) server** that gives Claude (or any MCP-compatible AI) the power to SSH into your network devices, back up configs, push changes, and query Cisco Support APIs — all through natural language conversation.

Think of it this way: in Chapter 32, you built an AI agent that talks to OpenAI. In this chapter, you build a **tool server** that Claude Desktop (or Claude.ai) can connect to directly. No middleman script needed — Claude calls your tools natively.

---

## 33.1 What is MCP? (Explained Like You're 10)

Imagine you have a really smart friend (Claude) who knows a lot about networking, but is locked in a room with no computer. They can talk to you, answer questions, and give advice — but they cannot actually *do* anything on your network.

Now imagine you install a special walkie-talkie system between your friend's room and your network lab. Through this walkie-talkie, your friend can say "Hey, run `show version` on router 10.0.0.1" — and the walkie-talkie system actually does it and reads the result back.

**That walkie-talkie system is MCP.**

```
┌──────────────────────┐ ┌───────────────────────┐
│ │ │ │
│ CLAUDE │ │ YOUR MCP SERVER │
│ (The Smart Friend)│◄────────►│ (The Walkie-Talkie) │
│ │ MCP │ │
│ "Show me the config │ Protocol │ Actually SSHes into │
│ on router 10.0.0.1"│ │ your routers with │
│ │ │ Netmiko and returns │
│ Understands network │ │ the real output │
│ concepts, summarizes│ │ │
│ output, gives advice│ │ │
└──────────────────────┘ └───────────┬───────────┘
 │
 │ SSH / HTTPS
 ▼
 ┌───────────────────────┐
 │ YOUR NETWORK DEVICES │
 │ Routers, Switches, │
 │ Firewalls │
 └───────────────────────┘
```

### The Three Things an MCP Server Can Provide

| MCP Primitive | Analogy | Network Example |
|---|---|---|
| **Tools** | Buttons Claude can press | "Run show command", "Push config", "Backup config" |
| **Resources** | Files Claude can read | Device inventory YAML, saved backup configs |
| **Prompts** | Pre-written instruction cards | "Audit this device", "Generate change report" |

In this chapter, we focus on **Tools** — the most powerful primitive.

---

## 33.2 How MCP Works — Step by Step

Here is what happens when you ask Claude "Back up the config on router 10.0.0.1":

```
Step 1: You type your request in Claude Desktop
 ┌─────────────────────────────────────────┐
 │ "Back up the config on router 10.0.0.1" │
 └────────────────────┬────────────────────┘
 │
Step 2: Claude reads the MCP tool list (your server told Claude
 what tools are available when it connected)
 ┌─────────────────────────────────────────┐
 │ Available tools: │
 │ - send_show_command(device_ip, command) │
 │ - backup_config(device_ip) ◄── │ Claude picks this one!
 │ - send_config_commands(device_ip, cmds) │
 └────────────────────┬────────────────────┘
 │
Step 3: Claude sends a tool call request via MCP protocol
 ┌─────────────────────────────────────────┐
 │ { "tool": "backup_config", │
 │ "arguments": {"device_ip":"10.0.0.1"}}│
 └────────────────────┬────────────────────┘
 │
Step 4: YOUR MCP server receives the request and runs
 the REAL Python function (Netmiko SSH!)
 ┌─────────────────────────────────────────┐
 │ nc = ConnectHandler(**device) │
 │ output = nc.send_command("show run") │
 │ write to backup/rtr1_20260313.cfg │
 │ return "Saved to backup/rtr1_..." │
 └────────────────────┬────────────────────┘
 │
Step 5: Your MCP server sends the result back to Claude
 ┌─────────────────────────────────────────┐
 │ "Config saved to backup/rtr1_20260313 │
 │ .cfg (15,847 bytes)" │
 └────────────────────┬────────────────────┘
 │
Step 6: Claude summarizes in plain English
 ┌─────────────────────────────────────────┐
 │ "I've backed up the running config of │
 │ rtr1 (10.0.0.1). The file is saved at │
 │ backup/rtr1_20260313.cfg (15 KB)." │
 └─────────────────────────────────────────┘
```

---

## 33.3 Installation — Setting Up Your MCP Development Environment

### Step 1: Install uv (the Modern Python Package Manager)

MCP projects use `uv` as the recommended package manager. It is much faster than `pip`.

```bash
# Install uv (macOS/Linux)
curl -LsSf https://astral.sh/uv/install.sh | sh

# Restart your terminal, then verify
uv --version
```

### Step 2: Create Your MCP Server Project

```bash
# Create project directory
mkdir netmiko-mcp-server
cd netmiko-mcp-server

# Initialize a uv project
uv init

# Add dependencies
uv add "mcp[cli]" netmiko python-dotenv pyyaml cisco-support
```

This creates a `pyproject.toml` file (like the one in `cisco_support` from Chapter 31) and installs everything.

### Step 3: Create Your .env File

> **Chapter 19 (Environment variables), Chapter 23 (API credentials), Chapter 32 (secure key handling)**

```bash
cat > .env << 'EOF'
DEVICE_USERNAME=cisco
DEVICE_PASSWORD=cisco
CISCO_CLIENT_ID=your-cisco-api-client-id
CISCO_CLIENT_SECRET=your-cisco-api-client-secret
EOF
```

### Step 4: Create the Device Inventory

> **Chapter 11 (YAML files)**

```yaml
# devices.yaml
---
- hostname: rtr1
 device_type: cisco_ios
 ip: 198.18.1.11
- hostname: rtr2
 device_type: cisco_ios
 ip: 198.18.1.12
```

---

## 33.4 Building the MCP Server — The Complete Code

This is the heart of the project. One single Python file that turns your Netmiko skills into tools that Claude can use.

> **Key MCP concept:** The `@mcp.tool()` decorator turns any Python function into an MCP tool. Claude reads the function name, docstring, and type hints to understand what the tool does. No JSON schemas needed — FastMCP generates them automatically from your Python code.

```python
#!/usr/bin/env python
"""
netmiko_mcp_server.py
An MCP server that gives Claude the ability to manage Cisco network devices.

Run with: uv run netmiko_mcp_server.py
Test with: mcp dev netmiko_mcp_server.py
"""
import os
import json
import yaml
import sys
from datetime import datetime

from mcp.server.fastmcp import FastMCP # The MCP framework
from netmiko import ConnectHandler # Chapter 20 (SSH)
from netmiko import NetmikoAuthenticationException # Chapter 12 (Exceptions)
from netmiko import NetmikoTimeoutException
from dotenv import load_dotenv # Chapter 19 (env vars)

# ── Setup ──────────────────────────────────────────────────────

load_dotenv() # Load .env file

# IMPORTANT: MCP stdio servers must NEVER print to stdout!
# stdout is reserved for the MCP JSON-RPC protocol.
# Use sys.stderr for any debug logging.
def log(msg):
 """Safe logging for MCP stdio servers."""
 print(msg, file=sys.stderr)

# Create the MCP server
# The name "netmiko" is what appears in Claude Desktop
mcp = FastMCP("netmiko")

# Read credentials from environment (Chapter 19)
USERNAME = os.getenv("DEVICE_USERNAME", "cisco")
PASSWORD = os.getenv("DEVICE_PASSWORD", "cisco")


# ── Helper Function ────────────────────────────────────────────

def _connect(device_ip: str, device_type: str = "cisco_ios"):
 """Create a Netmiko SSH connection to a device.

 This is an internal helper — not exposed as an MCP tool.
 It follows the device dictionary pattern from Chapter 5 and Chapter 20.

 """
 device = {
 "device_type": device_type,
 "ip": device_ip,
 "username": USERNAME,
 "password": PASSWORD,
 "timeout": 30,
 }
 return ConnectHandler(**device)


# ══════════════════════════════════════════════════════════════
# TOOL 1: Send Show Commands
# ══════════════════════════════════════════════════════════════

@mcp.tool()
def send_show_command(device_ip: str, command: str,
 device_type: str = "cisco_ios") -> str:
 """SSH to a Cisco device and run a show command.

 Use this for any read-only command like 'show version',
 'show ip route', 'show interfaces', 'show running-config',
 'show ip ospf neighbor', 'show cdp neighbors', etc.

 Args:
 device_ip: The IP address of the network device
 command: The IOS show command to execute
 device_type: Netmiko device type (default: cisco_ios)

 Returns:
 The command output as text, or an error message
 """
 log(f"Tool called: send_show_command({device_ip}, {command})")
 try:
 nc = _connect(device_ip, device_type)
 output = nc.send_command(command)
 nc.disconnect()
 return output
 except NetmikoAuthenticationException:
 return f"ERROR: Authentication failed for {device_ip}. Check credentials."
 except NetmikoTimeoutException:
 return f"ERROR: Connection timed out for {device_ip}. Device may be unreachable."
 except Exception as e:
 return f"ERROR: {str(e)}"


# ══════════════════════════════════════════════════════════════
# TOOL 2: Send Configuration Commands
# ══════════════════════════════════════════════════════════════

@mcp.tool()
def send_config_commands(device_ip: str, commands: list[str],
 device_type: str = "cisco_ios") -> str:
 """SSH to a Cisco device and push configuration commands.

 Automatically enters config mode, sends commands, exits config
 mode, and saves the configuration (write memory).

 Args:
 device_ip: The IP address of the network device
 commands: List of IOS configuration commands to send
 device_type: Netmiko device type (default: cisco_ios)

 Returns:
 The CLI output from the configuration session
 """
 log(f"Tool called: send_config_commands({device_ip}, {commands})")
 try:
 nc = _connect(device_ip, device_type)
 output = nc.send_config_set(commands)
 output += nc.save_config()
 nc.disconnect()
 return output
 except Exception as e:
 return f"ERROR: {str(e)}"


# ══════════════════════════════════════════════════════════════
# TOOL 3: Backup Running Configuration
# ══════════════════════════════════════════════════════════════

@mcp.tool()
def backup_config(device_ip: str,
 device_type: str = "cisco_ios") -> str:
 """Backup the running configuration of a device to a local file.

 Connects via SSH, retrieves the full running-config, and saves
 it to a timestamped file in the backup/ directory.

 Args:
 device_ip: The IP address of the network device
 device_type: Netmiko device type (default: cisco_ios)

 Returns:
 A message with the backup filename and size
 """
 log(f"Tool called: backup_config({device_ip})")
 try:
 nc = _connect(device_ip, device_type)
 hostname = nc.find_prompt()[:-1]
 output = nc.send_command("show running-config")
 nc.disconnect()

 os.makedirs("backup", exist_ok=True)
 timestamp = datetime.now().strftime("%Y%m%d_%H%M%S")
 filename = f"backup/{hostname}_{timestamp}.cfg"

 with open(filename, "w") as f:
 f.write(output)

 return f"Config saved to {filename} ({len(output):,} bytes, {len(output.splitlines())} lines)"
 except Exception as e:
 return f"ERROR: {str(e)}"


# ══════════════════════════════════════════════════════════════
# TOOL 4: Get Structured Device Inventory
# ══════════════════════════════════════════════════════════════

@mcp.tool()
def get_device_inventory(device_ip: str,
 device_type: str = "cisco_ios") -> str:
 """Collect structured inventory from a device via SSH.

 Returns hostname, chassis model, serial number, OS type,
 software version, and uptime in JSON format.

 Args:
 device_ip: The IP address of the network device
 device_type: Netmiko device type (default: cisco_ios)

 Returns:
 JSON string with device inventory details
 """
 log(f"Tool called: get_device_inventory({device_ip})")
 try:
 nc = _connect(device_ip, device_type)
 output = nc.send_command("show version", use_genie=True)
 nc.disconnect()

 if isinstance(output, dict):
 v = output.get("version", {})
 info = {
 "hostname": v.get("hostname", "N/A"),
 "chassis": v.get("chassis", "N/A"),
 "serial_number": v.get("chassis_sn", "N/A"),
 "os_type": v.get("os", "N/A"),
 "software_version": v.get("version", "N/A"),
 "uptime": v.get("uptime", "N/A"),
 }
 return json.dumps(info, indent=2)
 else:
 return f"Structured parsing unavailable. Raw output:\n{str(output)[:1000]}"
 except Exception as e:
 return f"ERROR: {str(e)}"


# ══════════════════════════════════════════════════════════════
# TOOL 5: List All Devices in Inventory
# ══════════════════════════════════════════════════════════════

@mcp.tool()
def list_devices() -> str:
 """List all devices from the YAML inventory file.

 Reads devices.yaml and returns the list of managed devices
 with their hostnames, IPs, and device types.

 Returns:
 JSON string with the device inventory list
 """
 log("Tool called: list_devices()")
 try:
 with open("devices.yaml") as f:
 devices = yaml.safe_load(f)
 return json.dumps(devices, indent=2)
 except FileNotFoundError:
 return "ERROR: devices.yaml not found. Create it first."
 except Exception as e:
 return f"ERROR: {str(e)}"


# ══════════════════════════════════════════════════════════════
# TOOL 6: Check End-of-Life Status (Cisco Support API)
# ══════════════════════════════════════════════════════════════

@mcp.tool()
def check_eol_status(serial_numbers: list[str]) -> str:
 """Check Cisco End-of-Life status for device serial numbers.

 Queries the Cisco Support EoX API to find End-of-Sale and
 End-of-Support dates for the given serial numbers.

 Args:
 serial_numbers: List of Cisco device serial numbers

 Returns:
 JSON string with EoL dates and status for each serial
 """
 log(f"Tool called: check_eol_status({serial_numbers})")
 try:
 from cisco_support import EoX

 client_id = os.getenv("CISCO_CLIENT_ID")
 client_secret = os.getenv("CISCO_CLIENT_SECRET")
 if not client_id or not client_secret:
 return "ERROR: Set CISCO_CLIENT_ID and CISCO_CLIENT_SECRET in .env"

 eox = EoX(client_id=client_id, client_secret=client_secret)
 result = eox.get_by_serial_numbers(serial_numbers)

 records = result.get("EOXRecord", [])
 if not records:
 return "No End-of-Life records found for those serial numbers."

 summary = []
 for rec in records:
 summary.append({
 "serial": rec.get("EOXInputValue", "N/A"),
 "product_id": rec.get("EOLProductID", "N/A"),
 "end_of_sale": rec.get("EndOfSaleDate", {}).get("value", "N/A"),
 "end_of_support": rec.get("LastDateOfSupport", {}).get("value", "N/A"),
 "end_of_vulnerability_support": rec.get("EndOfSecurityVulSupportDate", {}).get("value", "N/A"),
 })
 return json.dumps(summary, indent=2)
 except Exception as e:
 return f"ERROR: {str(e)}"


# ══════════════════════════════════════════════════════════════
# TOOL 7: Check Bug Information (Cisco Support API)
# ══════════════════════════════════════════════════════════════

@mcp.tool()
def check_bugs(bug_ids: list[str]) -> str:
 """Look up Cisco bug details by bug ID.

 Queries the Cisco Support Bug API for details about specific
 bugs (e.g., CSCxx12345).

 Args:
 bug_ids: List of Cisco bug IDs (e.g., ["CSCab12345"])

 Returns:
 JSON string with bug headline, severity, status
 """
 log(f"Tool called: check_bugs({bug_ids})")
 try:
 from cisco_support import Bug

 client_id = os.getenv("CISCO_CLIENT_ID")
 client_secret = os.getenv("CISCO_CLIENT_SECRET")
 if not client_id or not client_secret:
 return "ERROR: Set CISCO_CLIENT_ID and CISCO_CLIENT_SECRET in .env"

 bug = Bug(client_id=client_id, client_secret=client_secret)
 result = bug.get_by_ids(bug_ids)

 bugs = result.get("bugs", [])
 summary = []
 for b in bugs:
 summary.append({
 "bug_id": b.get("bug_id"),
 "headline": b.get("headline"),
 "severity": b.get("severity"),
 "status": b.get("status"),
 "product": b.get("product"),
 "description": b.get("description", "")[:200],
 })
 return json.dumps(summary, indent=2)
 except Exception as e:
 return f"ERROR: {str(e)}"


# ══════════════════════════════════════════════════════════════
# START THE SERVER
# ══════════════════════════════════════════════════════════════

if __name__ == "__main__":
 mcp.run()
```

### How FastMCP Automates Everything

Notice there are **no JSON schemas** anywhere in this code. Compare this to Chapter 32 where you had to write 150+ lines of JSON tool definitions. FastMCP reads your Python and generates all of that automatically:

```
Your Python: What FastMCP generates for Claude:
───────────── ─────────────────────────────────
def send_show_command( → Tool name: "send_show_command"
 device_ip: str, → Parameter: device_ip (string, required)
 command: str, → Parameter: command (string, required)
 device_type: str = "cisco_ios" → Parameter: device_type (string, default)
) -> str: → Returns: string
 """SSH to a Cisco device and → Description: "SSH to a Cisco device
 run a show command...""" and run a show command..."
```

> **Note (Chapter 9):** Docstrings are used to document function purpose.

FastMCP uses Python's `inspect` module to read your function signature, type hints, and docstring — and automatically creates the MCP tool schema. This is why good docstrings (Chapter 9) and type hints matter.

---

## 33.5 Testing Your MCP Server

### Test 1: Run with the MCP Inspector

The MCP Inspector is a web-based debugging tool that lets you call your tools manually.

```bash
# Start the inspector (opens a browser)
mcp dev netmiko_mcp_server.py
```

This opens a web interface where you can see all your tools listed, call them with test parameters, and see the results.

### Test 2: Run from the Command Line

```bash
# Run the server directly (stdio mode)
uv run netmiko_mcp_server.py
```

The server starts and waits for MCP JSON-RPC messages on stdin. You would not normally interact with it directly — Claude Desktop does that for you.

---

## 33.6 Connecting to Claude Desktop

### Step 1: Find Your Claude Desktop Config File

| Operating System | Config File Location |
|---|---|
| macOS | `~/Library/Application Support/Claude/claude_desktop_config.json` |
| Windows | `%APPDATA%\Claude\claude_desktop_config.json` |
| Linux | `~/.config/Claude/claude_desktop_config.json` |

### Step 2: Add Your MCP Server

Open the config file and add your server. Replace the paths with your actual absolute paths:

```json
{
 "mcpServers": {
 "netmiko": {
 "command": "uv",
 "args": [
 "--directory",
 "/home/youruser/netmiko-mcp-server",
 "run",
 "netmiko_mcp_server.py"
 ],
 "env": {
 "DEVICE_USERNAME": "cisco",
 "DEVICE_PASSWORD": "cisco",
 "CISCO_CLIENT_ID": "your-client-id",
 "CISCO_CLIENT_SECRET": "your-client-secret"
 }
 }
 }
}
```

**Important notes:**
- Use **absolute paths** (start with `/` on Linux/macOS or `C:\` on Windows).
- The `env` block passes secrets to your server securely — they never appear in your code.
- On Windows, use forward slashes or double backslashes in paths.

### Step 3: Restart Claude Desktop

Close Claude Desktop completely and reopen it. You should see a small hammer icon indicating MCP tools are available.

---

## 33.7 Using It — Real Conversation Examples with Claude

Once connected, you talk to Claude normally. Claude will recognize when to use your network tools based on your request.

### Use Case 1: Device Discovery

**You:** "List all my managed devices"

**Claude calls:** `list_devices()`

**Claude responds:** "You have 2 managed devices: rtr1 at 198.18.1.11 (Cisco IOS) and rtr2 at 198.18.1.12 (Cisco IOS)."

### Use Case 2: Collecting Show Commands (Chapter 21, Script 1)

**You:** "Show me the OSPF neighbors on 198.18.1.11"

**Claude calls:** `send_show_command(device_ip="198.18.1.11", command="show ip ospf neighbor")`

**Claude responds:** "Router 198.18.1.11 has one OSPF neighbor: 10.0.0.2 on GigabitEthernet2, in FULL state. The adjacency has been up for 3 days."

### Use Case 3: Configuration Backup (Chapter 22, Script 8)

**You:** "Back up the configs on both routers"

**Claude calls:** `backup_config(device_ip="198.18.1.11")` then `backup_config(device_ip="198.18.1.12")`

**Claude responds:** "Both configs backed up successfully. rtr1: saved to backup/rtr1_20260313_143022.cfg (15,847 bytes). rtr2: saved to backup/rtr2_20260313_143025.cfg (14,233 bytes)."

### Use Case 4: Pushing Config Changes (Chapter 22, Script 5)

**You:** "Add NTP server 10.1.1.4 and SNMP community 'netauto_ro' read-only to both routers"

**Claude calls:**
```
send_config_commands(device_ip="198.18.1.11",
 commands=["ntp server 10.1.1.4", "snmp-server community netauto_ro RO"])
send_config_commands(device_ip="198.18.1.12",
 commands=["ntp server 10.1.1.4", "snmp-server community netauto_ro RO"])
```

**Claude responds:** "NTP and SNMP configured on both routers. Changes have been saved to startup config."

### Use Case 5: Inventory Report (Chapter 30, Script 10)

**You:** "Get me a full inventory of all devices with serial numbers"

**Claude calls:** `get_device_inventory("198.18.1.11")` then `get_device_inventory("198.18.1.12")`

**Claude responds with a table:**

| Hostname | Chassis | Serial | OS | Version | Uptime |
|---|---|---|---|---|---|
| rtr1 | CSR1000V | 9ABC1234 | iosxe | 17.3.4a | 3 days |
| rtr2 | CSR1000V | 9DEF5678 | iosxe | 17.3.4a | 5 days |

### Use Case 6: End-of-Life Check (Chapter 31)

**You:** "Check if any of these devices are end-of-life: serial numbers 9ABC1234 and 9DEF5678"

**Claude calls:** `check_eol_status(serial_numbers=["9ABC1234", "9DEF5678"])`

**Claude responds:** "Both devices have the following EoL status: End-of-Sale was October 2022, but End-of-Support is not until October 2027. You have approximately 18 months of remaining vendor support. I recommend starting a hardware refresh plan."

### Use Case 7: Combined Workflow — The Ultimate Test

**You:** "Do a complete audit of rtr1: back up the config, collect the inventory, check EoL status, and look for any OSPF issues."

Claude automatically chains multiple tool calls together and gives you a comprehensive report combining all the data.

---

## 33.8 Complete Project Structure

```
netmiko-mcp-server/
├── .env ← Credentials (Chapter 19 — never commit!)
├── .gitignore ← Excludes .env, backup/, __pycache__
├── pyproject.toml ← Project metadata (Chapter 29, Chapter 31)
├── devices.yaml ← Device inventory (Chapter 11)
├── netmiko_mcp_server.py ← The MCP server (THIS CHAPTER)
└── backup/ ← Config backups land here (Chapter 10)
 ├── rtr1_20260313_143022.cfg
 └── rtr2_20260313_143025.cfg
```

---

## 33.9 MCP vs OpenAI Function Calling — Comparison

| Feature | Chapter 32 (OpenAI Agent) | Chapter 33 (MCP Server) |
|---|---|---|
| AI Provider | OpenAI (GPT-4o) | Claude (Anthropic) |
| Connection method | API calls from your script | Claude Desktop connects to your server |
| Tool definitions | Manual JSON schemas (150+ lines) | Auto-generated from Python type hints |
| Where code runs | Your script manages the loop | MCP framework manages everything |
| Cost | OpenAI API charges per token | Claude Desktop (included with subscription) |
| Setup complexity | Write the full agent loop | Write functions, add `@mcp.tool()` |
| Multi-user | Single user per script | Multiple Claude instances can connect |

---

## 33.10 Concept Map — Every Chapter Reference in This Project

| Component | Book/Chapter Reference |
|---|---|
| `uv` and `pyproject.toml` | Chapter 1 (Setup), Chapter 29 (Project structure), Chapter 31 (cisco_support) |
| `.env` + `load_dotenv()` | Chapter 19 (OS), Chapter 23 (APIs), KByers `gaia_auth.py` |
| `devices.yaml` | Chapter 11 (YAML), Chapter 11 |
| `_connect()` helper | Chapter 9 (Functions), Chapter 20 (Netmiko), Netmiko Course class1 |
| `ConnectHandler(**device)` | Chapter 5 (Dicts), Chapter 9 (kwargs), Chapter 20 |
| `try/except` blocks | Chapter 12, Script 5 |
| `nc.send_command()` | Chapter 21, Script 1 |
| `nc.send_config_set()` | Chapter 22, Script 2–6 |
| `nc.find_prompt()[:-1]` | Chapter 3 (Slicing), Script 8 |
| `os.makedirs()` | Chapter 19, Script 8 |
| `with open() as f:` | Chapter 10, Chapter 10 |
| `use_genie=True` | Chapter 26, Script 9–10 |
| `json.dumps()` | Chapter 11, Chapter 11 |
| `yaml.safe_load()` | Chapter 11, KByers class1/files |
| `from cisco_support import EoX` | Chapter 31, cisco_support package |
| Docstrings and type hints | Chapter 9 (Functions), Chapter 9 |
| `if __name__ == "__main__"` | Chapter 13 (Modules) |
| `@mcp.tool()` decorator | New (Chapter 33) — the MCP magic |
| `mcp.run()` | New (Chapter 33) — starts the server |

---

## 33.11 Chapter 33 Lab Tasks

**Task 33.1 — Build and Test:**
Set up the complete MCP server project. Install `uv`, create the project, add all dependencies, create `.env` and `devices.yaml`. Run `mcp dev netmiko_mcp_server.py` and verify all 7 tools appear in the inspector. Call `list_devices` from the inspector to confirm it reads your YAML.

**Task 33.2 — Connect to Claude Desktop:**
Configure your Claude Desktop `claude_desktop_config.json` to connect to your MCP server. Restart Claude and verify the hammer icon appears. Ask Claude "What tools do you have for network management?" and confirm it lists your tools.

**Task 33.3 — Add a New Tool:**
Add an 8th tool called `get_interface_status` that runs `show ip interface brief` on a device and returns the output. Use the `@mcp.tool()` decorator with a full docstring and type hints. Test it from Claude by asking "Show me the interface status on 198.18.1.11."

**Task 33.4 — Add an MCP Resource:**
Add a resource that lets Claude read the contents of any backup config file. Use the `@mcp.resource()` decorator. Example: `@mcp.resource("backup://{filename}")` should return the file contents when Claude requests a specific backup.

**Task 33.5 — Full Audit Workflow:**
Connect to Claude Desktop and perform this complete workflow in a single conversation:
1. "List my devices"
2. "Back up configs on all devices"
3. "Get inventory for each device"
4. "Check EoL status for all serial numbers you found"
5. "Create a summary report of everything"

Document the entire conversation, noting which tools Claude called at each step and how it chained them together. This exercise demonstrates the power of MCP: you gave Claude one set of tools, and it orchestrated a complex multi-step workflow autonomously.

---

## Appendix A (continued): Chapter 33 Answers

**33.3:**
```python
@mcp.tool()
def get_interface_status(device_ip: str,
 device_type: str = "cisco_ios") -> str:
 """Get the interface status table from a device.

 Runs 'show ip interface brief' and returns the output showing
 all interfaces with their IP addresses, status, and protocol.

 Args:
 device_ip: The IP address of the network device
 device_type: Netmiko device type (default: cisco_ios)

 Returns:
 The interface status table as text
 """
 log(f"Tool called: get_interface_status({device_ip})")
 try:
 nc = _connect(device_ip, device_type)
 output = nc.send_command("show ip interface brief")
 nc.disconnect()
 return output
 except Exception as e:
 return f"ERROR: {str(e)}"
```

**33.4:**
```python
@mcp.resource("backup://{filename}")
def read_backup_file(filename: str) -> str:
 """Read the contents of a backup configuration file.

 Args:
 filename: Name of the backup file (e.g., rtr1_20260313_143022.cfg)

 Returns:
 The full contents of the backup file
 """
 filepath = f"backup/{filename}"
 if not os.path.exists(filepath):
 return f"ERROR: File {filepath} not found."
 with open(filepath) as f:
 return f.read()
```

---

*End of Lab Guide*


**Total Chapters:** 33 + Appendix | **Total Lab Tasks:** 170 with answers