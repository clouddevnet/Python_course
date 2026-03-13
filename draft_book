# MASTER PYTHON STUDY GUIDE
## From Zero to Network Automation Expert

### A Comprehensive Learning Path Combining Three Authoritative Sources

---

| Source | Author | Focus |
|--------|--------|-------|
| **Python Crash Course, 3rd Edition** | Eric Matthes | General Python fundamentals, projects |
| **PyNEng – Python for Network Engineers** | Natasha Samoylenko | Python with Cisco networking focus |
| **Kirk Byers / Twin Bridges Technology** | Kirk Byers (CCIE #6243) | Netmiko, network automation training |

**Course Repository:** `github.com/twin-bridges/python_course_mar26`

---

> *"I have taken several paid and non-paid Python courses. I can say that by far your course is the best one I have taken."* — Kirk Byers course student review

---

## How To Use This Guide

This guide is structured as **20 progressive modules**. Each module:

1. **Explains concepts in plain language** with analogies network engineers understand
2. **Shows code examples** from all three sources with network-relevant context
3. **Provides step-by-step walkthroughs** you can type along with
4. **Includes practice questions** to test your understanding
5. **Contains homework scripts** you can modify and extend

**Color-coded source references throughout:**
- 🟢 **PCC** = Python Crash Course concept
- 🔴 **PyNEng** = Python for Network Engineers concept  
- 🟣 **Byers** = Kirk Byers / Twin Bridges course concept

---

## Complete Table of Contents

### Part I: Python Foundations (Modules 1–7)
- [Module 1: Environment Setup, Tools & Git](#module-1-environment-setup-tools--git)
- [Module 2: Variables, Strings & Numbers](#module-2-variables-strings--numbers)
- [Module 3: Lists & Tuples](#module-3-lists--tuples)
- [Module 4: Dictionaries & Sets](#module-4-dictionaries--sets)
- [Module 5: If Statements & Conditional Logic](#module-5-if-statements--conditional-logic)
- [Module 6: Loops – for and while](#module-6-loops--for-and-while)
- [Module 7: Comprehensions & Built-in Functions](#module-7-comprehensions--built-in-functions)

### Part II: Code Organization (Modules 8–10)
- [Module 8: Functions](#module-8-functions)
- [Module 9: Modules & the Standard Library](#module-9-modules--the-standard-library)
- [Module 10: File Input/Output & Exceptions](#module-10-file-inputoutput--exceptions)

### Part III: Data Processing (Modules 11–12)
- [Module 11: Regular Expressions](#module-11-regular-expressions)
- [Module 12: Data Formats – CSV, JSON & YAML](#module-12-data-formats--csv-json--yaml)

### Part IV: Object-Oriented Programming (Modules 13–14)
- [Module 13: Classes & OOP](#module-13-classes--oop)
- [Module 14: Testing Your Code with Pytest](#module-14-testing-your-code-with-pytest)

### Part V: Network Automation (Modules 15–19)
- [Module 15: SSH/Telnet – Netmiko, Paramiko & Scrapli](#module-15-sshtelnet--netmiko-paramiko--scrapli)
- [Module 16: Concurrent Connections to Multiple Devices](#module-16-concurrent-connections-to-multiple-devices)
- [Module 17: Jinja2 Configuration Templates](#module-17-jinja2-configuration-templates)
- [Module 18: TextFSM & Output Parsing](#module-18-textfsm--output-parsing)
- [Module 19: Databases with SQLite](#module-19-databases-with-sqlite)

### Part VI: Capstone & Reference
- [Module 20: Capstone Projects, Practice Exam & Resources](#module-20-capstone-projects-practice-exam--resources)

---

## Learning Roadmap – Cross-Reference Map

| Module | Topic | PCC Chapter | PyNEng Chapter | Kirk Byers Week |
|--------|-------|-------------|----------------|-----------------|
| 1 | Environment Setup & Git | Ch 1, Appendix A-C | Ch 1–3 | Free Wk1 |
| 2 | Variables, Strings & Numbers | Ch 2 | Ch 3–4 (Strings) | Free Wk1, LP Wk1 |
| 3 | Lists & Tuples | Ch 3–4 | Ch 4 (Lists/Tuples) | Free Wk2, LP Wk2 |
| 4 | Dictionaries & Sets | Ch 6 | Ch 4 (Dicts/Sets) | Free Wk4, LP Wk4 |
| 5 | If Statements | Ch 5 | Ch 6 | LP Wk3 |
| 6 | Loops (for & while) | Ch 4 (range), Ch 7 | Ch 7 | LP Wk3 |
| 7 | Comprehensions & Useful Functions | Ch 4 (comprehensions) | Ch 8, 10 | LP Wk3 |
| 8 | Functions | Ch 8 | Ch 9 | LP Wk5 |
| 9 | Modules & Standard Library | Ch 8 (imports) | Ch 11–12 | LP Wk8 |
| 10 | File I/O & Exceptions | Ch 10 | Ch 16 | LP Wk2 |
| 11 | Regular Expressions | — | Ch 14–15 | LP Wk4 |
| 12 | CSV, JSON & YAML | Ch 10 (JSON) | Ch 17 | LP Wk7 |
| 13 | Classes & OOP | Ch 9 | Ch 23–25 | — |
| 14 | Testing Your Code | Ch 11 | — | — |
| 15 | SSH/Telnet: Netmiko & Paramiko | — | Ch 18 | LP Wk6, Netmiko Wk1–6 |
| 16 | Concurrent Connections | — | Ch 19 | Paid Wk7 |
| 17 | Jinja2 Templates | — | Ch 20 | LP Wk7 |
| 18 | TextFSM & Parsing | — | Ch 21–22 | Paid Wk5 |
| 19 | Databases (SQLite) | — | Ch 26–27 | — |
| 20 | Capstone Projects | Part II Projects | — | Full Course |

**Legend:** PCC = Python Crash Course 3rd Ed | PyNEng = pyneng.readthedocs.io | LP = Kirk Byers Learning Python (8-week paid course) | Free = Kirk Byers Free 10-week course | Netmiko = Netmiko By Example 6-week course

---

# PART I: PYTHON FOUNDATIONS

---

# Module 1: Environment Setup, Tools & Git

> 📚 **Sources:** PCC Ch 1 + Appendix A-C | PyNEng Ch 1–3 | Byers Free Course Wk1

## Why This Module Matters

Before writing a single line of Python, you need a properly configured environment. This is the step most self-taught programmers rush through, and it causes endless frustration later. All three of our source materials emphasize that getting setup right saves hours of debugging.

**What you'll learn:**
- How to install Python on any operating system
- What virtual environments are and why they're non-negotiable
- How to use IPython for interactive exploration
- Git fundamentals for version-controlling your automation scripts
- Choosing and configuring a code editor

---

## 1.1 Installing Python

### PCC Approach (Ch 1)
Python Crash Course walks through installation on Windows, macOS, and Linux. The book recommends Python 3.11 or later and emphasizes checking the "Add Python to PATH" checkbox on Windows, which is the most common source of installation issues.

### PyNEng Approach (Ch 1)
PyNEng uses Debian Linux exclusively and recommends Python 3.7+. For network engineers, Linux is the preferred platform because most network automation tools (Ansible, Nornir, Netmiko) are developed and tested on Linux first.

### Byers Approach
Kirk Byers' courses provide pre-built AWS Linux lab environments with Python already configured. His free course expects you to set up your own environment.

### Step-by-Step Installation

**On Ubuntu/Debian (Recommended for Network Automation):**

```bash
# Update package lists
sudo apt update

# Install Python 3, pip, venv, and essential build tools
sudo apt install -y python3 python3-pip python3-venv python3-dev git

# Verify installation
python3 --version
# Output: Python 3.10.12 (or similar)

pip3 --version
# Output: pip 22.0.2 from /usr/lib/python3/dist-packages/pip (python 3.10)
```

**On Windows:**

1. Download Python from [python.org](https://python.org)
2. **CRITICAL:** Check "Add Python 3.x to PATH" during installation
3. Open Command Prompt and verify:

```powershell
python --version
pip --version
```

**On macOS:**

```bash
# Install Homebrew first (if not installed)
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Install Python
brew install python3

# Verify
python3 --version
```

### Understanding What Got Installed

When you install Python, you get several things:

| Component | What It Is | Analogy for Network Engineers |
|-----------|-----------|-------------------------------|
| `python3` | The Python interpreter | Like the IOS CLI — it reads and executes your commands |
| `pip3` | Package installer | Like installing IOS features with `install add` |
| Standard Library | Built-in modules | Like the default IOS feature set |
| `venv` | Virtual environment tool | Like VRFs — isolated environments that don't interfere |

---

## 1.2 Virtual Environments

### Why Virtual Environments Are Non-Negotiable

Think of virtual environments like VRFs (Virtual Routing and Forwarding) on a Cisco router. Just as VRFs keep routing tables separate so one customer's routes don't interfere with another's, virtual environments keep Python package installations separate so one project's dependencies don't break another project.

**Without virtual environments:**
- Project A needs `netmiko==4.0`
- Project B needs `netmiko==3.0`
- Both install to the same global location → conflict!

**With virtual environments:**
- Project A's venv has `netmiko==4.0`
- Project B's venv has `netmiko==3.0`
- No conflict, both work perfectly

### Creating and Using Virtual Environments

```bash
# Step 1: Create a virtual environment named 'netauto'
python3 -m venv ~/netauto-env

# What just happened?
# Python created a directory structure:
# ~/netauto-env/
# ├── bin/           # Scripts (activate, python, pip)
# ├── include/       # C headers (for compiling packages)
# ├── lib/           # Installed packages go here
# └── pyvenv.cfg     # Configuration file

# Step 2: Activate the virtual environment
source ~/netauto-env/bin/activate    # Linux/macOS
# netauto-env\Scripts\activate       # Windows

# Your prompt changes to show the active venv:
# (netauto-env) user@host:~$

# Step 3: Install packages (they go into the venv, not globally)
pip install netmiko paramiko napalm
pip install jinja2 pyyaml textfsm
pip install ipython pytest rich tabulate

# Step 4: Verify packages are installed
pip list

# Step 5: Save your requirements (for reproducibility)
pip freeze > requirements.txt

# Step 6: Deactivate when done
deactivate

# Later, recreate the same environment anywhere:
pip install -r requirements.txt
```

### The Network Automation Starter Package

Here's the recommended set of packages for a Cisco-focused automation environment:

| Package | Purpose | Used In |
|---------|---------|---------|
| `netmiko` | SSH to network devices (simplifies paramiko) | PyNEng Ch18, Byers entire course |
| `paramiko` | Low-level SSH library | PyNEng Ch18 |
| `napalm` | Multi-vendor abstraction layer | Byers paid course |
| `jinja2` | Configuration templates | PyNEng Ch20, Byers Wk7 |
| `pyyaml` | Read/write YAML files | PyNEng Ch17, Byers Wk7 |
| `textfsm` | Parse CLI output to structured data | PyNEng Ch21, Byers paid course |
| `ntc-templates` | Pre-built TextFSM templates | Byers Netmiko course |
| `ipython` | Enhanced interactive Python shell | PyNEng Ch3, Byers all courses |
| `rich` | Beautiful terminal output | Modern best practice |
| `pytest` | Testing framework | PCC Ch11 |
| `netaddr` | IP address manipulation | Network-specific |

---

## 1.3 The Python Interpreter & IPython

### The Standard Python Interpreter (PCC Ch 1)

PCC introduces the Python interpreter as your first interaction with Python:

```python
$ python3
Python 3.11.0 (main, Oct 24 2022, 18:26:48)
>>> print("Hello, World!")
Hello, World!
>>> 2 + 3
5
>>> exit()
```

### IPython – The Network Engineer's Best Friend (PyNEng Ch 3 + Byers)

Both PyNEng and Kirk Byers strongly recommend IPython over the standard interpreter. Here's why:

```python
$ ipython

In [1]: # Feature 1: Tab completion
In [1]: hostname = 'R1-CORE-SWITCH'
In [2]: hostname.   # Press Tab here!
# Shows ALL available string methods:
# hostname.capitalize  hostname.center    hostname.count
# hostname.encode      hostname.endswith  hostname.find
# hostname.format      ...

In [3]: # Feature 2: ? for documentation
In [3]: hostname.startswith?
# Signature: hostname.startswith(prefix, start=0, end=9223372036854775807)
# Docstring: Return True if S starts with the specified prefix...

In [4]: # Feature 3: ! for shell commands
In [4]: !ping -c 2 10.1.1.1
# PING 10.1.1.1 (10.1.1.1) 56(84) bytes of data...

In [5]: # Feature 4: %history to see what you typed
In [5]: %history

In [6]: # Feature 5: Syntax highlighting and auto-indent
In [6]: for i in range(3):
   ...:     print(f"Interface GigabitEthernet0/{i}")
   ...:
Interface GigabitEthernet0/0
Interface GigabitEthernet0/1
Interface GigabitEthernet0/2

In [7]: # Feature 6: %timeit for performance testing
In [7]: %timeit [x**2 for x in range(1000)]
# 62.5 µs ± 1.23 µs per loop
```

### When to Use the Interpreter vs. Scripts

| Situation | Use Interpreter | Use Script (.py file) |
|-----------|----------------|----------------------|
| Testing a quick idea | ✅ | |
| Exploring a data structure | ✅ | |
| Running a one-time command | ✅ | |
| Automating a repeatable task | | ✅ |
| Building a tool others will use | | ✅ |
| Working with multiple files | | ✅ |
| Anything you want to save | | ✅ |

---

## 1.4 Choosing a Code Editor

### PCC Recommendation
Python Crash Course recommends VS Code (Visual Studio Code) as the primary editor, with Sublime Text as an alternative.

### PyNEng Recommendation
PyNEng recommends Mu editor for absolute beginners and VS Code for everyone else. The book notes that PyCharm is powerful but can be overwhelming for beginners.

### Byers Recommendation
Kirk Byers' courses use vim/nano on Linux lab servers, but recommend VS Code for local development.

### VS Code Setup for Network Automation

```
Essential VS Code Extensions:
1. Python (Microsoft)           - IntelliSense, debugging, linting
2. Pylance                      - Advanced type checking
3. GitLens                      - Git integration
4. YAML                         - YAML syntax highlighting
5. Jinja                        - Jinja2 template highlighting
6. Remote - SSH                 - Edit files on remote servers
7. Cisco IOS Syntax             - Highlight Cisco configs
```

---

## 1.5 Git for Network Engineers

### Why Network Engineers Need Git (PCC Cheat Sheet + PyNEng Ch 2 + Byers Git Course)

Git is version control for your code, just like RANCID or Oxidized is version control for your router configs. But Git is far more powerful:

| Traditional Config Backup | Git-Based Approach |
|--------------------------|-------------------|
| Save config to TFTP | Commit changes with descriptive messages |
| Filename: `router1_20240101.cfg` | Git tracks WHO changed WHAT and WHEN |
| No easy way to compare versions | `git diff` shows exact changes |
| No way to undo a specific change | `git revert` undoes any specific commit |
| No collaboration features | Branches, pull requests, code review |

### Git Essentials – Step by Step

```bash
# ---- First-time Git configuration ----
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git config --global core.editor "nano"    # or "code --wait" for VS Code

# ---- Starting a new project ----
mkdir cisco-automation
cd cisco-automation
git init
# Output: Initialized empty Git repository in .../cisco-automation/.git/

# ---- Create essential files ----
# .gitignore - CRITICAL for security
cat > .gitignore << 'EOF'
# Python
__pycache__/
*.pyc
*.pyo
venv/
*.egg-info/

# Security - NEVER commit these!
.env
*.key
*password*
*secret*
credentials.yaml

# OS files
.DS_Store
Thumbs.db

# IDE
.vscode/
.idea/
EOF

# Create a README
cat > README.md << 'EOF'
# Cisco Automation Scripts
Network automation tools using Python and Netmiko.
EOF

# ---- Your first commit ----
git add .                    # Stage all files
git status                   # Review what will be committed
git commit -m "Initial project structure with .gitignore"

# ---- Making changes and committing ----
# ... edit some files ...
git add .
git commit -m "Add VLAN configuration script"

# ---- Viewing history ----
git log                      # Full history
git log --oneline            # Compact history
git diff                     # See uncommitted changes
git diff HEAD~1              # Compare with previous commit

# ---- Branching (for new features) ----
git checkout -b feature/vlan-audit   # Create and switch to new branch
# ... do work ...
git add . && git commit -m "Add VLAN audit functionality"
git checkout main                     # Switch back to main
git merge feature/vlan-audit          # Merge the feature in
git branch -d feature/vlan-audit      # Delete the branch

# ---- Working with GitHub ----
git remote add origin https://github.com/yourusername/cisco-automation.git
git push -u origin main
```

### Cloning Kirk Byers' Course Repository

```bash
# Clone the course exercises
git clone https://github.com/twin-bridges/python_course_mar26
cd python_course_mar26
ls
# You'll see weekly lesson directories with exercises
```

---

## Module 1 Practice Questions

**Q1.1:** What is the command to create a virtual environment named `lab-env` and activate it on Linux?

```bash
# Answer:
python3 -m venv lab-env
source lab-env/bin/activate
```

**Q1.2:** Why should you NEVER commit passwords or API keys to Git? What file prevents this?

```
Answer: If pushed to GitHub (even briefly), credentials can be found by bots
that scan public repositories. The .gitignore file prevents specified files
from being tracked by Git. Always use environment variables or separate
credential files listed in .gitignore.
```

**Q1.3:** What are three advantages of IPython over the standard Python interpreter?

```
Answer:
1. Tab completion - shows available methods on any object
2. ? help system - quick documentation without leaving the shell
3. Syntax highlighting and auto-indentation - easier to read code
(Also: %timeit, !shell commands, %history, better error messages)
```

**Q1.4 Homework Script:** Create a new Git repository called `network-scripts`, add a `.gitignore` that excludes Python cache files and any file containing "password", create a README.md, and make your first commit.

---

# Module 2: Variables, Strings & Numbers

> 📚 **Sources:** PCC Ch 2 | PyNEng Ch 3–4 (Strings/Numbers) | Byers Free Wk1-2, LP Wk1

## Why This Module Matters

**Everything in network automation is a string.** Every command you send to a router is a string. Every line of output you receive is a string. Every configuration file is made of strings. IP addresses, hostnames, interface names, VLAN numbers stored in configs — all strings initially.

Understanding how to create, manipulate, search, and transform strings is the single most important Python skill for a network engineer. Kirk Byers' students consistently report that the string manipulation lessons are where they first see how Python applies to their daily work.

---

## 2.1 Variables – Labels for Your Data

### The PCC Explanation (Ch 2)
Python Crash Course explains variables as "labels" that point to values. Unlike some languages, you don't need to declare variable types — Python figures it out automatically.

### The Network Engineer Mental Model
Think of variables like the `hostname` command on a Cisco device. When you type `hostname R1-CORE`, you're assigning the label "hostname" to the value "R1-CORE". In Python:

```python
# This is exactly the same concept
hostname = 'R1-CORE'
```

### Variable Assignment – The Basics

```python
# Simple assignment (PCC Ch 2 style)
message = "Hello, Python world!"
print(message)
# Output: Hello, Python world!

# Network-focused assignment (PyNEng + Byers style)
hostname = 'SW-ACCESS-01'
mgmt_ip = '10.255.0.1'
vlan_id = 100
ssh_port = 22
is_reachable = True
cpu_utilization = 45.7

# Multiple assignment on one line (PyNEng technique)
host, ip, platform = 'R1', '10.0.0.1', 'cisco_ios'

# Constants (convention: ALL_CAPS) — PCC Ch 2
MAX_VLANS = 4094
SSH_TIMEOUT = 30
DEFAULT_USERNAME = 'admin'
```

### Variable Naming Rules and Conventions

All three sources agree on Python naming conventions:

```python
# ✅ GOOD variable names (snake_case)
device_hostname = 'R1'
interface_name = 'GigabitEthernet0/1'
vlan_list = [10, 20, 30]
is_connected = True
max_retry_count = 3

# ❌ BAD variable names
DeviceHostname = 'R1'    # This is for class names (CamelCase)
DEVICE_HOSTNAME = 'R1'   # This is for constants
x = 'R1'                 # Not descriptive
1st_device = 'R1'        # Can't start with a number
my-device = 'R1'         # Hyphens not allowed (use underscores)

# ❌ RESERVED WORDS (can't use as variable names)
# print, list, dict, type, str, int, for, if, while, class, def, return...
```

### Understanding Data Types

```python
# Python has several built-in data types
hostname = 'R1-CORE'        # str (string)
vlan_id = 100                # int (integer)
cpu_load = 45.7              # float (decimal number)
is_up = True                 # bool (boolean: True/False)
interfaces = ['Gi0/0']      # list (ordered, mutable collection)
device_info = {'ip': '10.1.1.1'}  # dict (key-value pairs)
connection = ('10.1.1.1', 22)     # tuple (ordered, immutable)
unique_vlans = {10, 20, 30}       # set (unique values only)

# Check the type of any variable
print(type(hostname))    # <class 'str'>
print(type(vlan_id))     # <class 'int'>
print(type(cpu_load))    # <class 'float'>
print(type(is_up))       # <class 'bool'>
```

---

## 2.2 Strings – The Network Engineer's Primary Data Type

### Creating Strings

```python
# Single quotes (most common in network scripts)
intf = 'GigabitEthernet0/1'

# Double quotes (use when string contains single quote)
description = "Mike's workstation"

# Triple quotes for multiline strings (perfect for configs!)
router_config = '''
hostname R1-CORE
!
interface GigabitEthernet0/0
 description WAN Uplink to ISP
 ip address 203.0.113.1 255.255.255.252
 no shutdown
!
interface GigabitEthernet0/1
 description LAN - User Network
 ip address 10.1.0.1 255.255.255.0
 no shutdown
!
router ospf 1
 network 10.0.0.0 0.255.255.255 area 0
 network 203.0.113.0 0.0.0.3 area 0
'''

# Raw strings (the r prefix) - for regex patterns
# Backslashes are treated literally, not as escape characters
ip_regex = r'\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}'
# Without r: you'd need '\\d{1,3}\\.\\d{1,3}...' — messy!
```

### String Indexing and Slicing

Strings are sequences of characters, and you can access individual characters or substrings using indexing:

```python
interface = 'GigabitEthernet0/1'

# Positive indexing (from the start, starting at 0)
print(interface[0])     # 'G'
print(interface[1])     # 'i'
print(interface[7])     # 'E'

# Negative indexing (from the end)
print(interface[-1])    # '1'
print(interface[-3])    # '0'

# Slicing [start:end] — end is EXCLUSIVE
print(interface[0:7])    # 'Gigabit'
print(interface[7:15])   # 'Ethernet'
print(interface[:7])     # 'Gigabit' (start from beginning)
print(interface[15:])    # '0/1' (go to end)
print(interface[-3:])    # '0/1' (last 3 characters)

# Step slicing [start:end:step]
print(interface[::2])    # 'GgbtEhre/'  (every other char)
print(interface[::-1])   # '1/0tenrehtEtibagiG' (reversed!)
```

### Essential String Methods – Complete Guide

This is the most important section for network engineers. Every method below will be used repeatedly in your automation scripts:

#### Searching and Testing Methods

```python
line = '  interface GigabitEthernet0/1  '

# strip() – Remove whitespace from both ends
clean = line.strip()
print(f"'{clean}'")   # 'interface GigabitEthernet0/1'

# lstrip() / rstrip() – Remove from left/right only
print(line.lstrip())  # 'interface GigabitEthernet0/1  '
print(line.rstrip())  # '  interface GigabitEthernet0/1'

# startswith() – Does string begin with this prefix?
print(clean.startswith('interface'))  # True
print(clean.startswith('router'))    # False

# endswith() – Does string end with this suffix?
filename = 'running_config.cfg'
print(filename.endswith('.cfg'))  # True
print(filename.endswith('.txt'))  # False

# find() – Where does a substring first appear? (-1 if not found)
config_line = 'ip address 10.1.1.1 255.255.255.0'
pos = config_line.find('10.1.1.1')
print(pos)  # 11

# count() – How many times does a substring appear?
show_output = 'up up down up up down up'
print(show_output.count('up'))    # 5
print(show_output.count('down'))  # 2

# in / not in – Membership testing (not a method, but essential)
if 'up' in show_output:
    print("At least one interface is up")
if 'error' not in show_output:
    print("No errors found")
```

#### Transformation Methods

```python
hostname = 'r1-core-switch'

# upper() / lower() – Case conversion
print(hostname.upper())   # 'R1-CORE-SWITCH'
print(hostname.lower())   # 'r1-core-switch'

# title() – Capitalize first letter of each word
name = 'john smith'
print(name.title())       # 'John Smith'

# capitalize() – Capitalize only first letter
print(hostname.capitalize())  # 'R1-core-switch'

# replace() – Substitute substrings
old_config = 'ip address 10.1.1.1 255.255.255.0'
new_config = old_config.replace('10.1.1.1', '10.2.2.1')
print(new_config)  # 'ip address 10.2.2.1 255.255.255.0'

# You can chain replacements
clean_output = raw_output.replace('\r\n', '\n').replace('\r', '\n')
```

#### Splitting and Joining – THE Most Important Methods

```python
# split() – Break a string into a list of parts
# This is used in almost every network parsing script

# Split by whitespace (default)
line = 'GigabitEthernet0/0 192.168.1.1     YES manual up       up'
fields = line.split()
print(fields)
# ['GigabitEthernet0/0', '192.168.1.1', 'YES', 'manual', 'up', 'up']

intf_name = fields[0]   # 'GigabitEthernet0/0'
ip_addr = fields[1]     # '192.168.1.1'
status = fields[4]      # 'up'
protocol = fields[5]    # 'up'

# Split by specific delimiter
vlan_string = '10,20,30,40,100'
vlan_list = vlan_string.split(',')
print(vlan_list)  # ['10', '20', '30', '40', '100']

# Split IP address into octets
ip = '192.168.1.1'
octets = ip.split('.')
print(octets)  # ['192', '168', '1', '1']
print(octets[0])  # '192' — first octet

# splitlines() – Split multiline string (PyNEng favorite)
show_output = '''Interface          IP-Address
GigabitEthernet0/0 192.168.1.1
GigabitEthernet0/1 10.1.1.1'''

lines = show_output.strip().splitlines()
print(len(lines))  # 3
for line in lines[1:]:  # Skip header
    print(line)

# join() – The opposite of split() — combine list into string
commands = [
    'interface GigabitEthernet0/1',
    ' switchport mode access',
    ' switchport access vlan 10',
    ' no shutdown',
]
config_block = '\n'.join(commands)
print(config_block)
# interface GigabitEthernet0/1
#  switchport mode access
#  switchport access vlan 10
#  no shutdown

# Join VLANs for trunk config
vlans = [10, 20, 30, 40]
vlan_str = ','.join(str(v) for v in vlans)
print(f'switchport trunk allowed vlan {vlan_str}')
# switchport trunk allowed vlan 10,20,30,40
```

### String Formatting – Three Methods

Python has evolved its string formatting over the years. All three sources cover this, but with different emphasis:

```python
hostname = 'R1-CORE'
ip = '10.255.0.1'
vlan = 100
uptime = 47.5

# ---- Method 1: f-strings (RECOMMENDED — PCC Ch 2, PyNEng, Byers) ----
# Available in Python 3.6+. The modern, readable way.
print(f"Device: {hostname}, IP: {ip}")
print(f"VLAN {vlan} on {hostname}")

# Expressions inside f-strings
print(f"Hostname uppercase: {hostname.upper()}")
print(f"First octet: {ip.split('.')[0]}")
print(f"Uptime: {uptime:.1f} days")

# Alignment and padding (great for formatted tables)
print(f"{'Hostname':<20s} {'IP Address':<16s} {'Status'}")
print(f"{'-' * 20} {'-' * 16} {'-' * 8}")
print(f"{hostname:<20s} {ip:<16s} {'UP'}")
# Output:
# Hostname             IP Address       Status
# -------------------- ---------------- --------
# R1-CORE              10.255.0.1       UP

# Width and fill characters
for v in [10, 20, 100, 4094]:
    print(f"VLAN {v:>5d}")
# VLAN    10
# VLAN    20
# VLAN   100
# VLAN  4094

# ---- Method 2: .format() method (PyNEng uses this frequently) ----
template = 'switchport access vlan {}'
print(template.format(100))  # switchport access vlan 100

# Named placeholders
msg = 'Device {name} at {ip} is {status}'
print(msg.format(name='R1', ip='10.1.1.1', status='reachable'))

# ---- Method 3: % operator (older style, seen in legacy code) ----
print("VLAN %d on %s" % (100, hostname))
# You'll see this in older scripts but shouldn't write new code with it
```

---

## 2.3 Numbers in Network Context

```python
# ---- Integers (int) ----
vlan_id = 100
ssh_port = 22
bgp_as = 65001
max_routes = 1_000_000    # Underscores for readability (PCC tip)

# Arithmetic operations
total_ports = 48
used_ports = 36
available = total_ports - used_ports        # 12
utilization = (used_ports / total_ports) * 100  # 75.0

# Integer division and modulo
print(17 // 5)   # 3 (floor division — whole number only)
print(17 % 5)    # 2 (modulo — remainder)
print(2 ** 8)    # 256 (exponentiation — 2 to the 8th)
print(2 ** 32)   # 4294967296 (useful: total IPv4 addresses)

# ---- Floats (decimal numbers) ----
cpu_usage = 45.7
bandwidth_gbps = 10.0
latency_ms = 2.34
packet_loss = 0.01    # 1% loss

# Float precision (be careful!)
print(0.1 + 0.2)         # 0.30000000000000004 (not exactly 0.3!)
print(round(0.1 + 0.2, 1))  # 0.3 (use round() for display)

# ---- Type Conversion ----
# This is CRITICAL because input() always returns strings
user_input = '100'           # String from input() or CLI parsing
vlan_num = int(user_input)   # Convert to integer: 100
bw_value = float('10.5')    # Convert to float: 10.5
vlan_str = str(vlan_num)    # Convert back to string: '100'

# Network-specific conversions
ip_parts = '192.168.1.1'.split('.')
first_octet = int(ip_parts[0])  # 192 as an integer
if 1 <= first_octet <= 126:
    print("Class A network")
elif 128 <= first_octet <= 191:
    print("Class B network")
elif 192 <= first_octet <= 223:
    print("Class C network")

# Subnet calculations
prefix_length = 24
host_bits = 32 - prefix_length          # 8
total_addresses = 2 ** host_bits         # 256
usable_hosts = total_addresses - 2       # 254
print(f"/{prefix_length} = {usable_hosts} usable hosts")
```

---

## 2.4 Step-by-Step Exercise: Parsing Show Command Output

This exercise combines everything from Module 2 and is the kind of task you'll do constantly in network automation:

```python
#!/usr/bin/env python3
"""
Parse 'show ip interface brief' output and display a formatted report.
Combines: PCC string methods + PyNEng parsing patterns + Byers style
"""

# Simulated output (in real scripts, this comes from netmiko)
show_ip_int_br = """
Interface                  IP-Address      OK? Method Status                Protocol
GigabitEthernet0/0         192.168.1.1     YES NVRAM  up                    up
GigabitEthernet0/1         10.1.1.1        YES NVRAM  up                    up
GigabitEthernet0/2         unassigned      YES NVRAM  administratively down down
Serial0/0/0                172.16.1.1      YES NVRAM  up                    up
Loopback0                  10.255.0.1      YES NVRAM  up                    up
Loopback1                  10.255.1.1      YES NVRAM  up                    up
Vlan1                      unassigned      YES NVRAM  up                    up
"""

# Step 1: Clean up and split into lines
lines = show_ip_int_br.strip().splitlines()
print(f"Total lines (including header): {len(lines)}")

# Step 2: Print formatted header
print(f"\n{'Interface':<28s} {'IP Address':<16s} {'Status':<12s} {'Protocol'}")
print(f"{'-'*28} {'-'*16} {'-'*12} {'-'*10}")

# Step 3: Process each data line (skip header)
up_count = 0
down_count = 0

for line in lines[1:]:
    # Split the line into fields
    # Note: 'administratively down' has a space, so we handle it carefully
    if 'administratively' in line:
        # Special handling for admin down interfaces
        parts = line.split()
        intf = parts[0]
        ip = parts[1]
        status = 'admin-down'
        protocol = parts[-1]
    else:
        parts = line.split()
        intf = parts[0]
        ip = parts[1]
        status = parts[4]
        protocol = parts[5]

    # Step 4: Count up/down
    if protocol == 'up':
        up_count += 1
    else:
        down_count += 1

    # Step 5: Format output with f-strings
    status_indicator = '✓' if protocol == 'up' else '✗'
    print(f"{intf:<28s} {ip:<16s} {status:<12s} {protocol} {status_indicator}")

# Step 6: Print summary
total = up_count + down_count
print(f"\n{'='*70}")
print(f"Total: {total} interfaces | Up: {up_count} | Down: {down_count}")
print(f"Availability: {(up_count/total)*100:.1f}%")
```

---

## Module 2 Practice Questions

**Q2.1:** What is the difference between `split()` and `splitlines()`?

```
Answer:
- split() breaks a string by a delimiter (default: any whitespace).
  It works on a SINGLE line to separate fields.
  Example: 'Gi0/0 10.1.1.1 up'.split() → ['Gi0/0', '10.1.1.1', 'up']

- splitlines() breaks a MULTILINE string into a list of individual lines.
  Example: 'line1\nline2\nline3'.splitlines() → ['line1', 'line2', 'line3']

Typical workflow: use splitlines() first to get individual lines,
then use split() on each line to extract fields.
```

**Q2.2:** Given `ip = '10.1.1.1'`, how do you get just the first octet as an integer?

```python
# Answer:
first_octet = int(ip.split('.')[0])   # 10
```

**Q2.3:** Write an f-string that prints a router hostname left-aligned in 20 characters, followed by its IP right-aligned in 16 characters.

```python
# Answer:
hostname = 'R1-CORE'
ip = '10.255.0.1'
print(f"{hostname:<20s}{ip:>16s}")
# Output: R1-CORE             10.255.0.1
```

**Q2.4:** What does `raw string` (r-prefix) do and why is it important for regex?

```
Answer: A raw string (r'...') treats backslashes as literal characters
instead of escape sequences. This is critical for regex because regex
uses lots of backslashes (\d, \s, \S, etc.). Without r-prefix, Python
would try to interpret \d as an escape code and either error or produce
wrong results.

Example: r'\d+\.\d+' means literally \d+\.\d+ (regex pattern)
Without r: '\d+\.\d+' — Python might misinterpret some backslash combos
```

**Q2.5 Homework Script:** Write a script that takes a multiline string containing 5 lines of `show cdp neighbors` output and extracts the device ID and connected interface into a formatted table.

---

# Module 3: Lists & Tuples

> 📚 **Sources:** PCC Ch 3–4 | PyNEng Ch 4 (Lists/Tuples) | Byers Free Wk2, LP Wk2

## Why This Module Matters

Lists are Python's most versatile data structure. In network automation, you'll use lists to store:
- Collections of commands to send to a device
- Lists of IP addresses to ping
- Parsed output from show commands
- Device hostnames to iterate through
- VLAN IDs, interface names, routing table entries

PCC dedicates TWO full chapters (Ch 3 and Ch 4) to lists because they're that important. PyNEng teaches lists exclusively through network examples. Kirk Byers' courses use lists from the very first exercises.

---

## 3.1 Creating Lists

```python
# ---- PCC style: everyday examples (Ch 3) ----
bicycles = ['trek', 'cannondale', 'redline', 'specialized']
print(bicycles)

# ---- Network engineer style (PyNEng + Byers) ----
# A list of VLANs
vlans = [10, 20, 30, 40, 100, 200]

# A list of commands to send to a switch
access_commands = [
    'switchport mode access',
    'switchport access vlan 10',
    'switchport nonegotiate',
    'spanning-tree portfast',
    'spanning-tree bpduguard enable',
]

# A list of device IPs to connect to
device_ips = [
    '10.255.0.1',
    '10.255.0.2',
    '10.255.0.3',
    '10.255.0.10',
    '10.255.0.11',
]

# A list of dictionaries (VERY common pattern — Byers + PyNEng)
devices = [
    {'hostname': 'R1', 'ip': '10.0.0.1', 'platform': 'cisco_ios'},
    {'hostname': 'R2', 'ip': '10.0.0.2', 'platform': 'cisco_ios'},
    {'hostname': 'SW1', 'ip': '10.0.0.10', 'platform': 'cisco_ios'},
]

# Empty list (start empty, add items later)
failed_devices = []
collected_outputs = []
```

## 3.2 Accessing List Elements

```python
vlans = [10, 20, 30, 40, 100]

# ---- Indexing (PCC Ch 3) ----
# Python uses ZERO-BASED indexing
first_vlan = vlans[0]     # 10
second_vlan = vlans[1]    # 20
last_vlan = vlans[-1]     # 100
second_to_last = vlans[-2]  # 40

# ---- Slicing [start:end:step] (PCC Ch 4) ----
# end index is EXCLUSIVE (up to but not including)
print(vlans[0:3])    # [10, 20, 30]  — first 3 elements
print(vlans[:3])     # [10, 20, 30]  — same (start defaults to 0)
print(vlans[2:])     # [30, 40, 100] — from index 2 to end
print(vlans[-3:])    # [30, 40, 100] — last 3 elements
print(vlans[::2])    # [10, 30, 100] — every other element
print(vlans[::-1])   # [100, 40, 30, 20, 10] — reversed

# ---- Slicing for parsing (PyNEng technique) ----
# Skip the header line in show command output
output_lines = [
    'Interface          IP-Address      OK? Method Status   Protocol',
    'GigabitEthernet0/0 192.168.1.1     YES manual up       up',
    'GigabitEthernet0/1 10.1.1.1        YES manual up       up',
    'GigabitEthernet0/2 unassigned      YES unset  down     down',
]
data_lines = output_lines[1:]  # Skip header — this pattern is EVERYWHERE

# ---- Copying a list (PCC Ch 4 — important gotcha!) ----
original_vlans = [10, 20, 30]

# WRONG way (creates a reference, not a copy!)
alias = original_vlans        # Both point to SAME list
alias.append(40)
print(original_vlans)  # [10, 20, 30, 40] — original changed too!

# RIGHT way (creates a true copy)
copy1 = original_vlans[:]        # Slice copy
copy2 = original_vlans.copy()    # .copy() method
copy3 = list(original_vlans)     # list() constructor
```

## 3.3 Modifying Lists

Lists are **mutable** — you can add, remove, and change elements after creation:

```python
# ---- Adding elements ----
vlans = [10, 20, 30]

# append() — add ONE item to the END
vlans.append(40)
print(vlans)  # [10, 20, 30, 40]

# insert() — add at a SPECIFIC position
vlans.insert(0, 1)      # Insert VLAN 1 at the beginning
print(vlans)  # [1, 10, 20, 30, 40]

# extend() — add ALL items from ANOTHER list
new_vlans = [50, 60, 70]
vlans.extend(new_vlans)
print(vlans)  # [1, 10, 20, 30, 40, 50, 60, 70]

# + operator — creates a NEW list (doesn't modify original)
combined = vlans + [80, 90]
print(combined)  # [1, 10, 20, 30, 40, 50, 60, 70, 80, 90]
print(vlans)     # [1, 10, 20, 30, 40, 50, 60, 70] — unchanged!

# ---- Removing elements ----
vlans = [10, 20, 30, 40, 50]

# remove() — remove by VALUE (first occurrence)
vlans.remove(30)
print(vlans)  # [10, 20, 40, 50]

# pop() — remove by INDEX and RETURN the removed item
last = vlans.pop()       # Remove and return last item
print(last)   # 50
print(vlans)  # [10, 20, 40]

first = vlans.pop(0)     # Remove and return first item
print(first)  # 10
print(vlans)  # [20, 40]

# del — remove by index (no return value)
vlans = [10, 20, 30, 40, 50]
del vlans[2]          # Remove item at index 2
print(vlans)  # [10, 20, 40, 50]
del vlans[1:3]        # Remove slice
print(vlans)  # [10, 50]

# clear() — remove ALL items
vlans.clear()
print(vlans)  # []

# ---- Changing elements ----
interfaces = ['Gi0/0', 'Gi0/1', 'Gi0/2']
interfaces[1] = 'GigabitEthernet0/1'  # Replace by index
print(interfaces)  # ['Gi0/0', 'GigabitEthernet0/1', 'Gi0/2']
```

## 3.4 Sorting Lists

```python
# sort() — sort IN PLACE (modifies the list, returns None!)
vlans = [100, 10, 40, 20, 30]
vlans.sort()
print(vlans)  # [10, 20, 30, 40, 100]

vlans.sort(reverse=True)
print(vlans)  # [100, 40, 30, 20, 10]

# sorted() — return a NEW sorted list (original unchanged)
original = [100, 10, 40, 20, 30]
ordered = sorted(original)
print(original)  # [100, 10, 40, 20, 30] — unchanged!
print(ordered)   # [10, 20, 30, 40, 100]

# Sorting strings (alphabetical)
hostnames = ['SW2', 'R1', 'FW1', 'R3', 'SW1']
hostnames.sort()
print(hostnames)  # ['FW1', 'R1', 'R3', 'SW1', 'SW2']

# Custom sort with key function
# Sort interfaces numerically by port number
interfaces = ['Gi0/10', 'Gi0/2', 'Gi0/1', 'Gi0/3', 'Gi0/20']
interfaces_sorted = sorted(interfaces, key=lambda x: int(x.split('/')[1]))
print(interfaces_sorted)
# ['Gi0/1', 'Gi0/2', 'Gi0/3', 'Gi0/10', 'Gi0/20']

# reverse() — reverse the current order (not sort!)
commands = ['no shutdown', 'switchport access vlan 10', 'interface Gi0/1']
commands.reverse()
print(commands)  # ['interface Gi0/1', 'switchport access vlan 10', 'no shutdown']
```

## 3.5 Looping Through Lists (PCC Ch 3-4 + PyNEng Ch 7)

This is covered more in Module 6, but the basics:

```python
# Basic for loop (PCC uses singular/plural naming convention)
vlans = [10, 20, 30, 40]
for vlan in vlans:
    print(f"vlan {vlan}")

# With index using enumerate()
for index, vlan in enumerate(vlans):
    print(f"Index {index}: VLAN {vlan}")

# Building a command list for netmiko (PyNEng + Byers pattern)
interfaces = ['Gi0/1', 'Gi0/2', 'Gi0/3']
all_commands = []

for intf in interfaces:
    all_commands.append(f'interface {intf}')
    all_commands.append(' switchport mode access')
    all_commands.append(' switchport access vlan 10')
    all_commands.append(' no shutdown')

# all_commands is now ready to send via ssh.send_config_set()
```

## 3.6 The range() Function (PCC Ch 4)

```python
# range(stop) — 0 to stop-1
for i in range(5):
    print(i)  # 0, 1, 2, 3, 4

# range(start, stop) — start to stop-1
for port in range(1, 49):
    print(f"interface GigabitEthernet0/{port}")

# range(start, stop, step)
for vlan in range(100, 201, 10):
    print(f"vlan {vlan}")  # 100, 110, 120, ..., 200

# Generate a list from range
port_numbers = list(range(1, 49))  # [1, 2, 3, ..., 48]
even_vlans = list(range(10, 50, 10))  # [10, 20, 30, 40]
```

## 3.7 Simple Statistics (PCC Ch 4)

```python
latencies = [2.3, 5.1, 1.8, 3.4, 2.9, 4.2]

print(f"Min latency: {min(latencies)} ms")    # 1.8
print(f"Max latency: {max(latencies)} ms")    # 5.1
print(f"Avg latency: {sum(latencies)/len(latencies):.2f} ms")  # 3.28
print(f"Total samples: {len(latencies)}")     # 6
```

## 3.8 Tuples – Immutable Lists

```python
# Tuples use parentheses (or just commas)
dimensions = (1920, 1080)
connection_params = ('192.168.1.1', 22, 'cisco_ios')

# You CANNOT modify a tuple after creation
# connection_params[0] = '10.1.1.1'  # TypeError!

# But you CAN overwrite the entire variable
dimensions = (2560, 1440)

# Tuple unpacking — extracting values into variables
ip, port, platform = connection_params
print(ip)        # '192.168.1.1'
print(port)      # 22
print(platform)  # 'cisco_ios'

# When to use tuples vs lists:
# - Use LISTS when data might change (adding/removing items)
# - Use TUPLES for fixed data (connection params, coordinates, dict keys)

# Tuples as dictionary keys (lists CAN'T be dict keys!)
interface_ips = {
    ('R1', 'Gi0/0'): '192.168.1.1',
    ('R1', 'Gi0/1'): '10.1.1.1',
    ('R2', 'Gi0/0'): '192.168.2.1',
}
print(interface_ips[('R1', 'Gi0/0')])  # '192.168.1.1'
```

---

## Module 3 Practice Questions

**Q3.1:** What is the output of this code?
```python
vlans = [10, 20, 30, 40, 50]
print(vlans[1:4])
```

```
Answer: [20, 30, 40]
Explanation: Slicing is [start:end] where end is EXCLUSIVE.
Index 1 is 20, index 2 is 30, index 3 is 40. Index 4 (50) is NOT included.
```

**Q3.2:** What is the difference between `append()` and `extend()`?

```
Answer:
- append(item) adds ONE item to the end. If you append a list, the entire
  list becomes a single nested element.
  [1,2].append([3,4]) → [1, 2, [3, 4]]

- extend(list) adds EACH item from the argument list individually.
  [1,2].extend([3,4]) → [1, 2, 3, 4]
```

**Q3.3:** Why does this code produce unexpected results?
```python
original = [10, 20, 30]
copy = original
copy.append(40)
print(original)  # [10, 20, 30, 40] — WHY?
```

```
Answer: 'copy = original' creates a REFERENCE (alias), not a true copy.
Both variables point to the same list object in memory.
Fix: use copy = original[:] or copy = original.copy()
```

**Q3.4 Homework Script:** Write a script that generates Cisco configuration for 48 access ports (Gi0/1 through Gi0/48), assigning VLANs in a round-robin pattern from `[10, 20, 30]`. The output should be valid IOS configuration.

```python
# Expected output format:
# interface GigabitEthernet0/1
#  switchport mode access
#  switchport access vlan 10
#  spanning-tree portfast
# !
# interface GigabitEthernet0/2
#  switchport mode access
#  switchport access vlan 20
# ...
```

**Q3.5 Homework Script:** Create a script that reads a list of 10 IP addresses, separates them into two lists (reachable and unreachable) based on whether the first octet is in the 10.x.x.x range, and prints both lists sorted.

# Module 4: Dictionaries & Sets

> 📚 **Sources:** PCC Ch 6 | PyNEng Ch 4 (Dicts/Sets) | Byers Free Wk4, LP Wk4

## Why This Module Matters

If strings are the language of network devices and lists are how you organize collections of data, then **dictionaries are how you model the real world of networking**. Every device has properties (hostname, IP, model, OS version). Every interface has attributes (name, IP, status, speed). Every route has components (network, next-hop, metric). Dictionaries let you represent all of these naturally.

Kirk Byers' students consistently report that learning to work with nested dictionaries — what he calls "unwrapping data structures" — is the breakthrough moment where Python starts making real sense for network automation. Structured output from APIs, TextFSM parsing, and YAML files all produce nested dictionaries that you must navigate confidently.

---

## 4.1 Dictionary Fundamentals

### What Is a Dictionary?

A dictionary stores **key-value pairs**. Think of it like a Cisco device's `show` command output structured as labeled fields:

```python
# PCC introduces dictionaries with simple examples (Ch 6)
alien_0 = {'color': 'green', 'points': 5}

# Network engineer's first dictionary (PyNEng style)
router = {
    'hostname': 'R1-CORE',
    'mgmt_ip': '10.255.0.1',
    'vendor': 'Cisco',
    'model': 'ISR4451-X',
    'ios_version': '17.03.04a',
    'serial': 'FTX2137A0B1',
    'uptime_days': 142,
    'is_reachable': True,
}

# The router analogy:
# show version on a Cisco device gives you hostname, version, uptime, etc.
# A dictionary is the Python way to store that same structured data.
```

### Accessing Values

```python
# Direct access with square brackets (raises KeyError if key missing!)
print(router['hostname'])     # 'R1-CORE'
print(router['mgmt_ip'])      # '10.255.0.1'
print(router['uptime_days'])  # 142

# THIS WILL CRASH if the key doesn't exist:
# print(router['location'])  # KeyError: 'location'

# Safe access with .get() — returns None or a default instead of crashing
location = router.get('location')           # None (no crash!)
location = router.get('location', 'Unknown')  # 'Unknown'
serial = router.get('serial', 'N/A')        # 'FTX2137A0B1' (key exists)

# RULE OF THUMB (all three sources agree):
# Use dict['key'] when you're SURE the key exists
# Use dict.get('key', default) when the key MIGHT not exist
```

### Adding, Modifying, and Removing Entries

```python
router = {'hostname': 'R1-CORE', 'mgmt_ip': '10.255.0.1'}

# Add new key-value pairs (PCC Ch 6)
router['location'] = 'Building-A, Rack-12'
router['contact'] = 'netops@company.com'

# Modify existing values
router['mgmt_ip'] = '10.255.0.100'    # Changed!

# Remove entries
del router['contact']                   # Remove by key
popped = router.pop('location')         # Remove AND return the value
print(popped)  # 'Building-A, Rack-12'

# update() — merge another dictionary in (PyNEng technique)
extra_info = {'model': 'ISR4451', 'ios': '17.3.4'}
router.update(extra_info)
# If keys overlap, the new values overwrite the old ones

# setdefault() — set only if key doesn't already exist
router.setdefault('vendor', 'Cisco')     # Sets 'Cisco' only if 'vendor' is missing
router.setdefault('hostname', 'UNKNOWN')  # Does nothing — hostname already exists
```

### Iterating Through Dictionaries

```python
device = {
    'hostname': 'SW1-ACCESS',
    'mgmt_ip': '10.255.0.10',
    'model': 'C9300-48T',
    'ios_version': '17.06.03',
    'location': 'Floor-2, IDF-A',
}

# Loop through ALL key-value pairs — .items()
print("=== Device Information ===")
for key, value in device.items():
    print(f"  {key:15s}: {value}")

# Loop through KEYS only — .keys()
print("\nAvailable fields:")
for key in device.keys():
    print(f"  - {key}")

# Loop through VALUES only — .values()
print("\nAll values:")
for value in device.values():
    print(f"  {value}")

# Sorted iteration (PCC Ch 6 technique)
for key in sorted(device.keys()):
    print(f"  {key}: {device[key]}")
```

---

## 4.2 Nested Data Structures — Kirk Byers' Key Lesson

Kirk Byers emphasizes that the ability to navigate nested data structures is **the breakthrough skill** for network automation. API responses, TextFSM output, YAML files — they all produce nested combinations of dictionaries and lists.

### The Unwrapping Technique

```python
# This is what structured data from a network device looks like
# (similar to what netmiko + TextFSM returns, or what an API gives you)

network_data = {
    'device': {
        'hostname': 'R1-CORE',
        'interfaces': [
            {
                'name': 'GigabitEthernet0/0',
                'ip_address': '192.168.1.1',
                'subnet_mask': '255.255.255.0',
                'status': 'up',
                'protocol': 'up',
                'speed': '1000Mbps',
                'duplex': 'full',
            },
            {
                'name': 'GigabitEthernet0/1',
                'ip_address': '10.1.1.1',
                'subnet_mask': '255.255.255.252',
                'status': 'up',
                'protocol': 'up',
                'speed': '1000Mbps',
                'duplex': 'full',
            },
            {
                'name': 'GigabitEthernet0/2',
                'ip_address': 'unassigned',
                'subnet_mask': '',
                'status': 'down',
                'protocol': 'down',
                'speed': 'auto',
                'duplex': 'auto',
            },
        ],
        'routing': {
            'ospf': {
                'process_id': 1,
                'router_id': '10.255.0.1',
                'neighbors': [
                    {'neighbor_id': '10.255.0.2', 'state': 'FULL/DR', 'interface': 'Gi0/0'},
                    {'neighbor_id': '10.255.0.3', 'state': 'FULL/BDR', 'interface': 'Gi0/1'},
                ]
            }
        }
    }
}

# ---- BYERS' UNWRAPPING TECHNIQUE ----
# Step 1: Start at the top. What type is the outer structure?
print(type(network_data))           # <class 'dict'>
print(network_data.keys())          # dict_keys(['device'])

# Step 2: Go one level deeper
device = network_data['device']
print(type(device))                 # <class 'dict'>
print(device.keys())                # dict_keys(['hostname', 'interfaces', 'routing'])

# Step 3: Access the hostname (simple string)
print(device['hostname'])           # 'R1-CORE'

# Step 4: Access interfaces (it's a list of dicts!)
interfaces = device['interfaces']
print(type(interfaces))             # <class 'list'>
print(len(interfaces))              # 3

# Step 5: Access one interface (it's a dict)
first_intf = interfaces[0]
print(type(first_intf))             # <class 'dict'>
print(first_intf['name'])           # 'GigabitEthernet0/0'
print(first_intf['ip_address'])     # '192.168.1.1'

# Step 6: Loop through all interfaces
print("\n--- Interface Report ---")
for intf in device['interfaces']:
    status_symbol = '✓' if intf['protocol'] == 'up' else '✗'
    print(f"  {status_symbol} {intf['name']:25s} {intf['ip_address']:16s} {intf['status']}/{intf['protocol']}")

# Step 7: Dive into nested routing info
ospf = device['routing']['ospf']
print(f"\nOSPF Process {ospf['process_id']}, Router ID: {ospf['router_id']}")
for neighbor in ospf['neighbors']:
    print(f"  Neighbor {neighbor['neighbor_id']:15s} State: {neighbor['state']:12s} via {neighbor['interface']}")
```

### List of Dictionaries — The Most Common Pattern

```python
# This is the pattern you'll see EVERYWHERE in network automation:
# - netmiko send_command(use_textfsm=True) returns this
# - YAML device files parse to this
# - API responses contain this

show_ip_int_brief = [
    {'intf': 'Gi0/0', 'ipaddr': '192.168.1.1', 'status': 'up', 'proto': 'up'},
    {'intf': 'Gi0/1', 'ipaddr': '10.1.1.1', 'status': 'up', 'proto': 'up'},
    {'intf': 'Gi0/2', 'ipaddr': 'unassigned', 'status': 'down', 'proto': 'down'},
    {'intf': 'Lo0', 'ipaddr': '10.255.0.1', 'status': 'up', 'proto': 'up'},
]

# Filter for only 'up' interfaces
up_interfaces = [entry for entry in show_ip_int_brief if entry['proto'] == 'up']
print(f"Up interfaces: {len(up_interfaces)}")

# Build a quick lookup dictionary: interface name → IP
ip_lookup = {entry['intf']: entry['ipaddr'] for entry in show_ip_int_brief}
print(ip_lookup)
# {'Gi0/0': '192.168.1.1', 'Gi0/1': '10.1.1.1', 'Gi0/2': 'unassigned', 'Lo0': '10.255.0.1'}

# Get a specific interface's IP
print(ip_lookup.get('Gi0/0'))   # '192.168.1.1'
print(ip_lookup.get('Gi0/5', 'Not found'))  # 'Not found'
```

---

## 4.3 The Netmiko Device Dictionary

This is **THE** most important dictionary pattern in network automation. Every netmiko script uses it:

```python
# Basic device dictionary
cisco_router = {
    'device_type': 'cisco_ios',      # REQUIRED: tells netmiko which driver to use
    'host': '192.168.1.1',           # REQUIRED: IP or hostname
    'username': 'admin',              # REQUIRED: SSH username
    'password': 'C1sc0!23',          # REQUIRED: SSH password
    'secret': 'En@ble!23',           # OPTIONAL: enable password
    'port': 22,                       # OPTIONAL: SSH port (default 22)
    'timeout': 30,                    # OPTIONAL: connection timeout in seconds
    'session_log': 'session_R1.log',  # OPTIONAL: log all session activity
}

# Common device_type values:
# 'cisco_ios'     — Cisco IOS/IOS-XE (routers, switches)
# 'cisco_nxos'    — Cisco NX-OS (Nexus switches)
# 'cisco_asa'     — Cisco ASA firewalls
# 'cisco_xr'      — Cisco IOS-XR
# 'cisco_ftd'     — Cisco Firepower FTD (via SSH)
# 'arista_eos'    — Arista switches
# 'juniper_junos' — Juniper devices
# 'cisco_ios_telnet' — Telnet to Cisco IOS

# The ** unpacking operator (PCC covers *args/**kwargs in Ch 8)
from netmiko import ConnectHandler
# These two lines are EQUIVALENT:
ssh = ConnectHandler(**cisco_router)
# ssh = ConnectHandler(device_type='cisco_ios', host='192.168.1.1', ...)
```

### Loading Multiple Devices from YAML

```python
# devices.yaml file:
# ---
# - hostname: R1-CORE
#   device_type: cisco_ios
#   host: 10.255.0.1
#   username: admin
#   password: cisco123
#   secret: enable123
#
# - hostname: R2-DIST
#   device_type: cisco_ios
#   host: 10.255.0.2
#   username: admin
#   password: cisco123
#   secret: enable123
#
# - hostname: SW1-ACCESS
#   device_type: cisco_ios
#   host: 10.255.0.10
#   username: admin
#   password: cisco123

import yaml

with open('devices.yaml') as f:
    devices = yaml.safe_load(f)

# devices is now a list of dictionaries — ready for netmiko!
print(type(devices))     # <class 'list'>
print(len(devices))      # 3

for device in devices:
    print(f"  {device['hostname']:15s} {device['host']:15s} {device['device_type']}")
```

---

## 4.4 Sets — Unique Collections for Comparisons

Sets store **unique values only** and support mathematical set operations. They're perfect for comparing configuration state across devices.

```python
# ---- Creating Sets ----
sw1_vlans = {10, 20, 30, 40, 100}
sw2_vlans = {10, 20, 50, 60, 100}

# Sets automatically remove duplicates
vlan_list = [10, 20, 10, 30, 20, 40, 30]
unique_vlans = set(vlan_list)
print(unique_vlans)  # {40, 10, 20, 30}  (unordered!)
print(sorted(unique_vlans))  # [10, 20, 30, 40]  (sorted list)

# ---- Set Operations (THE power feature) ----

# INTERSECTION (&) — Items in BOTH sets
common = sw1_vlans & sw2_vlans
print(f"Common VLANs: {sorted(common)}")     # [10, 20, 100]

# DIFFERENCE (-) — Items in first set but NOT in second
only_sw1 = sw1_vlans - sw2_vlans
only_sw2 = sw2_vlans - sw1_vlans
print(f"Only on SW1: {sorted(only_sw1)}")     # [30, 40]
print(f"Only on SW2: {sorted(only_sw2)}")     # [50, 60]

# SYMMETRIC DIFFERENCE (^) — Items in EITHER but not BOTH
mismatched = sw1_vlans ^ sw2_vlans
print(f"Mismatched: {sorted(mismatched)}")    # [30, 40, 50, 60]

# UNION (|) — ALL unique items from both sets
all_vlans = sw1_vlans | sw2_vlans
print(f"All VLANs: {sorted(all_vlans)}")      # [10, 20, 30, 40, 50, 60, 100]

# SUBSET / SUPERSET tests
required_vlans = {10, 20, 100}
print(required_vlans <= sw1_vlans)  # True — required is a subset of sw1
print(required_vlans <= sw2_vlans)  # True — required is a subset of sw2

# ---- Real-World Use Case: Configuration Compliance ----
required_ntp_servers = {'10.255.0.100', '10.255.0.101'}
configured_ntp = {'10.255.0.100', '10.255.0.102'}

missing = required_ntp_servers - configured_ntp
extra = configured_ntp - required_ntp_servers
print(f"Missing NTP servers: {missing}")   # {'10.255.0.101'}
print(f"Unauthorized NTP servers: {extra}")  # {'10.255.0.102'}
```

---

## Module 4 Practice Questions

**Q4.1:** What is the output of `device.get('serial', 'N/A')` if the dictionary does NOT contain a 'serial' key?
```
Answer: 'N/A' — the .get() method returns the default value when the key is missing,
instead of raising a KeyError like direct access with device['serial'] would.
```

**Q4.2:** Given nested data, how do you access the OSPF router ID?
```python
data = {'routing': {'ospf': {'router_id': '10.255.0.1', 'process': 1}}}
# Answer:
router_id = data['routing']['ospf']['router_id']  # '10.255.0.1'
```

**Q4.3:** Write code to find VLANs that need to be ADDED to SW2 to match SW1.
```python
sw1 = {10, 20, 30, 40, 100}
sw2 = {10, 20, 100}
# Answer:
to_add = sw1 - sw2   # {40, 30}
```

**Q4.4 Homework Script:** Create a "VLAN Compliance Checker" that takes two sets of VLANs (required and actual), reports which are missing, which are unauthorized, and gives a compliance percentage.

**Q4.5 Homework Script:** Build a device inventory dictionary from user input (hostname, IP, model, role), then print a formatted table. Allow the user to search by hostname.

---

# Module 5: If Statements & Conditional Logic

> 📚 **Sources:** PCC Ch 5 | PyNEng Ch 6 | Byers LP Wk3

## Why This Module Matters

Conditional logic is how your scripts make decisions. Should we proceed with the configuration change? Is this interface up or down? Did the login succeed or fail? Is this device running the required IOS version? Every automation script needs decision-making.

PCC teaches conditionals through everyday examples (voting age, ticket pricing). PyNEng applies them directly to interface classification and route filtering. Both approaches are valuable.

---

## 5.1 Conditional Tests

```python
# ---- Equality and Inequality (PCC Ch 5) ----
vlan = 100
print(vlan == 100)     # True
print(vlan == 200)     # False
print(vlan != 200)     # True

# CRITICAL: == tests equality, = assigns a value
# vlan == 100  →  "Is vlan equal to 100?"
# vlan = 100   →  "Set vlan TO 100"

# ---- String Comparison (case-sensitive by default!) ----
platform = 'Cisco'
print(platform == 'Cisco')   # True
print(platform == 'cisco')   # False (case matters!)
print(platform.lower() == 'cisco')  # True (normalize for comparison)

# ---- Numerical Comparisons ----
cpu = 85
print(cpu > 80)     # True
print(cpu >= 85)    # True
print(cpu < 90)     # True
print(cpu <= 84)    # False

# ---- Multiple Conditions ----
# and — BOTH must be True
status = 'up'
protocol = 'up'
if status == 'up' and protocol == 'up':
    print("Interface is fully operational")

# or — AT LEAST ONE must be True
severity = 3
if severity <= 3 or 'CRITICAL' in log_message:
    print("Alert: Requires attention!")

# not — Inverts the truth value
is_reachable = False
if not is_reachable:
    print("Device is unreachable!")

# ---- Membership Testing (in / not in) ----
allowed_vlans = [10, 20, 30, 40, 100]
requested_vlan = 50

if requested_vlan in allowed_vlans:
    print(f"VLAN {requested_vlan} is approved")
else:
    print(f"VLAN {requested_vlan} is NOT in the allowed list")

if 'shutdown' not in config_line:
    print("Interface is active")
```

## 5.2 If / Elif / Else Chains

```python
# ---- PCC Pattern: Ticket Pricing ----
age = 25
if age < 4:
    price = 0
elif age < 18:
    price = 10
elif age < 65:
    price = 40
else:
    price = 15

# ---- Network Pattern: Interface Classification ----
def classify_interface(status, protocol):
    """Classify interface health status.
    
    This function appears in both PyNEng Ch 6 and Byers exercises.
    It's a fundamental pattern for processing show command output.
    """
    if status == 'up' and protocol == 'up':
        return 'HEALTHY'
    elif status == 'up' and protocol == 'down':
        return 'LAYER3-PROBLEM'
    elif status == 'administratively down':
        return 'ADMIN-SHUTDOWN'
    elif status == 'down' and protocol == 'down':
        return 'PHYSICALLY-DOWN'
    else:
        return 'UNKNOWN'

# Test with all interface states
test_cases = [
    ('up', 'up'),
    ('up', 'down'),
    ('administratively down', 'down'),
    ('down', 'down'),
]

for status, proto in test_cases:
    result = classify_interface(status, proto)
    print(f"  Status={status:25s} Proto={proto:5s} → {result}")

# ---- Network Pattern: IP Address Classification ----
def classify_ip(ip_address):
    """Determine the class of an IPv4 address."""
    first_octet = int(ip_address.split('.')[0])
    
    if first_octet == 0:
        return 'Reserved'
    elif first_octet <= 126:
        return 'Class A'
    elif first_octet == 127:
        return 'Loopback'
    elif first_octet <= 191:
        return 'Class B'
    elif first_octet <= 223:
        return 'Class C'
    elif first_octet <= 239:
        return 'Multicast (Class D)'
    else:
        return 'Experimental (Class E)'

ips = ['10.1.1.1', '172.16.0.1', '192.168.1.1', '224.0.0.5', '127.0.0.1']
for ip in ips:
    print(f"  {ip:15s} → {classify_ip(ip)}")

# ---- Network Pattern: IOS Version Compliance ----
def check_ios_compliance(version_string, minimum='17.03.00'):
    """Check if device IOS version meets minimum requirement."""
    # Simple string comparison works for Cisco versioning
    if version_string >= minimum:
        return 'COMPLIANT'
    else:
        return f'NON-COMPLIANT (need >= {minimum})'

devices_versions = {
    'R1': '17.06.03a',
    'R2': '16.12.04',
    'SW1': '17.03.04',
    'SW2': '16.09.05',
}

for hostname, version in devices_versions.items():
    status = check_ios_compliance(version)
    print(f"  {hostname:8s} v{version:12s} {status}")
```

## 5.3 Boolean Values and Truthiness

```python
# ---- Boolean variables (PCC Ch 5) ----
game_active = True
is_connected = False

# ---- Truthy and Falsy values ----
# In Python, some values evaluate as False in boolean context:
# False, None, 0, 0.0, '' (empty string), [] (empty list),
# {} (empty dict), set() (empty set)

# Everything else is truthy (True, non-zero numbers, non-empty strings/lists)

# ---- Practical application: checking if a list is empty ----
failed_devices = []

if failed_devices:
    print(f"WARNING: {len(failed_devices)} devices failed")
else:
    print("All devices processed successfully")

# ---- Checking if a variable has been set ----
output = None    # Not yet assigned

if output:
    print("Got output, processing...")
else:
    print("No output received")

# ---- Ternary expression (one-line if/else) ----
status = 'up'
symbol = '✓' if status == 'up' else '✗'
print(f"Interface: {symbol}")
```

---

## Module 5 Practice Questions

**Q5.1:** What's the difference between `=` and `==`?
```
Answer: = is ASSIGNMENT (sets a variable to a value)
        == is COMPARISON (tests if two values are equal, returns True/False)
```

**Q5.2:** Write a function that takes a prefix length (1-32) and returns whether it represents a host route, point-to-point link, or network.
```python
# Answer:
def classify_prefix(prefix_len):
    if prefix_len == 32:
        return "Host route"
    elif prefix_len >= 30:
        return "Point-to-point link"
    elif prefix_len >= 24:
        return "Small network"
    elif prefix_len >= 16:
        return "Medium network"
    else:
        return "Large network"
```

**Q5.3 Homework Script:** Write a "Port Security Validator" that checks a list of switch ports. Each port is a dictionary with keys: name, mode (access/trunk), vlan, description. The script should flag: ports in trunk mode without a description, access ports on VLAN 1 (default = bad), and any port missing required fields.

---

# Module 6: Loops – for and while

> 📚 **Sources:** PCC Ch 4 (for), Ch 7 (while) | PyNEng Ch 7 | Byers LP Wk3

## Why This Module Matters

Loops let you automate repetitive tasks — the entire reason network engineers learn Python. Instead of manually configuring 48 switch ports, you write a loop that does it in seconds. Instead of checking one device, you loop through hundreds.

---

## 6.1 The for Loop

```python
# ---- Basic pattern (PCC Ch 4) ----
# PCC RULE: Use plural name for the list, singular for the loop variable
# for dog in dogs:  for user in users:  for vlan in vlans:

# ---- Generating Configuration (PyNEng Ch 7) ----
vlans = {
    10: 'MANAGEMENT',
    20: 'SERVERS',
    30: 'USERS',
    40: 'VOICE',
    50: 'PRINTERS',
    99: 'NATIVE',
}

print("! ---- VLAN Configuration ----")
for vlan_id, vlan_name in vlans.items():
    print(f"vlan {vlan_id}")
    print(f" name {vlan_name}")
    print("!")

# ---- Nested Loops for Interface Configuration ----
interfaces = ['GigabitEthernet0/1', 'GigabitEthernet0/2', 'GigabitEthernet0/3']
access_cmds = [
    'switchport mode access',
    'switchport access vlan 10',
    'spanning-tree portfast',
    'spanning-tree bpduguard enable',
    'no shutdown',
]

for intf in interfaces:
    print(f"interface {intf}")
    for cmd in access_cmds:
        print(f" {cmd}")
    print("!")

# ---- Enumerate — Loop with a Counter ----
log_entries = [
    '%SYS-5-RESTART: System restarted',
    '%LINK-3-UPDOWN: Interface GigabitEthernet0/1, changed state to down',
    '%SEC-6-IPACCESSLOGP: list DENY-ALL denied tcp 10.1.1.50',
]

for line_num, entry in enumerate(log_entries, start=1):
    print(f"Line {line_num:3d}: {entry}")

# ---- Zip — Process Two Lists in Parallel ----
hostnames = ['R1', 'R2', 'R3']
mgmt_ips = ['10.255.0.1', '10.255.0.2', '10.255.0.3']
platforms = ['cisco_ios', 'cisco_ios', 'cisco_nxos']

for hostname, ip, platform in zip(hostnames, mgmt_ips, platforms):
    print(f"  {hostname:8s} {ip:15s} ({platform})")

# Build a list of device dicts from parallel lists
devices = [
    {'hostname': h, 'host': ip, 'device_type': p}
    for h, ip, p in zip(hostnames, mgmt_ips, platforms)
]
```

## 6.2 The while Loop

```python
# ---- Basic while loop (PCC Ch 7) ----
current_number = 1
while current_number <= 5:
    print(current_number)
    current_number += 1

# ---- Connection Retry Pattern (PyNEng + Byers) ----
import time

def connect_with_retry(device_ip, max_retries=3, delay=5):
    """Attempt to connect to a device with automatic retry.
    
    This pattern is used in every production network automation script.
    """
    for attempt in range(1, max_retries + 1):
        print(f"  Attempt {attempt}/{max_retries} to {device_ip}...")
        try:
            # In real code: ssh = ConnectHandler(**device_params)
            if attempt == 3:  # Simulating success on 3rd try
                print(f"  ✓ Connected to {device_ip}")
                return True
            else:
                raise ConnectionError("Connection refused")
        except ConnectionError as e:
            print(f"  ✗ Failed: {e}")
            if attempt < max_retries:
                print(f"    Waiting {delay}s before retry...")
                time.sleep(delay)
    
    print(f"  ✗ All {max_retries} attempts to {device_ip} FAILED")
    return False

# ---- break and continue ----
# break — exit the loop immediately
# continue — skip the rest of this iteration, go to next

# Process a list of devices, skip unreachable ones, stop on critical error
devices = ['10.0.0.1', '10.0.0.2', 'INVALID', '10.0.0.3', 'CRITICAL_ERROR']

for device in devices:
    if device == 'CRITICAL_ERROR':
        print(f"CRITICAL: Stopping all operations!")
        break           # Exit the loop entirely
    
    if device == 'INVALID':
        print(f"Skipping invalid entry: {device}")
        continue        # Skip to next device
    
    print(f"Processing {device}...")
```

---

## Module 6 Practice Questions

**Q6.1 Homework Script:** Generate Cisco switch configuration for 48 access ports with round-robin VLAN assignment.

**Q6.2 Homework Script:** Write a "device poller" using a while loop that checks device status every 30 seconds until the user presses Ctrl+C, displaying a timestamp with each check.

---

# Module 7: Comprehensions & Built-in Functions

> 📚 **Sources:** PCC Ch 4 (list comprehensions) | PyNEng Ch 8, 10 | Byers LP Wk3

## 7.1 List Comprehensions

```python
# ---- Traditional loop (PCC shows this first, then the comprehension) ----
squares = []
for x in range(1, 11):
    squares.append(x ** 2)

# ---- List comprehension (same result, one line) ----
squares = [x ** 2 for x in range(1, 11)]

# ---- Network examples (PyNEng Ch 8) ----

# Extract only UP interfaces from parsed output
all_interfaces = [
    {'name': 'Gi0/0', 'status': 'up', 'ip': '10.1.1.1'},
    {'name': 'Gi0/1', 'status': 'down', 'ip': 'unassigned'},
    {'name': 'Gi0/2', 'status': 'up', 'ip': '10.2.2.1'},
    {'name': 'Lo0', 'status': 'up', 'ip': '10.255.0.1'},
]

# With condition (filtering)
up_names = [intf['name'] for intf in all_interfaces if intf['status'] == 'up']
print(up_names)  # ['Gi0/0', 'Gi0/2', 'Lo0']

# Transform data
up_ips = [intf['ip'] for intf in all_interfaces if intf['status'] == 'up' and intf['ip'] != 'unassigned']
print(up_ips)  # ['10.1.1.1', '10.2.2.1', '10.255.0.1']

# Generate commands
vlans = [10, 20, 30, 40]
vlan_commands = [f"vlan {v}" for v in vlans]
print(vlan_commands)  # ['vlan 10', 'vlan 20', 'vlan 30', 'vlan 40']

# Convert string VLANs to integers
vlan_strings = ['10', '20', '30', '40']
vlan_ints = [int(v) for v in vlan_strings]
```

## 7.2 Dictionary and Set Comprehensions

```python
# Dict comprehension — build a lookup table
lines = ['Gi0/0 192.168.1.1', 'Gi0/1 10.1.1.1', 'Lo0 10.255.0.1']
ip_map = {line.split()[0]: line.split()[1] for line in lines}
# {'Gi0/0': '192.168.1.1', 'Gi0/1': '10.1.1.1', 'Lo0': '10.255.0.1'}

# Set comprehension — unique first octets
ips = ['10.1.1.1', '10.2.2.2', '192.168.1.1', '10.3.3.3', '172.16.0.1']
first_octets = {ip.split('.')[0] for ip in ips}
# {'10', '172', '192'}

# Practical: build device_type mapping from hostname convention
hostnames = ['R1-CORE', 'R2-DIST', 'SW1-ACCESS', 'SW2-ACCESS', 'FW1-EDGE']
device_types = {
    h: 'cisco_ios' if h.startswith('R') or h.startswith('SW') else 'cisco_asa'
    for h in hostnames
}
```

## 7.3 Essential Built-in Functions (PyNEng Ch 10)

| Function | Purpose | Network Example |
|----------|---------|-----------------|
| `len()` | Count items | `len(interfaces)` |
| `enumerate()` | Loop with index | `for i, line in enumerate(output)` |
| `zip()` | Pair two lists | `dict(zip(names, ips))` |
| `sorted()` | Return sorted copy | `sorted(vlans, reverse=True)` |
| `map()` | Apply function to all | `list(map(int, vlan_strings))` |
| `filter()` | Keep matching items | `list(filter(lambda x: x > 100, vlans))` |
| `all()` | True if ALL True | `all(s == 'up' for s in statuses)` |
| `any()` | True if ANY True | `any('error' in l for l in log_lines)` |
| `min()/max()` | Find extremes | `max(latencies)` |
| `sum()` | Total all items | `sum(packet_counts)` |
| `range()` | Number sequence | `range(1, 49)` for port numbers |
| `isinstance()` | Check type | `isinstance(vlan, int)` |

```python
# ---- all() and any() — great for compliance checking ----
interface_statuses = ['up', 'up', 'up', 'up']
all_up = all(s == 'up' for s in interface_statuses)
print(f"All interfaces up: {all_up}")  # True

log_lines = ['Normal operation', 'WARNING: high CPU', 'Normal operation']
has_warnings = any('WARNING' in line for line in log_lines)
print(f"Warnings found: {has_warnings}")  # True
```

---

## Module 7 Practice Questions

**Q7.1:** Convert this loop to a list comprehension:
```python
result = []
for ip in all_ips:
    if ip.startswith('10.'):
        result.append(ip)
```
```python
# Answer:
result = [ip for ip in all_ips if ip.startswith('10.')]
```

**Q7.2:** Write a dict comprehension that maps hostnames to their first character (R, S, F) for device type classification.

**Q7.3 Homework Script:** Write a script that uses `zip()` to combine three parallel lists (hostnames, IPs, models) into a list of dictionaries, then uses list comprehension to filter only Cisco ISR models, and uses `all()` to check if all filtered devices have IPs in the 10.x.x.x range.

# PART II: CODE ORGANIZATION

---

# Module 8: Functions

> 📚 **Sources:** PCC Ch 8 | PyNEng Ch 9 | Byers LP Wk5

## Why This Module Matters

Functions are how you organize code into reusable, testable blocks. Without functions, you'd copy-paste the same 20 lines of code every time you need to connect to a device or parse output. With functions, you write the logic once and call it wherever needed.

PCC teaches functions through pizza-ordering examples. PyNEng builds network config generators. Kirk Byers wraps netmiko operations in functions. Here we combine all three perspectives for complete understanding.

---

## 8.1 Defining and Calling Functions

```python
# ---- PCC basic pattern (Ch 8) ----
def greet_user():
    """Display a simple greeting."""
    print("Hello!")

greet_user()   # Call the function

# ---- PyNEng network pattern ----
def generate_vlan_config(vlan_id, vlan_name):
    """Generate Cisco VLAN configuration commands.
    
    Args:
        vlan_id (int): VLAN number (1-4094)
        vlan_name (str): Descriptive VLAN name
    
    Returns:
        list: Configuration commands
    """
    commands = [
        f'vlan {vlan_id}',
        f' name {vlan_name}',
    ]
    return commands

# Call the function
config = generate_vlan_config(100, 'MANAGEMENT')
print('\n'.join(config))
# vlan 100
#  name MANAGEMENT
```

### The Anatomy of a Function

```python
def function_name(parameter1, parameter2):   # ← Definition line
    """Docstring: Describes what the function does."""  # ← Documentation
    
    # Function body — the code that runs when called
    result = parameter1 + parameter2
    
    return result   # ← Return value (optional)

# TERMINOLOGY:
# parameter = variable name in the function DEFINITION
# argument  = actual value passed when CALLING the function
# return value = what the function sends back to the caller
```

---

## 8.2 Parameters and Arguments

### Positional Arguments

```python
# PCC teaches positional arguments with pets
def describe_pet(animal_type, pet_name):
    """Display information about a pet."""
    print(f"I have a {animal_type} named {pet_name}.")

describe_pet('hamster', 'harry')  # Order matters!
describe_pet('dog', 'willie')

# Network version: interface config
def configure_interface(interface, ip_address, subnet_mask):
    """Generate interface configuration."""
    return [
        f'interface {interface}',
        f' ip address {ip_address} {subnet_mask}',
        f' no shutdown',
    ]

config = configure_interface('GigabitEthernet0/0', '10.1.1.1', '255.255.255.0')
```

### Keyword Arguments

```python
# PCC shows that keyword args let you skip positional ordering
describe_pet(animal_type='hamster', pet_name='harry')
describe_pet(pet_name='willie', animal_type='dog')  # Order doesn't matter

# Network version — much clearer with many parameters
def configure_interface(interface, ip_address, subnet_mask,
                       description='', shutdown=False):
    commands = [f'interface {interface}']
    if description:
        commands.append(f' description {description}')
    commands.append(f' ip address {ip_address} {subnet_mask}')
    if shutdown:
        commands.append(' shutdown')
    else:
        commands.append(' no shutdown')
    return commands

# Using keyword arguments for clarity
config = configure_interface(
    interface='GigabitEthernet0/1',
    ip_address='10.2.2.1',
    subnet_mask='255.255.255.252',
    description='WAN Link to ISP',
    shutdown=False,
)
```

### Default Values

```python
# PCC pattern: default pizza topping
def make_pizza(topping='pineapple'):
    print(f"Have a {topping} pizza!")

make_pizza()            # Uses default: pineapple
make_pizza('mushroom')  # Override: mushroom

# Network pattern: default SSH parameters
def create_device_dict(host, username, password,
                       device_type='cisco_ios',
                       port=22,
                       timeout=30,
                       secret=''):
    """Create a netmiko-compatible device dictionary.
    
    Most devices use cisco_ios on port 22 with 30s timeout,
    so these are sensible defaults that reduce repetition.
    """
    device = {
        'device_type': device_type,
        'host': host,
        'username': username,
        'password': password,
        'port': port,
        'timeout': timeout,
    }
    if secret:
        device['secret'] = secret
    return device

# Only specify what differs from defaults
r1 = create_device_dict('10.0.0.1', 'admin', 'cisco123')
nexus = create_device_dict('10.0.0.10', 'admin', 'nxos123', device_type='cisco_nxos')
asa = create_device_dict('10.0.0.100', 'admin', 'asa123', device_type='cisco_asa', port=8443)
```

---

## 8.3 Return Values

```python
# A function can return any type of data

# Return a string
def get_hostname(config_text):
    """Extract hostname from running config."""
    for line in config_text.splitlines():
        if line.startswith('hostname'):
            return line.split()[1]
    return 'UNKNOWN'

# Return a list
def get_interfaces(config_text):
    """Extract all interface names from running config."""
    interfaces = []
    for line in config_text.splitlines():
        if line.startswith('interface '):
            interfaces.append(line.split()[1])
    return interfaces

# Return a dictionary
def parse_interface_line(line):
    """Parse one line of 'show ip interface brief' into a dict."""
    fields = line.split()
    return {
        'name': fields[0],
        'ip': fields[1],
        'status': fields[4],
        'protocol': fields[5],
    }

# Return multiple values (actually a tuple)
def analyze_interfaces(parsed_data):
    """Count up and down interfaces."""
    up = sum(1 for i in parsed_data if i['protocol'] == 'up')
    down = len(parsed_data) - up
    return up, down    # Returns a tuple

up_count, down_count = analyze_interfaces(my_data)   # Tuple unpacking
```

---

## 8.4 *args and **kwargs

This is crucial for understanding how netmiko's `ConnectHandler(**device)` works.

```python
# ---- *args: Collect extra positional arguments into a TUPLE ----
def send_commands(device_ip, *commands):
    """Send one or more commands to a device.
    *commands captures any number of additional arguments.
    """
    print(f"Connecting to {device_ip}")
    for cmd in commands:
        print(f"  Sending: {cmd}")
    print(f"  Total commands: {len(commands)}")

send_commands('10.1.1.1', 'show version')
send_commands('10.1.1.1', 'show ip route', 'show ip int brief', 'show cdp neighbors')

# ---- **kwargs: Collect extra keyword arguments into a DICT ----
def build_device_profile(hostname, **properties):
    """Build a device profile with flexible properties.
    **properties captures any keyword arguments as a dictionary.
    """
    profile = {'hostname': hostname}
    profile.update(properties)
    return profile

device = build_device_profile(
    'R1-CORE',
    ip='10.1.1.1',
    model='ISR4451',
    location='DC-1',
    role='core',
)
print(device)
# {'hostname': 'R1-CORE', 'ip': '10.1.1.1', 'model': 'ISR4451', 
#  'location': 'DC-1', 'role': 'core'}

# ---- ** unpacking (THIS is how netmiko works!) ----
device_params = {
    'device_type': 'cisco_ios',
    'host': '10.1.1.1',
    'username': 'admin',
    'password': 'cisco123',
}

# These two calls are IDENTICAL:
# ConnectHandler(**device_params)
# ConnectHandler(device_type='cisco_ios', host='10.1.1.1', username='admin', password='cisco123')
```

---

## 8.5 Practical Function: Complete Netmiko Wrapper

```python
from netmiko import ConnectHandler
from netmiko.exceptions import NetmikoTimeoutException, NetmikoAuthenticationException

def collect_device_info(device_params, commands=None):
    """Connect to a device and collect show command output.
    
    This is the pattern you'll use in almost every network automation script.
    It combines: PyNEng connection handling + PCC error handling + Byers structure.
    
    Args:
        device_params (dict): Netmiko connection dictionary
        commands (list): Show commands to execute. Defaults to common commands.
    
    Returns:
        dict: Hostname, status, and command outputs
    """
    if commands is None:
        commands = ['show version', 'show ip interface brief']
    
    hostname = device_params.get('hostname', device_params['host'])
    result = {
        'hostname': hostname,
        'host': device_params['host'],
        'status': 'UNKNOWN',
        'outputs': {},
        'error': None,
    }
    
    try:
        with ConnectHandler(**device_params) as ssh:
            ssh.enable()
            
            # Discover actual hostname from device
            prompt = ssh.find_prompt()
            result['hostname'] = prompt.strip('#>')
            
            # Execute each command
            for cmd in commands:
                output = ssh.send_command(cmd)
                result['outputs'][cmd] = output
            
            result['status'] = 'SUCCESS'
    
    except NetmikoTimeoutException:
        result['status'] = 'TIMEOUT'
        result['error'] = f"Cannot reach {device_params['host']}"
    
    except NetmikoAuthenticationException:
        result['status'] = 'AUTH_FAILED'
        result['error'] = f"Authentication failed for {device_params['host']}"
    
    except Exception as e:
        result['status'] = 'ERROR'
        result['error'] = str(e)
    
    return result
```

---

## Module 8 Practice Questions

**Q8.1:** What is the difference between a parameter and an argument?
```
Answer: A PARAMETER is the variable name in the function DEFINITION.
An ARGUMENT is the actual value you pass when CALLING the function.

def greet(name):        # 'name' is a parameter
    print(f"Hi {name}")

greet('Alice')          # 'Alice' is an argument
```

**Q8.2:** Why does `ConnectHandler(**device)` use `**`?
```
Answer: The ** operator UNPACKS a dictionary into keyword arguments.
So ConnectHandler(**{'host': '10.1.1.1', 'username': 'admin'}) becomes
ConnectHandler(host='10.1.1.1', username='admin').
This lets you build connection parameters as a dictionary (from YAML, etc.)
and pass them cleanly to netmiko.
```

**Q8.3 Homework Script:** Write a function `generate_trunk_config(interface, native_vlan, allowed_vlans)` that generates Cisco trunk port configuration. Test it with 3 different interfaces.

**Q8.4 Homework Script:** Write a function `ping_sweep(network, start, end)` that takes a network prefix and a range, generates a list of IPs, and returns two lists: reachable and unreachable (use subprocess to ping).

---

# Module 9: Modules & the Standard Library

> 📚 **Sources:** PCC Ch 8 (imports) | PyNEng Ch 11–12 | Byers LP Wk8

## 9.1 Importing Modules

```python
# ---- Import entire module ----
import os
print(os.getcwd())   # Current working directory

# ---- Import specific items ----
from pathlib import Path
from datetime import datetime

# ---- Import with alias ----
import json as j
import yaml as y

# ---- Module organization: your own modules ----
# File: network_utils.py
def classify_interface(status, protocol):
    """..."""
    pass

# File: main_script.py
from network_utils import classify_interface
```

## 9.2 Essential Standard Library Modules for Networking

```python
# ---- os module: file and directory operations ----
import os
os.makedirs('backups/2024', exist_ok=True)
files = os.listdir('backups/')
config_path = os.path.join('backups', '2024', 'R1.cfg')

# ---- subprocess: run system commands (ping!) ----
import subprocess

def ping_device(ip, count=3):
    result = subprocess.run(
        ['ping', '-c', str(count), '-W', '1', ip],
        capture_output=True, text=True
    )
    return result.returncode == 0

# ---- ipaddress: IP address math ----
import ipaddress

network = ipaddress.ip_network('10.1.0.0/24')
print(f"Network: {network.network_address}")
print(f"Broadcast: {network.broadcast_address}")
print(f"Netmask: {network.netmask}")
print(f"Usable hosts: {network.num_addresses - 2}")

# Check membership
ip = ipaddress.ip_address('10.1.0.50')
print(f"{ip} in {network}? {ip in network}")  # True

# Subnetting
for subnet in network.subnets(new_prefix=26):
    print(f"  {subnet} ({subnet.num_addresses - 2} hosts)")

# ---- datetime: timestamps for logging ----
from datetime import datetime
now = datetime.now()
timestamp = now.strftime('%Y%m%d_%H%M%S')
print(f"Backup filename: R1_{timestamp}.cfg")

# ---- difflib: compare configurations ----
import difflib

old_config = ['hostname R1', 'interface Gi0/0', ' ip address 10.1.1.1 255.255.255.0']
new_config = ['hostname R1-CORE', 'interface Gi0/0', ' ip address 10.2.2.1 255.255.255.0']

diff = difflib.unified_diff(old_config, new_config, fromfile='before', tofile='after', lineterm='')
print('\n'.join(diff))
```

---

# Module 10: File Input/Output & Exceptions

> 📚 **Sources:** PCC Ch 10 | PyNEng Ch 16 | Byers LP Wk2

## 10.1 Reading Files

```python
# ---- PCC modern approach: pathlib ----
from pathlib import Path
path = Path('router_config.txt')
contents = path.read_text()
lines = contents.splitlines()

# ---- PyNEng/Byers traditional approach: open() with context manager ----
# This is MORE COMMON in network automation scripts

# Read entire file
with open('router_config.txt', 'r') as f:
    config = f.read()

# Read line by line (memory efficient for large files)
with open('router_config.txt', 'r') as f:
    for line in f:
        line = line.rstrip()  # Remove trailing newline
        if line.startswith('interface'):
            print(line)

# Read all lines into a list
with open('router_config.txt', 'r') as f:
    lines = f.readlines()      # Each line includes \n
    lines = [l.strip() for l in lines]  # Clean up
```

## 10.2 Writing Files

```python
# Write a new file (overwrites if exists!)
commands = ['hostname R1-CORE', 'ip domain-name company.com', 'ip name-server 8.8.8.8']

with open('generated_config.txt', 'w') as f:
    for cmd in commands:
        f.write(cmd + '\n')

# Append to existing file
with open('audit_log.txt', 'a') as f:
    f.write(f"{datetime.now()} - Configuration backup completed\n")

# Write list to file efficiently
with open('vlan_list.txt', 'w') as f:
    f.write('\n'.join(str(v) for v in [10, 20, 30, 40, 100]))
```

## 10.3 Exception Handling

```python
# ---- PCC pattern: try/except/else ----
try:
    result = int(user_input) / int(divisor)
except ZeroDivisionError:
    print("Cannot divide by zero!")
except ValueError:
    print("Please enter valid numbers!")
else:
    print(f"Result: {result}")     # Only runs if NO exception occurred
finally:
    print("Calculation attempt finished")  # ALWAYS runs

# ---- Network automation exception pattern ----
from netmiko import ConnectHandler
from netmiko.exceptions import NetmikoTimeoutException, NetmikoAuthenticationException

def safe_connect(device):
    """Connect to device with comprehensive error handling."""
    hostname = device.get('hostname', device['host'])
    
    try:
        ssh = ConnectHandler(**device)
        ssh.enable()
        output = ssh.send_command('show version')
        ssh.disconnect()
        return {'hostname': hostname, 'status': 'OK', 'output': output}
    
    except NetmikoTimeoutException:
        return {'hostname': hostname, 'status': 'TIMEOUT', 'output': None}
    
    except NetmikoAuthenticationException:
        return {'hostname': hostname, 'status': 'AUTH_FAILED', 'output': None}
    
    except Exception as e:
        return {'hostname': hostname, 'status': f'ERROR: {e}', 'output': None}

# ---- File handling with exceptions ----
from pathlib import Path

def read_device_list(filename):
    """Read device list from file with error handling."""
    path = Path(filename)
    try:
        contents = path.read_text()
        return contents.strip().splitlines()
    except FileNotFoundError:
        print(f"ERROR: File '{filename}' not found!")
        return []
    except PermissionError:
        print(f"ERROR: No permission to read '{filename}'!")
        return []
```

---

## Module 10 Practice Questions

**Q10.1 Homework Script:** Write a configuration backup script that reads a list of device IPs from a file, connects to each one (simulated), saves the "config" to a timestamped file in a `backups/` directory, and logs success/failure to an audit log file.

---

# PART III: DATA PROCESSING

---

# Module 11: Regular Expressions

> 📚 **Sources:** PCC does not cover regex | PyNEng Ch 14–15 | Byers LP Wk4

## Why This Module Matters

Regular expressions (regex) are pattern-matching tools that let you extract structured data from unstructured text. Since Cisco CLI output is unstructured text, regex is essential for parsing it. Kirk Byers and PyNEng both dedicate significant time to regex because it's the foundation for more advanced parsing tools like TextFSM.

---

## 11.1 Regex Basics

```python
import re

# ---- The fundamental pattern elements ----
# \d     — any digit (0-9)
# \D     — any NON-digit
# \w     — any word character (letter, digit, underscore)
# \W     — any NON-word character
# \s     — any whitespace (space, tab, newline)
# \S     — any NON-whitespace
# .      — any character EXCEPT newline
# ^      — start of line
# $      — end of line
# +      — one or more of the previous
# *      — zero or more of the previous
# ?      — zero or one of the previous
# {n}    — exactly n of the previous
# {n,m}  — between n and m of the previous
# ()     — capture group
# (?P<name>)  — named capture group
# []     — character class (any one of these chars)
# |      — OR
# \      — escape special characters
```

## 11.2 The re Module Functions

```python
import re

# ---- re.search() — Find FIRST match ----
line = 'interface GigabitEthernet0/1'
match = re.search(r'(\S+Ethernet\d+/\d+)', line)
if match:
    print(match.group(1))  # 'GigabitEthernet0/1'

# ---- re.findall() — Find ALL matches ----
config = '''
ip address 10.1.1.1 255.255.255.0
ip address 10.2.2.1 255.255.255.252
ip address 192.168.1.1 255.255.255.0
'''
ips = re.findall(r'\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}', config)
print(ips)  # ['10.1.1.1', '255.255.255.0', '10.2.2.1', ...]

# Better: capture only the IP (not the mask) using groups
ip_lines = re.findall(r'ip address (\S+) (\S+)', config)
print(ip_lines)  # [('10.1.1.1', '255.255.255.0'), ...]

# ---- re.sub() — Search and Replace ----
old_config = 'ip name-server 8.8.8.8'
new_config = re.sub(r'8\.8\.8\.8', '1.1.1.1', old_config)
print(new_config)  # 'ip name-server 1.1.1.1'

# ---- re.split() — Split by pattern ----
output = 'Gi0/0   up   up   10.1.1.1'
fields = re.split(r'\s+', output.strip())
print(fields)  # ['Gi0/0', 'up', 'up', '10.1.1.1']

# ---- re.finditer() — Iterator of match objects (for named groups) ----
route_output = '''
O     10.1.1.0/24 [110/20] via 192.168.1.2, 00:05:32, GigabitEthernet0/1
O     10.2.2.0/24 [110/30] via 192.168.1.2, 00:05:32, GigabitEthernet0/1
S     172.16.0.0/16 [1/0] via 10.1.1.1
'''

pattern = r'(?P<proto>[OSCRB])\s+(?P<network>\S+)\s+\[(?P<ad>\d+)/(?P<metric>\d+)\]\s+via\s+(?P<nexthop>\S+)'

for match in re.finditer(pattern, route_output):
    print(f"  {match.group('proto'):3s} {match.group('network'):20s} "
          f"via {match.group('nexthop'):15s} AD/Metric: {match.group('ad')}/{match.group('metric')}")
```

## 11.3 Practical Regex Patterns for Network Engineers

```python
# ---- Common patterns you'll use repeatedly ----

# IPv4 address
IP_PATTERN = r'\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}'

# MAC address (Cisco format: xxxx.xxxx.xxxx)
MAC_CISCO = r'[0-9a-fA-F]{4}\.[0-9a-fA-F]{4}\.[0-9a-fA-F]{4}'

# Interface name
INTF_PATTERN = r'(?:Gi|Fa|Te|Hu|Lo|Vl|Po|Se)\S+'

# VLAN ID in various contexts
VLAN_PATTERN = r'[Vv]lan\s*(\d+)'

# Hostname from prompt
HOSTNAME_PATTERN = r'^(\S+)[#>]'

# ---- Parse MAC address table ----
mac_output = '''
  10   0050.7966.6800  DYNAMIC  Gi0/1
  20   0050.7966.6801  DYNAMIC  Gi0/2
  30   aabb.cc00.1100  DYNAMIC  Gi0/3
'''

pattern = r'(\d+)\s+(' + MAC_CISCO + r')\s+\S+\s+(\S+)'
for match in re.finditer(pattern, mac_output):
    vlan, mac, port = match.groups()
    print(f"  VLAN {vlan:5s} MAC {mac}  Port {port}")
```

---

## Module 11 Practice Questions

**Q11.1:** Write a regex to extract the OSPF neighbor ID and state from "show ip ospf neighbor" output.

**Q11.2:** Write a regex that matches Cisco interface names in both short (Gi0/1) and long (GigabitEthernet0/1) format.

**Q11.3 Homework Script:** Write a "log parser" that reads a Cisco syslog file and extracts all entries with severity 0-3 (Emergency through Error), printing the timestamp, severity, and message.

---

# Module 12: Data Formats – CSV, JSON & YAML

> 📚 **Sources:** PCC Ch 10 (JSON) | PyNEng Ch 17 | Byers LP Wk7

## 12.1 JSON – JavaScript Object Notation

```python
import json

# ---- Writing JSON ----
device_data = {
    'hostname': 'R1-CORE',
    'mgmt_ip': '10.255.0.1',
    'interfaces': [
        {'name': 'Gi0/0', 'ip': '192.168.1.1', 'status': 'up'},
        {'name': 'Gi0/1', 'ip': '10.1.1.1', 'status': 'up'},
    ],
    'vlans': [10, 20, 30],
}

# Write to file
with open('device.json', 'w') as f:
    json.dump(device_data, f, indent=2)

# Convert to string
json_string = json.dumps(device_data, indent=2)

# ---- Reading JSON ----
with open('device.json') as f:
    loaded = json.load(f)

print(loaded['hostname'])
for intf in loaded['interfaces']:
    print(f"  {intf['name']}: {intf['ip']}")
```

## 12.2 YAML – YAML Ain't Markup Language

```python
import yaml

# ---- Reading YAML (most common operation) ----
# devices.yaml:
# ---
# - hostname: R1-CORE
#   device_type: cisco_ios
#   host: 10.255.0.1
#   username: admin
#   password: cisco123
#
# - hostname: R2-DIST
#   device_type: cisco_ios
#   host: 10.255.0.2
#   username: admin
#   password: cisco123

with open('devices.yaml') as f:
    devices = yaml.safe_load(f)    # ALWAYS use safe_load, never load()!

for device in devices:
    print(f"  {device['hostname']:15s} {device['host']}")

# ---- Writing YAML ----
with open('output.yaml', 'w') as f:
    yaml.dump(devices, f, default_flow_style=False)
```

## 12.3 CSV – For Inventories and Reports

```python
import csv

# ---- Writing CSV ----
devices = [
    {'hostname': 'R1', 'ip': '10.0.0.1', 'model': 'ISR4451', 'site': 'NYC'},
    {'hostname': 'R2', 'ip': '10.0.0.2', 'model': 'CSR1000v', 'site': 'LAX'},
    {'hostname': 'SW1', 'ip': '10.0.0.10', 'model': 'C9300', 'site': 'NYC'},
]

with open('inventory.csv', 'w', newline='') as f:
    writer = csv.DictWriter(f, fieldnames=['hostname', 'ip', 'model', 'site'])
    writer.writeheader()
    writer.writerows(devices)

# ---- Reading CSV ----
with open('inventory.csv') as f:
    reader = csv.DictReader(f)
    for row in reader:
        print(f"  {row['hostname']:8s} {row['ip']:12s} {row['model']:10s} {row['site']}")
```

---

## Module 12 Practice Questions

**Q12.1:** When should you use JSON vs YAML vs CSV?
```
Answer:
- JSON: API responses, data exchange between programs, structured data storage
- YAML: Configuration files (Ansible, device parameters), human-readable data
- CSV: Spreadsheet-compatible data, device inventories, reports for non-programmers
```

**Q12.2 Homework Script:** Create a script that reads a CSV device inventory, connects to each device (simulated), collects "show version" output, and writes the results to a JSON file with timestamps.

# PART IV: OBJECT-ORIENTED PROGRAMMING

---

# Module 13: Classes & OOP

> 📚 **Sources:** PCC Ch 9 | PyNEng Ch 23–25 | Byers: implicit in netmiko's design

## Why This Module Matters

Object-Oriented Programming (OOP) lets you model real-world things as Python objects. A router has a hostname, an IP, interfaces, and can do things (show version, apply config). A class is the blueprint; an object is the actual router.

PCC teaches OOP through Car and Dog classes. PyNEng builds a NetworkDevice class. And netmiko itself is built with OOP — when you use `ConnectHandler()`, you're creating an object from a class.

---

## 13.1 Creating a Class

```python
# ---- PCC pattern: Dog class (Ch 9) ----
class Dog:
    """A simple attempt to represent a dog."""
    
    def __init__(self, name, age):
        """Initialize name and age attributes."""
        self.name = name
        self.age = age
    
    def sit(self):
        """Simulate a dog sitting."""
        print(f"{self.name} is now sitting.")
    
    def roll_over(self):
        """Simulate rolling over."""
        print(f"{self.name} rolled over!")

my_dog = Dog('Peso', 6)
print(f"My dog's name is {my_dog.name}.")
my_dog.sit()

# ---- Network pattern: CiscoDevice class (PyNEng Ch 23) ----
class CiscoDevice:
    """Represents a Cisco network device for automation."""
    
    def __init__(self, hostname, ip, username, password,
                 device_type='cisco_ios', secret=''):
        """Initialize device attributes."""
        self.hostname = hostname
        self.ip = ip
        self.username = username
        self.password = password
        self.device_type = device_type
        self.secret = secret
        self._connection = None    # Private attribute (by convention)
        self.connected = False
    
    def connect(self):
        """Establish SSH connection to the device."""
        from netmiko import ConnectHandler
        params = {
            'device_type': self.device_type,
            'host': self.ip,
            'username': self.username,
            'password': self.password,
            'secret': self.secret,
        }
        self._connection = ConnectHandler(**params)
        if self.secret:
            self._connection.enable()
        self.connected = True
        print(f"[{self.hostname}] Connected successfully")
        return self
    
    def send_show(self, command):
        """Send a show command and return the output."""
        if not self.connected:
            self.connect()
        return self._connection.send_command(command)
    
    def send_config(self, commands):
        """Send configuration commands."""
        if not self.connected:
            self.connect()
        if isinstance(commands, str):
            commands = [commands]
        return self._connection.send_config_set(commands)
    
    def save_config(self):
        """Save running config to startup."""
        if self.connected:
            self._connection.save_config()
            print(f"[{self.hostname}] Configuration saved")
    
    def disconnect(self):
        """Close SSH connection."""
        if self._connection:
            self._connection.disconnect()
            self.connected = False
            print(f"[{self.hostname}] Disconnected")
    
    def __repr__(self):
        """String representation for debugging."""
        status = 'connected' if self.connected else 'disconnected'
        return f"CiscoDevice('{self.hostname}', '{self.ip}', {status})"
    
    def __str__(self):
        """Human-readable string representation."""
        return f"{self.hostname} ({self.ip})"
    
    # Context manager support (PCC doesn't cover this, but it's important)
    def __enter__(self):
        """Enable 'with' statement usage."""
        self.connect()
        return self
    
    def __exit__(self, exc_type, exc_val, exc_tb):
        """Automatically disconnect when 'with' block ends."""
        self.disconnect()
        return False  # Don't suppress exceptions

# ---- Usage ----
# Method 1: Manual connect/disconnect
r1 = CiscoDevice('R1-CORE', '10.255.0.1', 'admin', 'cisco123', secret='enable123')
r1.connect()
print(r1.send_show('show version'))
r1.save_config()
r1.disconnect()

# Method 2: Context manager (recommended — auto-disconnects)
with CiscoDevice('R1-CORE', '10.255.0.1', 'admin', 'cisco123') as r1:
    version = r1.send_show('show version')
    r1.send_config(['interface Lo99', 'ip address 10.99.99.1 255.255.255.255'])
    r1.save_config()
# Automatically disconnected here
```

## 13.2 Inheritance

```python
# ---- PCC pattern: ElectricCar inherits from Car ----
# ---- Network pattern: CiscoSwitch inherits from CiscoDevice ----

class CiscoSwitch(CiscoDevice):
    """A Cisco switch with switching-specific methods."""
    
    def __init__(self, hostname, ip, username, password, **kwargs):
        super().__init__(hostname, ip, username, password, **kwargs)
        self.vlans = []
    
    def get_vlans(self):
        """Get VLAN information."""
        output = self.send_show('show vlan brief')
        return output
    
    def get_mac_table(self, vlan=None):
        """Get MAC address table."""
        cmd = f'show mac address-table vlan {vlan}' if vlan else 'show mac address-table'
        return self.send_show(cmd)
    
    def configure_access_port(self, interface, vlan_id, description=''):
        """Configure an access port."""
        commands = [
            f'interface {interface}',
            f' switchport mode access',
            f' switchport access vlan {vlan_id}',
            f' spanning-tree portfast',
        ]
        if description:
            commands.insert(1, f' description {description}')
        return self.send_config(commands)

class CiscoRouter(CiscoDevice):
    """A Cisco router with routing-specific methods."""
    
    def get_routes(self):
        return self.send_show('show ip route')
    
    def get_ospf_neighbors(self):
        return self.send_show('show ip ospf neighbor')
    
    def get_bgp_summary(self):
        return self.send_show('show ip bgp summary')

# Inheritance means CiscoSwitch has ALL CiscoDevice methods
# PLUS its own specialized methods
sw1 = CiscoSwitch('SW1', '10.0.0.10', 'admin', 'cisco')
# sw1.connect()         ← inherited from CiscoDevice
# sw1.send_show()       ← inherited from CiscoDevice
# sw1.get_vlans()       ← CiscoSwitch-specific
# sw1.get_mac_table()   ← CiscoSwitch-specific
```

---

# Module 14: Testing Your Code with Pytest

> 📚 **Sources:** PCC Ch 11 | PyNEng: pytest for exercises | Byers: —

## 14.1 Why Test?

Testing proves your code works correctly. When you modify a function, tests catch if you accidentally broke something. PCC uses pytest exclusively (replacing unittest from earlier editions).

```python
# ---- File: network_utils.py ----
def classify_interface(status, protocol):
    if status == 'up' and protocol == 'up':
        return 'HEALTHY'
    elif status == 'up' and protocol == 'down':
        return 'L3-ISSUE'
    elif 'administratively' in status:
        return 'ADMIN-DOWN'
    else:
        return 'DOWN'

def is_valid_vlan(vlan_id):
    return isinstance(vlan_id, int) and 1 <= vlan_id <= 4094

# ---- File: test_network_utils.py ----
from network_utils import classify_interface, is_valid_vlan

def test_healthy_interface():
    assert classify_interface('up', 'up') == 'HEALTHY'

def test_l3_issue():
    assert classify_interface('up', 'down') == 'L3-ISSUE'

def test_admin_down():
    assert classify_interface('administratively down', 'down') == 'ADMIN-DOWN'

def test_down():
    assert classify_interface('down', 'down') == 'DOWN'

def test_valid_vlan():
    assert is_valid_vlan(100) == True
    assert is_valid_vlan(1) == True
    assert is_valid_vlan(4094) == True

def test_invalid_vlan():
    assert is_valid_vlan(0) == False
    assert is_valid_vlan(4095) == False
    assert is_valid_vlan('100') == False

# ---- Using fixtures (PCC Ch 11) ----
import pytest

@pytest.fixture
def sample_device():
    return {
        'hostname': 'R1',
        'ip': '10.1.1.1',
        'interfaces': [
            {'name': 'Gi0/0', 'status': 'up', 'protocol': 'up'},
            {'name': 'Gi0/1', 'status': 'down', 'protocol': 'down'},
        ]
    }

def test_device_has_hostname(sample_device):
    assert sample_device['hostname'] == 'R1'

def test_device_interface_count(sample_device):
    assert len(sample_device['interfaces']) == 2
```

```bash
# Run tests
$ pytest test_network_utils.py -v
# test_network_utils.py::test_healthy_interface PASSED
# test_network_utils.py::test_l3_issue PASSED
# ... all PASSED
```

---

# PART V: NETWORK AUTOMATION

---

# Module 15: SSH/Telnet – Netmiko, Paramiko & Scrapli

> 📚 **Sources:** PCC: — | PyNEng Ch 18 | Byers LP Wk6 + Netmiko By Example Course Wk1–6

## Why This Module Matters

This is **THE module** — the reason most network engineers learn Python. Everything before this was building blocks; now you connect to real (or virtual) devices and automate real tasks.

Kirk Byers created Netmiko and his 12-lesson "Netmiko By Example" course is the definitive resource. PyNEng covers netmiko, paramiko, telnetlib, and scrapli. We combine both perspectives here.

---

## 15.1 The Netmiko Connection Lifecycle

```python
from netmiko import ConnectHandler

# ---- Step 1: Define device parameters ----
device = {
    'device_type': 'cisco_ios',
    'host': '192.168.1.1',
    'username': 'admin',
    'password': 'cisco123',
    'secret': 'enable123',
}

# ---- Step 2: Connect (context manager = best practice) ----
with ConnectHandler(**device) as ssh:
    
    # ---- Step 3: Enter enable mode ----
    ssh.enable()
    
    # ---- Step 4: Send show commands ----
    version = ssh.send_command('show version')
    interfaces = ssh.send_command('show ip interface brief')
    routes = ssh.send_command('show ip route')
    
    # ---- Step 5: Send configuration ----
    config_commands = [
        'interface Loopback99',
        'description AUTOMATED_BY_PYTHON',
        'ip address 10.99.99.1 255.255.255.255',
        'no shutdown',
    ]
    output = ssh.send_config_set(config_commands)
    
    # ---- Step 6: Verify the change ----
    verify = ssh.send_command('show ip interface brief | include Loopback99')
    print(verify)
    
    # ---- Step 7: Save config ----
    ssh.save_config()

# Connection automatically closed when 'with' block ends
```

## 15.2 Netmiko Methods Deep Dive

### send_command() — For Show Commands

```python
# Basic usage
output = ssh.send_command('show ip interface brief')

# With TextFSM parsing (returns list of dicts!)
# Requires: pip install ntc-templates
structured = ssh.send_command('show ip int brief', use_textfsm=True)
for entry in structured:
    print(f"  {entry['intf']:25s} {entry['ipaddr']:16s} {entry['status']}")

# With custom expect string (for commands with unusual prompts)
output = ssh.send_command('delete flash:old_file', expect_string=r'confirm')

# With delay factor (for slow commands)
output = ssh.send_command('show tech-support', delay_factor=4)
```

### send_config_set() — For Configuration Changes

```python
# List of commands
commands = [
    'interface GigabitEthernet0/1',
    'description Configured by Python',
    'switchport mode access',
    'switchport access vlan 10',
]
output = ssh.send_config_set(commands)

# From a file
output = ssh.send_config_from_file('configs/access_ports.txt')

# With error detection
output = ssh.send_config_set(commands, cmd_verify=True)
```

## 15.3 Paramiko — Lower-Level SSH (PyNEng Ch 18)

```python
import paramiko
import time

def send_show_paramiko(ip, username, password, command, enable_pass=''):
    """Send a show command using paramiko directly."""
    client = paramiko.SSHClient()
    client.set_missing_host_key_policy(paramiko.AutoAddPolicy())
    client.connect(ip, username=username, password=password, look_for_keys=False)
    
    shell = client.invoke_shell()
    shell.settimeout(10)
    time.sleep(1)
    shell.recv(65535)  # Clear the banner
    
    if enable_pass:
        shell.send('enable\n')
        time.sleep(1)
        shell.recv(65535)
        shell.send(enable_pass + '\n')
        time.sleep(1)
        shell.recv(65535)
    
    shell.send('terminal length 0\n')
    time.sleep(1)
    shell.recv(65535)
    
    shell.send(command + '\n')
    time.sleep(3)
    output = shell.recv(65535).decode('utf-8')
    
    client.close()
    return output
```

## 15.4 Multi-Device Automation Script

```python
#!/usr/bin/env python3
"""
Complete multi-device automation script.
Demonstrates the end-to-end pattern from all three sources.
"""

from netmiko import ConnectHandler
from netmiko.exceptions import NetmikoTimeoutException, NetmikoAuthenticationException
import yaml
import json
from datetime import datetime

def load_devices(filename='devices.yaml'):
    """Load device list from YAML file."""
    with open(filename) as f:
        return yaml.safe_load(f)

def collect_device_data(device_params):
    """Connect to one device and collect show command outputs."""
    hostname = device_params.pop('hostname', device_params['host'])
    result = {
        'hostname': hostname,
        'timestamp': datetime.now().isoformat(),
        'status': 'UNKNOWN',
    }
    
    try:
        with ConnectHandler(**device_params) as ssh:
            ssh.enable()
            result['version'] = ssh.send_command('show version')
            result['interfaces'] = ssh.send_command('show ip int brief', use_textfsm=True)
            result['routes'] = ssh.send_command('show ip route')
            result['status'] = 'SUCCESS'
            
    except NetmikoTimeoutException:
        result['status'] = 'TIMEOUT'
    except NetmikoAuthenticationException:
        result['status'] = 'AUTH_FAILED'
    except Exception as e:
        result['status'] = f'ERROR: {e}'
    
    return result

def save_results(results, filename='audit_results.json'):
    """Save collected data to JSON file."""
    with open(filename, 'w') as f:
        json.dump(results, f, indent=2, default=str)

def main():
    devices = load_devices()
    print(f"Loaded {len(devices)} devices\n")
    
    all_results = []
    for device in devices:
        hostname = device.get('hostname', device['host'])
        print(f"Processing {hostname}...", end=' ')
        result = collect_device_data(device.copy())
        all_results.append(result)
        print(result['status'])
    
    save_results(all_results)
    
    # Summary
    success = sum(1 for r in all_results if r['status'] == 'SUCCESS')
    print(f"\n{'='*50}")
    print(f"Results: {success}/{len(all_results)} devices successful")

if __name__ == '__main__':
    main()
```

---

# Module 16: Concurrent Connections to Multiple Devices

> 📚 **Sources:** PyNEng Ch 19 | Byers Paid Course Wk7

```python
from concurrent.futures import ThreadPoolExecutor, as_completed
from netmiko import ConnectHandler
import yaml

def get_device_version(device):
    """Collect version info from one device."""
    hostname = device.get('hostname', device['host'])
    try:
        with ConnectHandler(**device) as ssh:
            ssh.enable()
            output = ssh.send_command('show version | include uptime')
            return {'hostname': hostname, 'output': output.strip(), 'status': 'OK'}
    except Exception as e:
        return {'hostname': hostname, 'output': None, 'status': str(e)}

with open('devices.yaml') as f:
    devices = yaml.safe_load(f)

print(f"Connecting to {len(devices)} devices (10 concurrent)...\n")

with ThreadPoolExecutor(max_workers=10) as executor:
    futures = {executor.submit(get_device_version, d): d for d in devices}
    
    for future in as_completed(futures):
        result = future.result()
        symbol = '✓' if result['status'] == 'OK' else '✗'
        print(f"  {symbol} {result['hostname']:15s} {result.get('output', result['status'])}")
```

---

# Module 17: Jinja2 Configuration Templates

> 📚 **Sources:** PyNEng Ch 20 | Byers LP Wk7

## 17.1 Template Basics

```python
from jinja2 import Environment, FileSystemLoader

# ---- Template file: templates/router.j2 ----
# hostname {{ hostname }}
# !
# {% for intf in interfaces %}
# interface {{ intf.name }}
#  description {{ intf.description }}
#  ip address {{ intf.ip }} {{ intf.mask }}
#  {% if intf.ospf %}
#  ip ospf {{ intf.ospf.process }} area {{ intf.ospf.area }}
#  {% endif %}
#  {% if not intf.shutdown %}no shutdown{% else %}shutdown{% endif %}
# !
# {% endfor %}
# !
# {% if ospf %}
# router ospf {{ ospf.process_id }}
#  router-id {{ ospf.router_id }}
#  {% for network in ospf.networks %}
#  network {{ network.address }} {{ network.wildcard }} area {{ network.area }}
#  {% endfor %}
# {% endif %}
# !
# {% for ntp in ntp_servers %}
# ntp server {{ ntp }}
# {% endfor %}

# ---- Data (typically from YAML) ----
data = {
    'hostname': 'R1-BRANCH-NYC',
    'interfaces': [
        {
            'name': 'GigabitEthernet0/0',
            'description': 'WAN Uplink to ISP',
            'ip': '203.0.113.1',
            'mask': '255.255.255.252',
            'shutdown': False,
            'ospf': {'process': 1, 'area': 0},
        },
        {
            'name': 'GigabitEthernet0/1',
            'description': 'LAN - User Network',
            'ip': '10.1.0.1',
            'mask': '255.255.255.0',
            'shutdown': False,
            'ospf': {'process': 1, 'area': 0},
        },
    ],
    'ospf': {
        'process_id': 1,
        'router_id': '10.255.1.1',
        'networks': [
            {'address': '10.0.0.0', 'wildcard': '0.255.255.255', 'area': 0},
        ],
    },
    'ntp_servers': ['10.255.0.100', '10.255.0.101'],
}

# ---- Render ----
env = Environment(
    loader=FileSystemLoader('templates'),
    trim_blocks=True,
    lstrip_blocks=True,
)
template = env.get_template('router.j2')
config = template.render(data)
print(config)
```

## 17.2 Jinja2 Syntax Quick Reference

| Syntax | Purpose | Example |
|--------|---------|---------|
| `{{ variable }}` | Output a variable | `{{ hostname }}` |
| `{% for x in list %}` | Loop | `{% for v in vlans %}` |
| `{% if condition %}` | Conditional | `{% if vlan > 100 %}` |
| `{{ var \| filter }}` | Apply filter | `{{ hostname \| upper }}` |
| `{% set x = val %}` | Set variable | `{% set count = 0 %}` |
| `{# comment #}` | Template comment | `{# This won't render #}` |
| `{% include %}` | Include template | `{% include 'acl.j2' %}` |
| `{% block %}` | Template inheritance | `{% block content %}` |

---

## Module 15-17 Practice Questions

**Q15.1:** What are the TWO most important netmiko exceptions to catch and what do they mean?
```
Answer:
1. NetmikoTimeoutException — Device is unreachable (wrong IP, network issue, device down)
2. NetmikoAuthenticationException — Wrong username or password
```

**Q15.2:** What is the difference between `send_command()` and `send_config_set()`?
```
Answer:
- send_command() runs in EXEC mode (# prompt), for show commands,
  sends ONE command, waits for the prompt, returns the output
- send_config_set() runs in CONFIG mode (config)# prompt, for configuration,
  sends ONE or MORE commands, auto-enters and exits config mode
```

**Q15.3 Homework Script:** Write a "configuration deployer" that reads a Jinja2 template and a YAML data file, renders configs for 3 sites, then connects to each device and applies the configuration using netmiko.

**Q15.4 Homework Script:** Write a concurrent "health checker" that connects to 10 devices simultaneously, checks CPU utilization from "show processes cpu", and flags any device over 80%.

# Module 18: TextFSM & Output Parsing

> 📚 **Sources:** PyNEng Ch 21–22 | Byers Paid Course Wk5

## 18.1 Why TextFSM?

CLI output is unstructured text. TextFSM converts it to structured data (list of dictionaries) using template files.

```python
# ---- Writing a TextFSM Template ----
# File: show_ip_int_brief.textfsm
# Value INTERFACE (\S+)
# Value IPADDRESS (\S+)
# Value STATUS (up|down|administratively down)
# Value PROTOCOL (up|down)
#
# Start
#   ^${INTERFACE}\s+${IPADDRESS}\s+\w+\s+\w+\s+${STATUS}\s+${PROTOCOL} -> Record

# ---- Using TextFSM in Python ----
import textfsm

raw_output = """
Interface          IP-Address      OK? Method Status   Protocol
GigabitEthernet0/0 192.168.1.1     YES manual up       up
GigabitEthernet0/1 10.1.1.1        YES manual up       up
GigabitEthernet0/2 unassigned      YES unset  down     down
"""

with open('show_ip_int_brief.textfsm') as f:
    template = textfsm.TextFSM(f)
    result = template.ParseText(raw_output)

print(f"Headers: {template.header}")
for row in result:
    print(row)
# ['GigabitEthernet0/0', '192.168.1.1', 'up', 'up']
# ['GigabitEthernet0/1', '10.1.1.1', 'up', 'up']
# ['GigabitEthernet0/2', 'unassigned', 'down', 'down']

# ---- Netmiko + TextFSM (the easy way — Byers recommendation) ----
with ConnectHandler(**device) as ssh:
    # use_textfsm=True auto-selects the right template from ntc-templates
    structured = ssh.send_command('show ip int brief', use_textfsm=True)
    
    for entry in structured:
        print(f"  {entry['intf']:25s} {entry['ipaddr']:16s} {entry['status']}")
```

## 18.2 NTC Templates Library

```bash
# Install the pre-built template collection
pip install ntc-templates

# Contains 1000+ templates for Cisco, Arista, Juniper, etc.
# When you use use_textfsm=True, netmiko searches this library automatically
```

## 18.3 CiscoConfParse (PyNEng Ch 22)

```python
from ciscoconfparse import CiscoConfParse

config_text = """
interface GigabitEthernet0/0
 description WAN Uplink
 ip address 10.1.1.1 255.255.255.0
 no shutdown
!
interface GigabitEthernet0/1
 description User Network
 switchport mode access
 switchport access vlan 10
 shutdown
!
interface GigabitEthernet0/2
 description Server Network
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30
 no shutdown
"""

parse = CiscoConfParse(config_text.splitlines())

# Find all interfaces
for intf in parse.find_objects(r'^interface'):
    print(intf.text)

# Find shutdown interfaces
for intf in parse.find_objects_w_child(r'^interface', r'shutdown'):
    print(f"  SHUTDOWN: {intf.text}")

# Find interfaces with specific VLAN
for intf in parse.find_objects_w_child(r'^interface', r'vlan 10'):
    print(f"  VLAN 10: {intf.text}")
```

---

# Module 19: Databases with SQLite

> 📚 **Sources:** PyNEng Ch 26–27

## 19.1 Network Inventory Database

```python
import sqlite3
from datetime import datetime

# ---- Create Database ----
conn = sqlite3.connect('network_inventory.db')
cursor = conn.cursor()

cursor.execute('''
    CREATE TABLE IF NOT EXISTS devices (
        id INTEGER PRIMARY KEY AUTOINCREMENT,
        hostname TEXT NOT NULL UNIQUE,
        mgmt_ip TEXT NOT NULL,
        vendor TEXT DEFAULT 'Cisco',
        model TEXT,
        ios_version TEXT,
        serial_number TEXT,
        location TEXT,
        last_backup TIMESTAMP,
        last_seen TIMESTAMP DEFAULT CURRENT_TIMESTAMP
    )
''')

cursor.execute('''
    CREATE TABLE IF NOT EXISTS config_backups (
        id INTEGER PRIMARY KEY AUTOINCREMENT,
        device_id INTEGER,
        backup_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
        config_text TEXT,
        FOREIGN KEY (device_id) REFERENCES devices(id)
    )
''')

# ---- Insert devices ----
devices = [
    ('R1-CORE', '10.255.0.1', 'Cisco', 'ISR4451', '17.03.04', 'FTX1234', 'DC-1'),
    ('SW1-ACCESS', '10.255.0.10', 'Cisco', 'C9300', '17.06.03', 'FCW5678', 'Floor-2'),
    ('FW1', '10.255.0.100', 'Cisco', 'FTD2110', '7.2.0', 'JAD9012', 'DC-1'),
]

cursor.executemany('''
    INSERT OR REPLACE INTO devices 
    (hostname, mgmt_ip, vendor, model, ios_version, serial_number, location)
    VALUES (?, ?, ?, ?, ?, ?, ?)
''', devices)
conn.commit()

# ---- Query devices ----
cursor.execute("SELECT hostname, mgmt_ip, model FROM devices WHERE location = ?", ('DC-1',))
for row in cursor.fetchall():
    print(f"  {row[0]:15s} {row[1]:15s} {row[2]}")

# ---- Query with dict-like access ----
conn.row_factory = sqlite3.Row
cursor = conn.cursor()
cursor.execute("SELECT * FROM devices")
for row in cursor.fetchall():
    print(f"  {row['hostname']:15s} {row['mgmt_ip']:15s} v{row['ios_version']}")

conn.close()
```

---

# PART VI: CAPSTONE & REFERENCE

---

# Module 20: Capstone Projects, Practice Exam & Resources

## 20.1 Capstone Project 1: Network Configuration Backup System

This project combines: YAML (device list), Netmiko (SSH connections), File I/O (saving configs), Threading (concurrent connections), Logging, and Exception handling.

```python
#!/usr/bin/env python3
"""
Network Configuration Backup System
====================================
Backs up running configs from all devices to timestamped files.
Uses concurrent connections for speed.

Technologies used:
- YAML for device inventory (Module 12)
- Netmiko for SSH connections (Module 15)
- ThreadPoolExecutor for concurrency (Module 16)
- Exception handling (Module 10)
- File I/O (Module 10)
- Functions (Module 8)
- f-strings (Module 2)
- Dictionaries (Module 4)
"""

from concurrent.futures import ThreadPoolExecutor, as_completed
from netmiko import ConnectHandler
from netmiko.exceptions import NetmikoTimeoutException, NetmikoAuthenticationException
import yaml
import os
from datetime import datetime

# ---- Configuration ----
BACKUP_DIR = 'backups'
MAX_WORKERS = 10
DEVICE_FILE = 'devices.yaml'

def load_devices(filename):
    with open(filename) as f:
        return yaml.safe_load(f)

def backup_device(device_params):
    hostname = device_params.pop('hostname', device_params['host'])
    result = {'hostname': hostname, 'status': 'UNKNOWN', 'size': 0}
    
    try:
        with ConnectHandler(**device_params) as ssh:
            ssh.enable()
            config = ssh.send_command('show running-config')
            
            timestamp = datetime.now().strftime('%Y%m%d_%H%M%S')
            filename = os.path.join(BACKUP_DIR, f'{hostname}_{timestamp}.cfg')
            
            with open(filename, 'w') as f:
                f.write(config)
            
            result['status'] = 'SUCCESS'
            result['size'] = len(config)
            result['filename'] = filename
            
    except NetmikoTimeoutException:
        result['status'] = 'TIMEOUT'
    except NetmikoAuthenticationException:
        result['status'] = 'AUTH_FAILED'
    except Exception as e:
        result['status'] = f'ERROR: {e}'
    
    return result

def main():
    os.makedirs(BACKUP_DIR, exist_ok=True)
    devices = load_devices(DEVICE_FILE)
    
    print(f"{'='*60}")
    print(f"Network Configuration Backup System")
    print(f"Devices: {len(devices)} | Workers: {MAX_WORKERS}")
    print(f"{'='*60}\n")
    
    results = []
    with ThreadPoolExecutor(max_workers=MAX_WORKERS) as executor:
        futures = {executor.submit(backup_device, d.copy()): d for d in devices}
        for future in as_completed(futures):
            result = future.result()
            results.append(result)
            symbol = '✓' if result['status'] == 'SUCCESS' else '✗'
            size_str = f"({result['size']:,} bytes)" if result['size'] else ''
            print(f"  {symbol} {result['hostname']:20s} {result['status']} {size_str}")
    
    # Summary
    success = sum(1 for r in results if r['status'] == 'SUCCESS')
    print(f"\n{'='*60}")
    print(f"Complete: {success}/{len(results)} devices backed up successfully")
    print(f"Backup directory: {os.path.abspath(BACKUP_DIR)}/")

if __name__ == '__main__':
    main()
```

## 20.2 Capstone Project 2: VLAN Compliance Auditor

```python
#!/usr/bin/env python3
"""
VLAN Compliance Auditor
========================
Connects to all switches, collects VLAN info, compares against
a required standard, and generates a compliance report.

Technologies: Sets (Module 4), Netmiko (Module 15), Jinja2 (Module 17),
JSON output (Module 12), Functions (Module 8)
"""

from netmiko import ConnectHandler
import yaml, json, re
from datetime import datetime

def get_vlans_from_device(device_params):
    """Connect to switch and extract configured VLANs."""
    hostname = device_params.get('hostname', device_params['host'])
    try:
        with ConnectHandler(**device_params) as ssh:
            output = ssh.send_command('show vlan brief')
        
        vlans = set()
        for line in output.splitlines():
            match = re.match(r'^(\d+)\s+\S+\s+active', line)
            if match:
                vlans.add(int(match.group(1)))
        return {'hostname': hostname, 'vlans': vlans, 'status': 'OK'}
    except Exception as e:
        return {'hostname': hostname, 'vlans': set(), 'status': str(e)}

def audit_compliance(device_vlans, required_vlans, forbidden_vlans=None):
    """Check VLAN compliance for a single device."""
    if forbidden_vlans is None:
        forbidden_vlans = set()
    
    actual = device_vlans
    missing = required_vlans - actual
    unauthorized = actual & forbidden_vlans
    
    compliant = len(missing) == 0 and len(unauthorized) == 0
    score = ((len(required_vlans) - len(missing)) / len(required_vlans)) * 100
    
    return {
        'compliant': compliant,
        'score': round(score, 1),
        'missing_vlans': sorted(missing),
        'unauthorized_vlans': sorted(unauthorized),
    }

# ---- Main ----
required = {10, 20, 30, 40, 100, 999}
forbidden = {1}  # VLAN 1 should not be in use

with open('switches.yaml') as f:
    switches = yaml.safe_load(f)

print(f"\nVLAN Compliance Audit — {datetime.now().strftime('%Y-%m-%d %H:%M')}")
print(f"Required VLANs: {sorted(required)}")
print(f"Forbidden VLANs: {sorted(forbidden)}")
print(f"{'='*70}\n")

for sw in switches:
    result = get_vlans_from_device(sw)
    if result['status'] == 'OK':
        audit = audit_compliance(result['vlans'], required, forbidden)
        status = '✓ COMPLIANT' if audit['compliant'] else '✗ NON-COMPLIANT'
        print(f"  {result['hostname']:20s} {status} (Score: {audit['score']}%)")
        if audit['missing_vlans']:
            print(f"    Missing: {audit['missing_vlans']}")
        if audit['unauthorized_vlans']:
            print(f"    Unauthorized: {audit['unauthorized_vlans']}")
    else:
        print(f"  {result['hostname']:20s} ✗ UNREACHABLE ({result['status']})")
```

---

## 20.3 Comprehensive Practice Exam (50 Questions)

### Section A: Python Fundamentals (Questions 1–15)

**Q1.** What is the output of: `'10.1.1.1'.split('.')`?
> Answer: `['10', '1', '1', '1']`

**Q2.** What does `vlans[1:4]` return if `vlans = [10, 20, 30, 40, 50]`?
> Answer: `[20, 30, 40]` — slicing is [start:end) where end is exclusive

**Q3.** What is the difference between a list and a tuple?
> Answer: Lists are mutable (can be changed after creation); tuples are immutable (cannot be changed). Use lists for collections that grow/shrink, tuples for fixed data like connection parameters.

**Q4.** What does `device.get('serial', 'N/A')` return if 'serial' is not a key?
> Answer: `'N/A'` — the default value. `.get()` never raises KeyError.

**Q5.** What are the set operations to find: (a) common items, (b) items in A but not B, (c) all unique items?
> Answer: (a) `A & B` intersection (b) `A - B` difference (c) `A | B` union

**Q6.** Write a list comprehension to extract IPs starting with '10.' from a list.
> Answer: `[ip for ip in all_ips if ip.startswith('10.')]`

**Q7.** What is the difference between `append()` and `extend()`?
> Answer: `append(item)` adds ONE item (even if it's a list). `extend(list)` adds EACH item from the argument list individually.

**Q8.** What does `**device` do in `ConnectHandler(**device)`?
> Answer: Unpacks the dictionary into keyword arguments. `**{'host': '10.1.1.1', 'username': 'admin'}` becomes `host='10.1.1.1', username='admin'`.

**Q9.** What is a docstring and why should every function have one?
> Answer: A docstring is a string in triple quotes at the start of a function that describes what it does, its parameters, and return value. It appears when you use `help()` or `?` in IPython.

**Q10.** What will `int('10.5')` do?
> Answer: Raise a `ValueError`. Use `int(float('10.5'))` or just `float('10.5')` to get 10.5.

**Q11.** How do you safely read a YAML file?
> Answer: `yaml.safe_load(f)` — ALWAYS use `safe_load`, never `yaml.load()` which can execute arbitrary code.

**Q12.** What does `enumerate()` return and why is it useful?
> Answer: Returns tuples of (index, value). Useful when you need both the position and the item in a loop: `for i, line in enumerate(output)`.

**Q13.** What is the `with` statement and why use it for file operations?
> Answer: `with` creates a context manager that automatically handles cleanup (closing files, disconnecting SSH). If an exception occurs inside the `with` block, the file/connection still gets properly closed.

**Q14.** What is a raw string (r'...') and when do you need it?
> Answer: A raw string treats backslashes literally instead of as escape characters. Essential for regex patterns which use `\d`, `\s`, `\.` etc.

**Q15.** What does `if __name__ == '__main__':` do?
> Answer: Code inside this block only runs when the file is executed directly (not when imported as a module). It's the standard way to make Python files both importable and executable.

### Section B: Network Automation (Questions 16–35)

**Q16.** What are the required keys in a netmiko device dictionary?
> Answer: `device_type`, `host`, `username`, `password`

**Q17.** What is the difference between `send_command()` and `send_config_set()`?
> Answer: `send_command()` = EXEC mode, one show command, returns output. `send_config_set()` = CONFIG mode, multiple commands, auto enters/exits config terminal.

**Q18.** Name three netmiko device_type values for Cisco platforms.
> Answer: `cisco_ios`, `cisco_nxos`, `cisco_asa` (also: `cisco_xr`, `cisco_ios_telnet`)

**Q19.** What does `use_textfsm=True` do in `send_command()`?
> Answer: Automatically parses the raw CLI output using NTC Templates, returning a list of dictionaries instead of a raw string.

**Q20.** How do you handle a device that is unreachable in a netmiko script?
> Answer: Catch `NetmikoTimeoutException` in a try/except block.

**Q21.** What Jinja2 syntax outputs a variable? What syntax creates a loop?
> Answer: `{{ variable }}` for output. `{% for item in list %}...{% endfor %}` for loops.

**Q22.** Why use `ThreadPoolExecutor` instead of sequential connections?
> Answer: Concurrent connections are much faster. Connecting to 100 devices sequentially at 5 seconds each = 500 seconds. With 10 threads = ~50 seconds.

**Q23.** What is the maximum recommended `max_workers` for SSH connections?
> Answer: 10-20. Too many simultaneous SSH sessions can overwhelm devices and trigger security lockouts.

**Q24.** What Python library do you use to read YAML files?
> Answer: `pyyaml` (imported as `import yaml`)

**Q25.** Write a regex to match a Cisco MAC address (format xxxx.xxxx.xxxx).
> Answer: `r'[0-9a-fA-F]{4}\.[0-9a-fA-F]{4}\.[0-9a-fA-F]{4}'`

**Q26.** What does `ssh.save_config()` do in netmiko?
> Answer: Equivalent to `write memory` or `copy running-config startup-config` on the device.

**Q27.** How do you create a Jinja2 conditional that outputs "no shutdown" only if a variable is False?
> Answer: `{% if not shutdown %}no shutdown{% endif %}`

**Q28.** What module do you use for IP address math (subnetting, membership)?
> Answer: `ipaddress` (built-in standard library module)

**Q29.** What is the purpose of `.gitignore` in a network automation project?
> Answer: Prevents sensitive files (passwords, API keys, .env files) and unnecessary files (__pycache__, .pyc) from being committed to version control.

**Q30.** How do you compare VLANs between two switches using Python?
> Answer: Convert VLAN lists to sets, then use set operations: `sw1_vlans - sw2_vlans` for missing, `sw1_vlans & sw2_vlans` for common, `sw1_vlans ^ sw2_vlans` for mismatched.

**Q31.** What is the `json.dumps()` vs `json.dump()` difference?
> Answer: `json.dumps()` converts to a JSON string. `json.dump()` writes directly to a file object.

**Q32.** Write a function signature that accepts a hostname (required), IP (required), and any number of additional keyword arguments.
> Answer: `def create_device(hostname, ip, **kwargs):`

**Q33.** What does `ssh.find_prompt()` return?
> Answer: The current device prompt string (e.g., 'R1-CORE#' or 'R1-CORE>')

**Q34.** How do you read a CSV file into a list of dictionaries?
> Answer: `csv.DictReader(f)` — each row becomes a dictionary with column headers as keys.

**Q35.** What is CiscoConfParse used for?
> Answer: Parsing Cisco configuration files to find specific sections, parent/child relationships between config lines (e.g., find all interfaces with a specific VLAN configured).

### Section C: Coding Challenges (Questions 36–50)

**Q36.** Write a one-liner to get unique sorted VLANs from `[10, 20, 10, 30, 20]`.
> Answer: `sorted(set([10, 20, 10, 30, 20]))` → `[10, 20, 30]`

**Q37.** Write code to reverse an IP address (192.168.1.1 → 1.1.168.192).
> Answer: `'.'.join('192.168.1.1'.split('.')[::-1])`

**Q38.** Write a dict comprehension to create `{1: 2, 2: 4, 3: 8, 4: 16, 5: 32}`.
> Answer: `{n: 2**n for n in range(1, 6)}`

**Q39.** Write a function that takes a /24 network (e.g., '10.1.1.0/24') and returns the last usable IP.
> Answer:
```python
import ipaddress
def last_usable(network_str):
    net = ipaddress.ip_network(network_str, strict=False)
    return str(net.broadcast_address - 1)
# last_usable('10.1.1.0/24') → '10.1.1.254'
```

**Q40.** Write a script that generates VLAN config for VLANs 100-110 with names VLAN_100 through VLAN_110.
> Answer:
```python
for v in range(100, 111):
    print(f"vlan {v}")
    print(f" name VLAN_{v}")
```

**Q41–Q50:** See the homework scripts throughout this guide. Each module contains at least one complete homework script that can serve as exam preparation.

---

## 20.4 Essential Resource Links

| Resource | URL | What You Get |
|----------|-----|-------------|
| **Kirk Byers Free Course** | pynet.twb-tech.com/free-python-course.html | 10-week email course, exercises |
| **Kirk Byers Course Repo** | github.com/twin-bridges/python_course_mar26 | All course exercise files |
| **Netmiko By Example** | pynet.twb-tech.com/class-netmiko.html | 12-lesson deep dive into netmiko |
| **Kirk Byers Paid Course** | pynet.twb-tech.com/class-pyauto.html | 8-week advanced with lab environment |
| **PyNEng Online Book** | pyneng.readthedocs.io/en/latest/ | Complete free textbook |
| **PyNEng Exercises** | github.com/natenka/pyneng-examples-exercises | All book exercises with tests |
| **PCC Resources** | ehmatthes.github.io/pcc_3e | Cheat sheets, errata, updates |
| **Netmiko Source** | github.com/ktbyers/netmiko | Source code, examples, issues |
| **NTC Templates** | github.com/networktocode/ntc-templates | 1000+ TextFSM templates |
| **NAPALM** | github.com/napalm-automation/napalm | Multi-vendor abstraction |

---

## 20.5 Recommended Learning Path

### Month 1: Python Foundations
- **Week 1-2:** Modules 1-4 (Setup, Strings, Lists, Dicts)
- **Week 3:** Modules 5-7 (Control flow, Loops, Comprehensions)
- **Week 4:** Modules 8-10 (Functions, Modules, Files)
- Sign up for Kirk Byers' free 10-week course

### Month 2: Data Processing & OOP
- **Week 5:** Modules 11-12 (Regex, JSON/YAML/CSV)
- **Week 6:** Modules 13-14 (OOP, Testing)
- **Week 7-8:** Start PyNEng book exercises (Chapters 4-12)
- Complete Kirk Byers free course exercises

### Month 3: Network Automation
- **Week 9-10:** Module 15 (Netmiko deep dive)
- **Week 11:** Modules 16-17 (Concurrency, Jinja2)
- **Week 12:** Modules 18-19 (TextFSM, Databases)
- Consider enrolling in Kirk Byers' Netmiko By Example course

### Month 4: Mastery
- **Week 13-14:** Capstone projects
- **Week 15-16:** Build your own tools for your actual network
- Take the practice exam (Module 20)
- Start exploring NAPALM, Nornir, Ansible

---

## Final Notes

This guide was built by combining the best elements from three authoritative sources. Each source has strengths the others don't:

- **Python Crash Course** excels at explaining Python fundamentals clearly with progressive examples
- **PyNEng** is unmatched for Cisco-specific Python examples and exercises with automated testing
- **Kirk Byers' courses** provide the most practical, hands-on network automation training with real lab environments

Use all three together. When you encounter a concept you don't understand, check the corresponding chapter in each source — one of them will explain it in a way that clicks for you.

**Good luck on your Python journey — your network will thank you.**

---

*Sources: Python Crash Course 3rd Edition (Eric Matthes) | PyNEng (Natasha Samoylenko, pyneng.readthedocs.io) | Kirk Byers / Twin Bridges Technology (pynet.twb-tech.com) | github.com/twin-bridges/python_course_mar26*

---

# APPENDIX A: EXPANDED MODULE DEEP DIVES

This appendix provides the extended explanations, additional examples, and extra exercises needed to fully master each concept. Work through these after completing the main module content.

---

# Expanded Module 1: Environment Deep Dive

## Understanding How Python Executes Code

When you type `python3 script.py`, here's what actually happens step by step. Understanding this will help you debug problems later.

```
1. The Python interpreter reads your .py file
2. It compiles the code to bytecode (.pyc files in __pycache__)
3. The Python Virtual Machine (PVM) executes the bytecode
4. Output goes to stdout (your terminal)
```

This is different from compiled languages like C, where you compile first, then run a separate binary. Python is "interpreted" — but it actually does compile to bytecode internally. The `.pyc` files in `__pycache__/` are this compiled bytecode, which is why Python caches them for faster subsequent runs.

### The Python Path and Import System

When you type `import netmiko`, Python searches for the module in a specific order:

```python
import sys
print(sys.path)
# [
#   '',                          # Current directory
#   '/usr/lib/python3.10',       # Standard library
#   '/usr/lib/python3.10/lib-dynload',
#   '/home/user/venv/lib/python3.10/site-packages',  # Installed packages
# ]
```

This is why virtual environments work — they add their own `site-packages` directory to `sys.path`, so packages installed there are found before system packages.

### pip — The Package Manager In Depth

```bash
# Install a specific version
pip install netmiko==4.2.0

# Install minimum version
pip install "netmiko>=4.0"

# Upgrade an existing package
pip install --upgrade netmiko

# Show info about an installed package
pip show netmiko
# Name: netmiko
# Version: 4.2.0
# Summary: Multi-vendor library to simplify SSH connections
# Requires: paramiko, setuptools, ...

# List all installed packages
pip list

# List outdated packages
pip list --outdated

# Export current environment
pip freeze > requirements.txt

# Install from requirements file (replicate environment)
pip install -r requirements.txt

# Uninstall a package
pip uninstall netmiko
```

### Editor Configuration for Network Automation

**VS Code settings.json for Python/Network development:**

```json
{
    "python.defaultInterpreterPath": "~/netauto-env/bin/python3",
    "python.linting.pylintEnabled": true,
    "python.formatting.provider": "black",
    "editor.formatOnSave": true,
    "editor.rulers": [79, 120],
    "files.associations": {
        "*.j2": "jinja-html",
        "*.yaml": "yaml",
        "*.yml": "yaml"
    },
    "[python]": {
        "editor.tabSize": 4,
        "editor.insertSpaces": true
    }
}
```

### Git Branching Strategy for Network Automation

```
main (or production)
  │
  ├── develop
  │     ├── feature/vlan-audit
  │     ├── feature/backup-tool
  │     └── bugfix/timeout-handling
  │
  └── release/v1.0
```

```bash
# Real-world workflow
git checkout main
git pull origin main
git checkout -b feature/ospf-monitor

# ... do development work ...
git add .
git commit -m "Add OSPF neighbor monitoring script"
git commit -m "Add email alerting for neighbor state changes"
git commit -m "Add unit tests for OSPF parser"

# Push to remote for code review
git push origin feature/ospf-monitor

# After code review, merge to main
git checkout main
git merge feature/ospf-monitor
git push origin main
git branch -d feature/ospf-monitor
```

### Additional Module 1 Exercises

**Exercise 1.1:** Set up a complete development environment from scratch on a fresh Linux VM. Document every step in a README.md.

**Exercise 1.2:** Create a Git repository with three branches (main, develop, feature/test). Make commits on each branch, then merge feature into develop, then develop into main. Use `git log --oneline --graph --all` to visualize the history.

**Exercise 1.3:** Create a `requirements.txt` file that specifies exact versions of: netmiko, paramiko, jinja2, pyyaml, textfsm, pytest, ipython, and rich. Install them in a fresh virtual environment.

---

# Expanded Module 2: Strings & Numbers Deep Dive

## String Encoding and Unicode (PyNEng Ch 16)

Network devices can output text in various encodings. Understanding encoding prevents garbled output:

```python
# UTF-8 is the default in Python 3
text = "Ñoño"  # Spanish characters
print(type(text))      # <class 'str'> — always Unicode in Python 3

# Encoding: str → bytes
encoded = text.encode('utf-8')
print(encoded)          # b'\xc3\x91o\xc3\xb1o'
print(type(encoded))    # <class 'bytes'>

# Decoding: bytes → str
decoded = encoded.decode('utf-8')
print(decoded)          # Ñoño

# Network devices often send bytes — you need to decode
# raw_bytes = ssh_channel.recv(65535)
# text_output = raw_bytes.decode('utf-8')

# Common encoding issues and fixes:
try:
    output = raw_bytes.decode('utf-8')
except UnicodeDecodeError:
    output = raw_bytes.decode('latin-1')  # Fallback encoding
```

## Advanced String Operations

### String Translation Tables

```python
# Replace multiple characters at once (faster than chained replace)
table = str.maketrans({
    '\r': '',       # Remove carriage returns
    '\t': '    ',   # Replace tabs with 4 spaces
})
clean_output = raw_output.translate(table)
```

### Multi-line String Processing Pattern

```python
# The complete pattern for processing show command output
def parse_show_output(raw_output, skip_header=True, skip_empty=True):
    """Clean and split show command output into processable lines.
    
    This is the foundation pattern used in virtually every
    network parsing script.
    """
    lines = raw_output.strip().splitlines()
    
    if skip_header and lines:
        lines = lines[1:]  # Remove header line
    
    if skip_empty:
        lines = [line for line in lines if line.strip()]
    
    return lines

# Usage
raw = """
Interface          IP-Address      OK? Method Status   Protocol
GigabitEthernet0/0 192.168.1.1     YES manual up       up
GigabitEthernet0/1 10.1.1.1        YES manual up       up

GigabitEthernet0/2 unassigned      YES unset  down     down
"""

clean_lines = parse_show_output(raw)
for line in clean_lines:
    fields = line.split()
    print(f"  {fields[0]:25s} {fields[1]:16s} {fields[4]}/{fields[5]}")
```

### String Alignment for Professional Reports

```python
# Building formatted tables without external libraries
def print_table(headers, rows, col_widths=None):
    """Print a formatted ASCII table.
    
    This is extremely useful for generating readable reports
    from network data.
    """
    if col_widths is None:
        col_widths = [max(len(str(row[i])) for row in [headers] + rows) + 2
                      for i in range(len(headers))]
    
    # Header
    header_line = ''.join(h.ljust(w) for h, w in zip(headers, col_widths))
    separator = ''.join('-' * w for w in col_widths)
    print(header_line)
    print(separator)
    
    # Data rows
    for row in rows:
        print(''.join(str(val).ljust(w) for val, w in zip(row, col_widths)))

# Example usage
headers = ['Hostname', 'IP Address', 'Model', 'Version', 'Status']
data = [
    ['R1-CORE', '10.255.0.1', 'ISR4451', '17.03.04', 'Compliant'],
    ['R2-DIST', '10.255.0.2', 'CSR1000v', '16.12.04', 'NON-COMPLIANT'],
    ['SW1-ACC', '10.255.0.10', 'C9300', '17.06.03', 'Compliant'],
    ['FW1', '10.255.0.100', 'FTD2110', '7.2.0', 'Compliant'],
]
print_table(headers, data)
```

### Number Systems for Network Engineers

```python
# Binary, Octal, Hexadecimal — all critical for networking

# Binary (base 2) — subnet masks, ACL wildcard masks
print(bin(255))         # '0b11111111'
print(bin(240))         # '0b11110000'  ← /28 mask last octet
print(int('11111100', 2))  # 252  ← convert binary string to int

# Hexadecimal (base 16) — MAC addresses, IPv6
print(hex(255))         # '0xff'
print(hex(192))         # '0xc0'
print(int('ff', 16))   # 255
print(int('c0a80101', 16))  # 3232235777 ← 192.168.1.1 as a 32-bit integer

# Practical: Convert subnet mask to prefix length
def mask_to_prefix(mask):
    """Convert subnet mask to prefix length.
    Example: '255.255.255.0' → 24
    """
    binary = ''.join(bin(int(octet))[2:].zfill(8) for octet in mask.split('.'))
    return binary.count('1')

print(mask_to_prefix('255.255.255.0'))    # 24
print(mask_to_prefix('255.255.255.252'))  # 30
print(mask_to_prefix('255.255.240.0'))    # 20

# Practical: Convert prefix length to subnet mask
def prefix_to_mask(prefix):
    """Convert prefix length to subnet mask.
    Example: 24 → '255.255.255.0'
    """
    binary = '1' * prefix + '0' * (32 - prefix)
    octets = [str(int(binary[i:i+8], 2)) for i in range(0, 32, 8)]
    return '.'.join(octets)

print(prefix_to_mask(24))   # '255.255.255.0'
print(prefix_to_mask(30))   # '255.255.255.252'
print(prefix_to_mask(20))   # '255.255.240.0'

# Practical: Calculate wildcard mask from subnet mask
def wildcard_mask(subnet_mask):
    """Calculate wildcard mask (for OSPF, ACLs).
    Example: '255.255.255.0' → '0.0.0.255'
    """
    octets = [str(255 - int(o)) for o in subnet_mask.split('.')]
    return '.'.join(octets)

print(wildcard_mask('255.255.255.0'))    # '0.0.0.255'
print(wildcard_mask('255.255.255.252'))  # '0.0.0.3'
```

### Additional Module 2 Exercises

**Exercise 2.1:** Write a function `normalize_interface_name(short_name)` that converts short interface names to long format: 'Gi0/1' → 'GigabitEthernet0/1', 'Fa0/1' → 'FastEthernet0/1', 'Te0/1' → 'TenGigabitEthernet0/1', 'Lo0' → 'Loopback0'.

**Exercise 2.2:** Write a script that takes an IP address and subnet mask as input and calculates: network address, broadcast address, first usable IP, last usable IP, number of usable hosts, prefix length, and wildcard mask. Do this WITHOUT the ipaddress module (pure string/math operations).

**Exercise 2.3:** Parse the following `show version` output and extract: hostname, IOS version, uptime, serial number, and model number into a dictionary.

```
Cisco IOS XE Software, Version 17.03.04a
Cisco IOS Software [Amsterdam], ISR Software (UNIVERSALK9-M), Version 17.03.04a, RELEASE SOFTWARE
Technical Support: http://www.cisco.com/techsupport
...
R1-CORE uptime is 142 days, 7 hours, 23 minutes
...
Processor board ID FTX2137A0B1
...
Cisco ISR4451-X/K9 (2RU) processor with 1795072K/6147K bytes of memory.
```

---

# Expanded Module 3: Lists Deep Dive

## List Memory Model — Understanding References

This is one of the most important concepts to understand and one that trips up many beginners. PCC covers this in Ch 4, and it's critical for understanding why `copy = original` doesn't work as expected.

```python
# When you assign a list to a new variable, you create a REFERENCE,
# not a copy. Both variables point to the SAME list in memory.

original = [10, 20, 30]
reference = original      # Both point to same list!

# Proof: they share the same memory address
print(id(original))      # 140234567890 (some memory address)
print(id(reference))     # 140234567890 (SAME address!)

reference.append(40)
print(original)          # [10, 20, 30, 40] — CHANGED!

# This matters in network scripts when passing lists to functions:
def add_default_commands(commands):
    """WARNING: This modifies the original list!"""
    commands.append('end')
    commands.append('write memory')
    return commands

my_commands = ['interface Gi0/1', 'no shutdown']
add_default_commands(my_commands)
print(my_commands)  # ['interface Gi0/1', 'no shutdown', 'end', 'write memory']
# The original list was modified!

# SAFE version: work with a copy
def add_default_commands_safe(commands):
    """Returns a new list without modifying the original."""
    full_commands = commands.copy()  # or commands[:]
    full_commands.append('end')
    full_commands.append('write memory')
    return full_commands
```

## Sorting Complex Data

```python
# Sorting lists of dictionaries (VERY common with parsed network data)
devices = [
    {'hostname': 'SW2', 'ip': '10.0.0.12', 'uptime_days': 45},
    {'hostname': 'R1', 'ip': '10.0.0.1', 'uptime_days': 142},
    {'hostname': 'SW1', 'ip': '10.0.0.11', 'uptime_days': 200},
    {'hostname': 'R2', 'ip': '10.0.0.2', 'uptime_days': 30},
]

# Sort by hostname
by_name = sorted(devices, key=lambda d: d['hostname'])

# Sort by uptime (ascending)
by_uptime = sorted(devices, key=lambda d: d['uptime_days'])

# Sort by uptime (descending — longest first)
by_uptime_desc = sorted(devices, key=lambda d: d['uptime_days'], reverse=True)

# Sort by IP address numerically (not alphabetically!)
# '10.0.0.2' should come before '10.0.0.11'
import ipaddress
by_ip = sorted(devices, key=lambda d: ipaddress.ip_address(d['ip']))

# Multi-level sort: by device type (R before SW), then by hostname
def sort_key(device):
    name = device['hostname']
    # R devices first (0), then SW (1), then everything else (2)
    if name.startswith('R'):
        return (0, name)
    elif name.startswith('SW'):
        return (1, name)
    return (2, name)

by_type_name = sorted(devices, key=sort_key)
```

## List as a Stack and Queue

```python
# Stack (Last In, First Out) — like a stack of plates
# Use append() and pop()
undo_stack = []
undo_stack.append('Added VLAN 10')
undo_stack.append('Modified interface Gi0/1')
undo_stack.append('Changed hostname')

last_action = undo_stack.pop()  # 'Changed hostname'
print(f"Undoing: {last_action}")

# Queue (First In, First Out) — like a line at the store
# For efficiency, use collections.deque instead of list
from collections import deque
task_queue = deque()
task_queue.append('Backup R1')
task_queue.append('Backup R2')
task_queue.append('Backup SW1')

next_task = task_queue.popleft()  # 'Backup R1'
print(f"Processing: {next_task}")
```

### Additional Module 3 Exercises

**Exercise 3.1:** Write a function `paginate(items, page_size)` that breaks a long list into pages. Example: `paginate([1,2,3,4,5,6,7], 3)` returns `[[1,2,3], [4,5,6], [7]]`. Use this to display parsed interface data 10 rows at a time.

**Exercise 3.2:** Implement a "command history" feature using a list as a stack. The script should let users enter commands, show history, and undo the last command.

**Exercise 3.3:** Given two lists of interface configurations (before and after a change window), write a script that identifies: added interfaces, removed interfaces, and modified interfaces.

---

# Expanded Module 4: Dictionaries Deep Dive

## Dictionary Performance — Why Dicts Are Fast

Dictionaries use a hash table internally, which gives O(1) average time complexity for lookups. This means looking up `device['hostname']` takes the same amount of time whether your dictionary has 10 entries or 10 million. Lists, by contrast, take O(n) time for `in` checks — they get slower as the list grows.

```python
# This is why you should convert lists to dicts for repeated lookups:

# SLOW: searching a list of 10,000 devices
device_list = [{'hostname': f'R{i}', 'ip': f'10.0.{i//256}.{i%256}'} for i in range(10000)]
# Finding a device requires scanning the entire list
target = None
for d in device_list:
    if d['hostname'] == 'R5000':
        target = d
        break

# FAST: convert to a dict lookup
device_dict = {d['hostname']: d for d in device_list}
target = device_dict['R5000']  # Instant lookup!
```

## Advanced Dictionary Techniques

```python
# ---- defaultdict: auto-creates missing keys ----
from collections import defaultdict

# Group interfaces by status
interface_data = [
    ('Gi0/0', 'up'), ('Gi0/1', 'down'), ('Gi0/2', 'up'),
    ('Gi0/3', 'up'), ('Gi0/4', 'down'), ('Lo0', 'up'),
]

by_status = defaultdict(list)
for intf, status in interface_data:
    by_status[status].append(intf)

print(dict(by_status))
# {'up': ['Gi0/0', 'Gi0/2', 'Gi0/3', 'Lo0'], 'down': ['Gi0/1', 'Gi0/4']}

# ---- Counter: count occurrences ----
from collections import Counter

log_severities = ['WARNING', 'ERROR', 'INFO', 'WARNING', 'ERROR', 
                  'INFO', 'INFO', 'CRITICAL', 'WARNING']
counts = Counter(log_severities)
print(counts)
# Counter({'WARNING': 3, 'INFO': 3, 'ERROR': 2, 'CRITICAL': 1})
print(counts.most_common(2))
# [('WARNING', 3), ('INFO', 3)]

# ---- OrderedDict: remember insertion order ----
# Note: regular dicts maintain order since Python 3.7+
# OrderedDict is still useful for equality comparisons based on order

# ---- Merging dictionaries ----
# Python 3.9+ syntax
defaults = {'device_type': 'cisco_ios', 'port': 22, 'timeout': 30}
overrides = {'host': '10.1.1.1', 'port': 8022}
merged = defaults | overrides    # overrides win for duplicate keys
print(merged)
# {'device_type': 'cisco_ios', 'port': 8022, 'timeout': 30, 'host': '10.1.1.1'}

# Python 3.5+ syntax
merged = {**defaults, **overrides}  # Same result
```

### Additional Module 4 Exercises

**Exercise 4.1:** Build a "Network Device Database" using nested dictionaries. Store 5 devices with hostname, IP, model, interfaces (each with IP and status), and OSPF neighbors. Write functions to: (a) find a device by hostname, (b) list all interfaces across all devices with status 'down', (c) find which devices are OSPF neighbors of a given device.

**Exercise 4.2:** Write a "Configuration Diff Tool" that takes two dictionaries representing device configurations (before and after), and reports all keys that were added, removed, or changed.

**Exercise 4.3:** Create a function that "flattens" a nested dictionary into a single-level dictionary with dot-notation keys. Example: `{'routing': {'ospf': {'process': 1}}}` becomes `{'routing.ospf.process': 1}`.

---

# Expanded Module 5-7: Control Flow Deep Dive

## Pattern Matching (Python 3.10+ — match/case)

```python
# Python 3.10 introduced structural pattern matching
# This is like a more powerful switch/case statement

def handle_syslog(message):
    """Process syslog messages using pattern matching."""
    match message.split('-'):
        case [_, severity, facility, *rest] if int(severity) <= 2:
            return f"CRITICAL: {'-'.join(rest)}"
        case [_, severity, 'LINK', *rest]:
            return f"LINK EVENT: {'-'.join(rest)}"
        case [_, severity, 'OSPF', *rest]:
            return f"ROUTING EVENT: {'-'.join(rest)}"
        case _:
            return f"INFO: {message}"
```

## The Walrus Operator := (Python 3.8+)

```python
# Assignment expression — assign and test in one step
# Useful in while loops and if statements

# Without walrus operator:
line = input("Enter command: ")
while line != 'quit':
    print(f"Processing: {line}")
    line = input("Enter command: ")

# With walrus operator (cleaner):
while (line := input("Enter command: ")) != 'quit':
    print(f"Processing: {line}")

# In list comprehensions — process and filter
import re
lines = ['interface Gi0/0', 'description WAN', 'ip address 10.1.1.1 255.255.255.0', 'hostname R1']
ip_lines = [m.group(1) for line in lines if (m := re.search(r'ip address (\S+)', line))]
print(ip_lines)  # ['10.1.1.1']
```

## Generator Expressions vs List Comprehensions

```python
# List comprehension — creates the ENTIRE list in memory
all_ips = [f"10.1.1.{i}" for i in range(1, 255)]  # 254 strings in memory

# Generator expression — generates one item at a time (memory efficient)
all_ips_gen = (f"10.1.1.{i}" for i in range(1, 255))  # Nearly zero memory

# For large datasets, use generators:
# Check if ANY device in a huge list has a specific error
# This STOPS as soon as it finds one match (doesn't process all 10000)
has_critical = any(
    'CRITICAL' in entry['message']
    for entry in process_huge_log_file('syslog.log')
)
```

### Additional Module 5-7 Exercises

**Exercise 5.1:** Write an "ACL Rule Evaluator" function that takes a source IP, destination IP, and protocol, and checks them against a list of ACL rules (represented as dictionaries). Return 'permit' or 'deny'.

**Exercise 6.1:** Write a "Port Scanner" that uses a for loop with subprocess to check if TCP ports 22, 23, 80, 443, and 8443 are open on a given IP address.

**Exercise 7.1:** Given a list of 1000 syslog messages, use a generator expression with `Counter` to find the top 5 most frequent message types.

---

# Expanded Module 8: Functions Deep Dive

## Decorators — Functions That Modify Functions

```python
import time
import functools

def timer(func):
    """Decorator that measures function execution time.
    Extremely useful for benchmarking network operations.
    """
    @functools.wraps(func)
    def wrapper(*args, **kwargs):
        start = time.perf_counter()
        result = func(*args, **kwargs)
        elapsed = time.perf_counter() - start
        print(f"  [{func.__name__}] completed in {elapsed:.2f}s")
        return result
    return wrapper

def retry(max_attempts=3, delay=5):
    """Decorator that retries a function on failure.
    Perfect for network connections that may time out.
    """
    def decorator(func):
        @functools.wraps(func)
        def wrapper(*args, **kwargs):
            for attempt in range(1, max_attempts + 1):
                try:
                    return func(*args, **kwargs)
                except Exception as e:
                    if attempt < max_attempts:
                        print(f"  Attempt {attempt} failed: {e}. Retrying in {delay}s...")
                        time.sleep(delay)
                    else:
                        print(f"  All {max_attempts} attempts failed.")
                        raise
        return wrapper
    return decorator

# Usage:
@timer
@retry(max_attempts=3, delay=2)
def connect_and_collect(device):
    """Connect to device and collect version info."""
    from netmiko import ConnectHandler
    with ConnectHandler(**device) as ssh:
        return ssh.send_command('show version')

# When you call connect_and_collect(device), it automatically:
# 1. Retries up to 3 times on failure
# 2. Measures and prints execution time
```

## Closures and Factory Functions

```python
def make_config_generator(template_commands, defaults=None):
    """Factory function that creates specialized config generators.
    
    This pattern is useful when you have multiple config templates
    that share similar structure but different details.
    """
    if defaults is None:
        defaults = {}
    
    def generate(interface, **overrides):
        params = {**defaults, **overrides}
        commands = [f'interface {interface}']
        for cmd in template_commands:
            commands.append(' ' + cmd.format(**params))
        return commands
    
    return generate

# Create specialized generators
access_port = make_config_generator(
    ['switchport mode access', 'switchport access vlan {vlan}',
     'spanning-tree portfast', 'no shutdown'],
    defaults={'vlan': 10}
)

trunk_port = make_config_generator(
    ['switchport mode trunk', 'switchport trunk native vlan {native}',
     'switchport trunk allowed vlan {allowed}', 'no shutdown'],
    defaults={'native': 99, 'allowed': '10,20,30'}
)

# Use them
print('\n'.join(access_port('Gi0/1')))                    # Uses default VLAN 10
print('\n'.join(access_port('Gi0/2', vlan=20)))            # Override VLAN
print('\n'.join(trunk_port('Gi0/24', allowed='10,20,30,40')))
```

### Additional Module 8 Exercises

**Exercise 8.1:** Write a `@validate_ip` decorator that checks if the first argument to a function is a valid IPv4 address before executing the function.

**Exercise 8.2:** Write a factory function `make_device_connector(platform)` that returns a function pre-configured for a specific platform (cisco_ios, cisco_nxos, etc.).

**Exercise 8.3:** Write a recursive function that flattens a deeply nested data structure (any combination of dicts and lists) into a flat list of all leaf values.

---

# Expanded Module 11: Regex Deep Dive

## Regex for Common Cisco Outputs

```python
import re

# ---- Parse show ip ospf neighbor ----
ospf_output = """
Neighbor ID     Pri   State           Dead Time   Address         Interface
10.255.0.2        1   FULL/DR         00:00:38    192.168.1.2     GigabitEthernet0/0
10.255.0.3        1   FULL/BDR        00:00:35    192.168.2.2     GigabitEthernet0/1
10.255.0.4        1   2WAY/DROTHER    00:00:33    192.168.3.2     GigabitEthernet0/2
"""

ospf_pattern = r'(?P<neighbor>\d+\.\d+\.\d+\.\d+)\s+\d+\s+(?P<state>\S+)\s+\S+\s+(?P<address>\d+\.\d+\.\d+\.\d+)\s+(?P<interface>\S+)'

neighbors = []
for match in re.finditer(ospf_pattern, ospf_output):
    neighbors.append(match.groupdict())
    print(f"  Neighbor: {match.group('neighbor'):15s} State: {match.group('state'):15s} via {match.group('interface')}")

# ---- Parse show ip bgp summary ----
bgp_output = """
Neighbor        V    AS MsgRcvd MsgSent   TblVer  InQ OutQ Up/Down  State/PfxRcd
10.1.1.2        4 65001   10234   10222     1024    0    0 3d05h          125
10.2.2.2        4 65002    8765    8750     1024    0    0 1d12h          250
10.3.3.2        4 65003       0       0        0    0    0 never    Idle
"""

bgp_pattern = r'(?P<neighbor>\d+\.\d+\.\d+\.\d+)\s+\d+\s+(?P<as>\d+)\s+\d+\s+\d+\s+\d+\s+\d+\s+\d+\s+(?P<uptime>\S+)\s+(?P<state>\S+)'

for match in re.finditer(bgp_pattern, bgp_output):
    state = match.group('state')
    status = '✓' if state.isdigit() else f'✗ {state}'
    print(f"  BGP Peer {match.group('neighbor'):15s} AS{match.group('as'):6s} Up: {match.group('uptime'):8s} {status}")

# ---- Parse show interfaces for errors ----
intf_output = """
GigabitEthernet0/0 is up, line protocol is up
  5 minute input rate 125000 bits/sec, 95 packets/sec
  5 minute output rate 250000 bits/sec, 180 packets/sec
     12345 packets input, 1234567 bytes
     0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored
     23456 packets output, 2345678 bytes
     0 output errors, 0 collisions, 0 interface resets
"""

# Extract error counts
error_pattern = r'(\d+)\s+(input errors|output errors|CRC|collisions|interface resets)'
errors = re.findall(error_pattern, intf_output)
for count, error_type in errors:
    if int(count) > 0:
        print(f"  ⚠ {error_type}: {count}")
    else:
        print(f"  ✓ {error_type}: {count}")

# ---- Compile patterns for reuse (performance optimization) ----
IP_RE = re.compile(r'\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}')
MAC_RE = re.compile(r'[0-9a-fA-F]{4}\.[0-9a-fA-F]{4}\.[0-9a-fA-F]{4}')
INTF_RE = re.compile(r'(?:Gi|Fa|Te|Hu|Lo|Vl|Po|Se|Tw)\S+')

# Compiled patterns are faster when used multiple times
all_ips = IP_RE.findall(some_large_output)
all_macs = MAC_RE.findall(mac_table_output)
all_intfs = INTF_RE.findall(config_output)
```

### Additional Module 11 Exercises

**Exercise 11.1:** Write regex patterns to parse `show ip arp` output and extract: IP address, MAC address, and interface for each entry.

**Exercise 11.2:** Write a function that takes a Cisco running config as a string and extracts ALL IP addresses configured on interfaces, returning a dictionary of `{interface_name: ip_address}`.

**Exercise 11.3:** Write a "Syslog Severity Analyzer" that uses regex to parse syslog messages, extract the facility and severity level, and produce a summary count by severity.

---

# Expanded Module 15: Netmiko Deep Dive

## Netmiko Advanced Features (Byers Netmiko By Example Course)

### Session Logging

```python
# Log everything that happens in the SSH session
device = {
    'device_type': 'cisco_ios',
    'host': '10.1.1.1',
    'username': 'admin',
    'password': 'cisco123',
    'session_log': 'session_R1.log',        # Log to file
    'session_log_record_writes': True,       # Log what WE send too
    'session_log_file_mode': 'append',       # Don't overwrite
}

# The session log captures the ENTIRE SSH interaction
# Invaluable for debugging automation issues
```

### Handling Different Prompt Types

```python
# Some commands have confirmation prompts
# Use send_command_timing for these

# Delete a file (asks "Delete flash:old.bin? [confirm]")
output = ssh.send_command_timing('delete flash:old.bin')
if 'confirm' in output:
    output += ssh.send_command_timing('y')

# Reload (asks "Proceed with reload? [confirm]")
output = ssh.send_command_timing('reload')
if 'confirm' in output.lower() or 'proceed' in output.lower():
    output += ssh.send_command_timing('y')

# Copy command (has multiple prompts)
output = ssh.send_command_timing('copy running-config tftp:')
output += ssh.send_command_timing('10.255.0.100')      # TFTP server
output += ssh.send_command_timing('R1-backup.cfg')      # Filename
output += ssh.send_command_timing('')                    # Confirm
```

### Configuration Rollback Pattern

```python
def apply_config_with_rollback(ssh, commands, verify_command, expected_output):
    """Apply configuration with automatic rollback on failure.
    
    This is a production-ready pattern for safe config deployment.
    """
    # Step 1: Backup current config
    pre_config = ssh.send_command('show running-config')
    
    # Step 2: Apply new configuration
    print("  Applying configuration...")
    output = ssh.send_config_set(commands)
    
    # Step 3: Verify the change
    verify = ssh.send_command(verify_command)
    
    if expected_output in verify:
        print("  ✓ Verification passed")
        ssh.save_config()
        return True
    else:
        print("  ✗ Verification FAILED — rolling back!")
        # Rollback: re-apply original config
        # In practice, you might use 'configure replace' on IOS-XE
        rollback_cmds = [f'no {cmd}' for cmd in reversed(commands) if not cmd.startswith('interface')]
        ssh.send_config_set(rollback_cmds)
        return False
```

### Additional Module 15 Exercises

**Exercise 15.1:** Write a script that connects to a router, adds a static route, verifies it appears in the routing table, and rolls back if verification fails.

**Exercise 15.2:** Write a "Config Compliance Checker" that connects to multiple devices, checks specific configuration elements (NTP servers, logging config, banner), and generates a compliance report.

**Exercise 15.3:** Write a "Change Window Automation" script that: (a) takes a pre-change snapshot, (b) applies a list of changes from a YAML file, (c) takes a post-change snapshot, (d) compares before/after, and (e) offers rollback if the user is not satisfied.

---

# APPENDIX B: COMPLETE HOMEWORK SCRIPTS INDEX

| Script | Module | Description | Skills Tested |
|--------|--------|-------------|---------------|
| 1.1 | 1 | Setup verification script | venv, pip, imports |
| 2.1 | 2 | Interface description generator | strings, f-strings, input |
| 2.2 | 2 | Subnet calculator (no ipaddress) | string splitting, math, binary |
| 3.1 | 3 | 48-port access config generator | lists, loops, range |
| 3.2 | 3 | IP categorizer | lists, conditionals, sorting |
| 4.1 | 4 | Device inventory builder | dicts, nesting, iteration |
| 4.2 | 4 | VLAN compliance checker | sets, comparison operations |
| 5.1 | 5 | ACL rule evaluator | if/elif/else, functions |
| 6.1 | 6 | Port scanner | for loops, subprocess |
| 7.1 | 7 | Syslog analyzer | comprehensions, Counter |
| 8.1 | 8 | Trunk config function | functions, defaults, *args |
| 8.2 | 8 | Ping sweep tool | functions, subprocess |
| 10.1 | 10 | Config backup to files | file I/O, exceptions |
| 11.1 | 11 | ARP table parser | regex, re.finditer |
| 11.2 | 11 | Config IP extractor | regex, groupdict |
| 12.1 | 12 | CSV-to-JSON converter | csv, json, data formats |
| 13.1 | 13 | NetworkDevice class | OOP, inheritance |
| 14.1 | 14 | Test suite for utils | pytest, fixtures, assert |
| 15.1 | 15 | Multi-device collector | netmiko, error handling |
| 15.2 | 15 | Config compliance checker | netmiko, regex, YAML |
| 15.3 | 15 | Change window automation | netmiko, difflib, rollback |
| 16.1 | 16 | Concurrent health checker | ThreadPoolExecutor |
| 17.1 | 17 | Jinja2 site config generator | jinja2, YAML |
| 18.1 | 18 | TextFSM custom template | textfsm, parsing |
| 19.1 | 19 | SQLite inventory database | sqlite3, SQL |
| 20.1 | 20 | Full network audit tool | ALL modules combined |
| 20.2 | 20 | VLAN compliance auditor | ALL modules combined |

---

# APPENDIX C: PYTHON CHEAT SHEET QUICK REFERENCE

## Data Types at a Glance

```python
# String
hostname = 'R1-CORE'                  # Immutable, ordered sequence of characters

# Integer
vlan_id = 100                          # Whole numbers, unlimited precision

# Float
cpu = 45.7                             # Decimal numbers

# Boolean
is_up = True                           # True or False

# List
vlans = [10, 20, 30]                  # Mutable, ordered, allows duplicates

# Tuple
params = ('10.1.1.1', 22)            # Immutable, ordered, allows duplicates

# Dictionary
device = {'host': '10.1.1.1'}        # Mutable, key-value pairs, keys unique

# Set
unique = {10, 20, 30}                 # Mutable, unordered, NO duplicates

# None
result = None                          # Represents absence of a value
```

## Control Flow at a Glance

```python
# If/elif/else
if condition:
    pass
elif other_condition:
    pass
else:
    pass

# For loop
for item in iterable:
    pass

# While loop
while condition:
    pass

# Try/except
try:
    risky_code()
except SpecificError:
    handle_error()
else:
    on_success()
finally:
    always_runs()

# Comprehension
[expr for item in iterable if condition]
{key: val for item in iterable}
{expr for item in iterable}
```

## Common Operations at a Glance

```python
# String operations
s.split()          s.strip()           s.startswith(x)
s.replace(a, b)    s.upper()           s.lower()
s.find(x)          s.count(x)          '\n'.join(list)
f"{var}"           s.splitlines()      s.endswith(x)

# List operations
l.append(x)        l.extend(list)      l.insert(i, x)
l.remove(x)        l.pop(i)            l.sort()
l.reverse()        l.copy()            len(l)
sorted(l)          l[start:end]        l.index(x)

# Dict operations
d[key]             d.get(key, default) d.keys()
d.values()         d.items()           d.update(other)
d.pop(key)         d.setdefault(k, v)  del d[key]

# Set operations
a & b              a | b               a - b
a ^ b              a <= b              a.add(x)
```

---

*End of Master Python Study Guide*

*Total content: 20 Modules + 3 Appendices*
*Sources: Python Crash Course 3rd Ed (Matthes) | PyNEng (Samoylenko) | Kirk Byers / Twin Bridges*
*Repository: github.com/twin-bridges/python_course_mar26*
