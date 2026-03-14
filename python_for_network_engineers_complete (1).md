# Python for Network Engineers — The Complete Practical Guide

**A hands-on journey from zero to network automation mastery**

*Inspired by the PyNEng methodology, enriched with Twin Bridges & Netmiko course exercises, and culminating in real-world Cisco lab projects.*

---

## About This Book

This book teaches Python programming through the lens of network engineering. Every concept — from strings to classes, from file I/O to concurrency — is taught using examples drawn from the networking domain: IP addresses, VLAN lists, device inventories, firewall policies, show command output, and live device automation.

The book is structured in eight parts, mirroring the proven PyNEng curriculum by Natasha Samoylenko, but extends every section with practical code from Kirk Byers' Twin Bridges Python and Netmiko courses, the official Netmiko examples repository, and a complete capstone lab project from Jagadnag's LABATO-1010 workshop.

### Who This Book Is For

Network engineers with or without programming experience. All examples and exercises focus on network equipment. This book will be useful for anyone who wants to automate daily network tasks and wants to start coding but doesn't know how to approach it.

### How to Use This Book

Each chapter follows this pattern:

1. **Concept Explanation** — The Python concept in plain language, answering "why does this exist?" and "when would I use this?"
2. **Line-by-Line Code Walkthrough** — Every single line of code is explained. Nothing is glossed over.
3. **PyNEng-Style Network Example** — Networking-focused code demonstrating the concept
4. **Twin Bridges Course Script** — The same concept from Kirk Byers' live training, placed side-by-side
5. **"What If?" Questions** — Common questions a learner would ask, answered directly
6. **Practice Exercises** — Hands-on tasks you can run immediately

### Source Repositories

All scripts referenced in this book come from these public repositories:

- **Twin Bridges Python Course**: `https://github.com/twin-bridges/python_course_mar26.git`
- **Twin Bridges Netmiko Course**: `https://github.com/twin-bridges/netmiko_course.git`
- **Netmiko Examples**: `https://github.com/ktbyers/netmiko/blob/develop/EXAMPLES.md`
- **LABATO-1010 Capstone**: `https://github.com/jagadnag/labato_1010.git`

---

# PART I — Python Basics

*The first part of this book is dedicated to Python basics. It covers preparing a working environment, core syntax rules, data types, control flow, file operations, and foundational coding patterns — all through the lens of network engineering.*

---

## Chapter 1: Preparing for Work

### 1.1 Why Do We Need a Specific Setup?

Before writing any code, you need three things: an operating system that runs Python well, an editor that helps you write Python efficiently, and a Python installation that is isolated so you don't break anything.

**Why does this matter?** Think of it like setting up a lab before running network configurations. You wouldn't configure OSPF on a production router without first having a lab topology, a console connection, and a known-good baseline config. Programming is the same — your "lab" is your development environment.

### 1.2 Operating System and Editor

You can use Linux, macOS, or Windows to follow along with this book. All examples were tested on Linux (Ubuntu/Debian), but the concepts apply universally. We recommend Python 3.10+ (the book was tested on Python 3.11/3.12).

**Why Linux?** Most network automation runs on Linux servers (jump hosts, Ansible control nodes, CI/CD runners). Learning Python on Linux means the skills transfer directly to production. However, Python works identically on all operating systems — the code itself doesn't change.

**Why does the Python version matter?** Python evolves. New versions add features and fix bugs. Python 3.10 introduced "structural pattern matching" (like a `switch` statement). Python 3.12 improved error messages dramatically. Older versions (Python 2.x) are completely different and should never be used for new projects.

**What if I'm on Windows?** That's perfectly fine. Install Python from python.org, or better yet, install WSL (Windows Subsystem for Linux) to get a full Linux terminal inside Windows. Many network engineers use VS Code on Windows with "Remote-SSH" to connect to a Linux VM — this gives you the best of both worlds.

**Choosing an editor:**

- **VS Code** — The most popular choice. Free, lightweight, has an excellent Python extension with autocomplete, debugging, and a built-in terminal. If you're unsure, start here.
- **PyCharm** — A full-featured Python IDE by JetBrains. More powerful than VS Code for large projects, but heavier and has a steeper learning curve.
- **Vim/Nano** — Terminal editors. Useful when you're SSH'd into a jump host and need to edit a script directly. Not recommended as your primary editor when learning.

**What if I don't want to install anything?** You can use Google Colab (colab.research.google.com) or Replit (replit.com) to write Python in a web browser. However, you won't be able to connect to network devices from these environments, so you'll need a local setup eventually.

### 1.3 Python Interpreter — Your Interactive Sandbox

The Python interpreter (also called the REPL — Read, Eval, Print, Loop) is an interactive environment where you can type Python code and see results immediately. Think of it like the CLI of a router — you type a command, you get output.

**How to start it:**

```bash
$ python3
Python 3.12.3 (main, Apr  9 2024, 08:09:14) [GCC 13.2.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>>
```

**What is the `>>>` prompt?** It's Python's way of saying "I'm ready for your next command." Just like `Router#` means the router is in privileged exec mode, `>>>` means Python is in interactive mode waiting for input.

**Why use the interpreter?** It's the fastest way to test small ideas. Before writing a full script, you can try things out:

```python
>>> 2 + 2
4
>>> "hello" + " " + "world"
'hello world'
>>> len("192.168.1.1")
11
>>> "192.168.1.1".split(".")
['192', '168', '1', '1']
```

**What's the difference between the interpreter and a script?** The interpreter executes code line-by-line as you type it. A script is a `.py` file containing multiple lines of code that execute all at once when you run it. You'll use the interpreter for testing and scripts for automation.

**What if I get an error?** That's expected and normal. The interpreter will show you exactly what went wrong:

```python
>>> "hello" + 5
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: can only concatenate str (not "int") to str
```

**How to read this error:** Python is telling you that you tried to add a string (`"hello"`) and a number (`5`) together, which doesn't make sense. The last line (`TypeError: can only concatenate str (not "int") to str`) is the most important — it tells you exactly what went wrong. Always read error messages from the bottom up.

**How to exit the interpreter:**

```python
>>> exit()
```

Or press `Ctrl+D` on Linux/Mac, `Ctrl+Z` then Enter on Windows.

### 1.4 Virtual Environments — Why Isolation Matters

A virtual environment is an isolated Python installation where you can install packages without affecting your system Python or other projects.

**Why do we need this?** Imagine you have two automation projects:
- Project A needs `netmiko==4.1.0`
- Project B needs `netmiko==4.3.0`

Without virtual environments, installing one version would break the other project. Virtual environments solve this by giving each project its own independent set of packages.

**Analogy for network engineers:** Virtual environments are like VRFs (Virtual Routing and Forwarding). Just as VRFs isolate routing tables so that two customers can use the same IP ranges without conflict, virtual environments isolate Python packages so that two projects can use different versions of the same library without conflict.

**How to create and use a virtual environment:**

```bash
# Step 1: Create a virtual environment named "netauto-venv"
$ python3 -m venv ~/netauto-venv
```

**What does this command do, piece by piece?**
- `python3` — Run the Python 3 interpreter
- `-m venv` — Run the built-in `venv` module (`-m` means "run this module as a script")
- `~/netauto-venv` — Create the virtual environment in your home directory in a folder called `netauto-venv`

```bash
# Step 2: Activate the virtual environment
$ source ~/netauto-venv/bin/activate
```

**What does "activate" do?** It modifies your shell's PATH so that when you type `python` or `pip`, it uses the versions inside the virtual environment instead of the system versions. You'll see your prompt change:

```bash
(netauto-venv) $
```

**That `(netauto-venv)` prefix is your indicator** that you're inside the virtual environment. It's like seeing `Router(config)#` — it tells you what "mode" you're in.

```bash
# Step 3: Install packages
(netauto-venv) $ pip install netmiko nornir pyyaml rich tabulate
```

**What is `pip`?** It's Python's package manager, like `apt` on Ubuntu or `yum` on CentOS. It downloads and installs Python packages from PyPI (the Python Package Index — think of it as the "app store" for Python libraries).

**What are these packages?**
- `netmiko` — Connects to network devices via SSH (Cisco, Arista, Juniper, etc.)
- `nornir` — A network automation framework (alternative to Ansible, but pure Python)
- `pyyaml` — Reads and writes YAML files (used by Ansible, Nornir, and many tools)
- `rich` — Makes terminal output look beautiful (colored text, tables, progress bars)
- `tabulate` — Creates formatted tables from data (for inventory reports)

```bash
# Step 4: Verify installation
(netauto-venv) $ pip list
```

This shows all installed packages and their versions.

```bash
# Step 5: Deactivate when done
(netauto-venv) $ deactivate
$
```

**What if I forget to activate my virtual environment?** Your script will fail with `ModuleNotFoundError` because the packages you installed are only available inside the virtual environment. This is the #1 beginner mistake — always check for the `(netauto-venv)` prefix before running scripts.

**What if I want to delete a virtual environment?** Just delete the folder:

```bash
$ rm -rf ~/netauto-venv
```

There's no "uninstall" process. The virtual environment is just a directory.

### 1.5 Your First Python Script

A Python script is a plain text file with a `.py` extension containing Python code. When you "run" the script, Python reads the file top-to-bottom and executes each line in order.

**Twin Bridges Course** (`class1/python_script/my_script.py`):

```python
#!/usr/bin/env python
print("Hello world")
```

**Line-by-line explanation:**

**Line 1: `#!/usr/bin/env python`**
This is called a "shebang" line (pronounced "sha-bang"). It tells Linux which program should execute this file. `/usr/bin/env python` means "find the `python` program in the system PATH and use it."

**Why is this needed?** On Linux, if you want to run a script directly (like `./my_script.py` instead of `python3 my_script.py`), the system needs to know which interpreter to use. The shebang line tells it. On Windows, this line is ignored — it doesn't hurt anything.

**What if I leave it out?** The script still works if you run it with `python3 my_script.py`. The shebang only matters for direct execution on Linux.

**Line 2: `print("Hello world")`**
This calls Python's built-in `print()` function, which outputs text to the terminal.

**What is a "function"?** A function is a named block of code that performs a specific action. `print()` is a function that takes whatever you put inside the parentheses and displays it on screen. We'll learn to create our own functions in Chapter 9.

**What are the parentheses for?** They tell Python "I'm calling this function." The value inside the parentheses is called an "argument" — it's the data you're passing to the function. In this case, `"Hello world"` is the argument.

**What are the quotes for?** The quotes define a "string" — a piece of text. Without quotes, Python would try to interpret `Hello` and `world` as variable names (and fail because they don't exist). Quotes say "this is literal text, not a command."

**How to run it:**

```bash
$ python3 my_script.py
Hello world
```

**What if I get `python: command not found`?** Try `python3` instead of `python`. On many Linux systems, `python` points to Python 2 (or doesn't exist), while `python3` points to Python 3.

**Network Engineer Version — Let's make it relevant:**

```python
#!/usr/bin/env python
"""My first network automation script."""

hostname = "core-rtr-01"
ip_address = "10.255.0.1"
vendor = "Cisco"
model = "CSR1000v"

print(f"Device: {hostname}")
print(f"IP: {ip_address}")
print(f"Vendor: {vendor}, Model: {model}")
```

**Line-by-line explanation:**

**Line 2: `"""My first network automation script."""`**
This is a "docstring" — a multi-line comment that describes what the script does. Triple quotes (`"""`) allow text to span multiple lines. Python ignores docstrings during execution, but tools can read them to generate documentation.

**Why use a docstring?** For the same reason you put descriptions on interfaces — so the next person (including future you) knows what this thing does.

**Line 4: `hostname = "core-rtr-01"`**
This creates a "variable" named `hostname` and assigns it the string value `"core-rtr-01"`.

**What is a variable?** A variable is a name that points to a value stored in memory. Think of it as a label on a box. The label is `hostname`, and inside the box is the text `"core-rtr-01"`. You can change what's in the box later, but the label stays the same.

**What does `=` mean?** In Python, `=` is the "assignment operator." It does NOT mean "equals" in the mathematical sense. It means "store the value on the right into the name on the left." So `hostname = "core-rtr-01"` means "create a variable called `hostname` and put the value `"core-rtr-01"` into it."

**What if I try to use a variable before assigning it?**

```python
>>> print(hostname)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'hostname' is not defined
```

Python will crash with a `NameError`. You must assign a value to a variable before using it.

**Lines 5-7:** Same pattern — creating more variables with different string values.

**Line 9: `print(f"Device: {hostname}")`**
This uses an "f-string" (formatted string literal). The `f` before the opening quote tells Python "this string contains expressions inside curly braces that should be evaluated."

**How does it work?**
1. Python sees `f"..."` and knows it's a formatted string
2. It finds `{hostname}` inside the string
3. It replaces `{hostname}` with the current value of the `hostname` variable
4. The result is `"Device: core-rtr-01"`
5. `print()` displays this on screen

**What if I forget the `f` prefix?**

```python
>>> print("Device: {hostname}")
Device: {hostname}
```

Without the `f`, Python treats `{hostname}` as literal text, not as a variable reference. This is a very common beginner mistake.

**What if the variable doesn't exist?**

```python
>>> print(f"Device: {nonexistent}")
NameError: name 'nonexistent' is not defined
```

Python will crash because it can't find a variable with that name.

**Expected output:**
```
Device: core-rtr-01
IP: 10.255.0.1
Vendor: Cisco, Model: CSR1000v
```

### 1.6 Git and GitHub — Version Control for Your Scripts

**Why do network engineers need Git?** For the same reason you keep backup configs — so you can see what changed, when it changed, who changed it, and roll back if something goes wrong. Git tracks every change to every file in your project.

**Analogy:** Git is like `archive` on a Cisco router, but for your automation scripts. Every time you "commit," you're saving a snapshot that you can return to later.

**Basic Git workflow:**

```bash
# Clone a repository (download it to your machine)
$ git clone https://github.com/twin-bridges/python_course_mar26.git
```

**What does `clone` do?** It creates a complete copy of the repository on your local machine, including all files and the entire history of changes.

```bash
# Check what's changed
$ git status
```

**What does `status` show?** It tells you which files have been modified, which are new (untracked), and which are staged for the next commit. Think of it as `show running-config` for your project — it shows the current state.

```bash
# Stage a file for commit
$ git add my_script.py
```

**What does "staging" mean?** It marks a file to be included in the next commit. Not all changes need to go into every commit — staging lets you choose which changes to save.

```bash
# Commit (save a snapshot)
$ git commit -m "Add first automation script"
```

**What is a commit?** A permanent snapshot of your project at this moment in time, with a message describing what changed. The `-m` flag lets you write the message inline.

**Why write good commit messages?** Because six months from now, when something breaks, you'll be reading these messages to figure out what changed. `"Add first automation script"` is useful. `"stuff"` is not.

```bash
# Push to remote (upload to GitHub)
$ git push origin main
```

**What if I make a mistake?** Git has many ways to undo changes. `git diff` shows what changed, `git checkout -- filename` discards changes to a file, and `git revert` creates a new commit that undoes a previous one. We won't cover advanced Git in this book, but knowing it's there gives you a safety net.

---

## Chapter 2: Python Syntax Basics — The Rules of the Language

### 2.1 Why Does Syntax Matter?

Every programming language has rules about how code must be written — just like every network protocol has rules about packet formats. If you send a malformed BGP UPDATE, the router rejects it. If you write malformed Python, the interpreter rejects it. Understanding syntax means understanding these rules.

### 2.2 Variables and Naming — The `snake_case` Convention

```python
# Good naming for network engineering
hostname = "core-rtr-01"
ip_address = "192.168.1.1"
vlan_id = 100
interface_name = "GigabitEthernet0/1"
is_connected = True
```

**Why `snake_case`?** Python has an official style guide called PEP 8 (Python Enhancement Proposal #8), written by the creator of Python. It says variable names should use lowercase letters with underscores between words. This is called `snake_case`.

**Why not `camelCase` or `PascalCase`?** Other languages use different conventions:
- **JavaScript** uses `camelCase`: `ipAddress`, `vlanId`
- **Java** uses `PascalCase` for classes: `NetworkDevice`, `VlanConfig`
- **Python** uses `snake_case`: `ip_address`, `vlan_id`

Following the convention makes your code readable to other Python developers. It's like using standard interface naming — everyone knows what `GigabitEthernet0/1` means because it follows a convention.

**What are the actual rules for variable names?**
1. Must start with a letter or underscore (`_`), never a number
2. Can contain letters, numbers, and underscores
3. Cannot be a Python keyword (`if`, `for`, `while`, `class`, etc.)
4. Are case-sensitive: `Hostname` and `hostname` are different variables

```python
# Valid names
router_1 = "R1"
_private = "internal"
my2ndDevice = "SW2"      # Valid, but not snake_case (avoid)

# Invalid names
# 1st_router = "R1"      # Cannot start with a number
# my-router = "R1"        # Hyphens are not allowed (Python thinks it's subtraction)
# class = "something"     # 'class' is a reserved keyword
```

**What if I use a bad variable name?**

```python
>>> 1st_router = "R1"
  File "<stdin>", line 1
    1st_router = "R1"
     ^
SyntaxError: invalid decimal literal
```

Python gives you a `SyntaxError` before the code even runs. It can't even begin to understand what you meant.

**What about hyphens?**

```python
>>> my-router = "R1"
  File "<stdin>", line 1
SyntaxError: cannot assign to expression here
```

Python interprets `my-router` as `my` minus `router` — a subtraction operation — not as a variable name. This is why we use underscores instead of hyphens.

**Best practices for naming in network automation:**

```python
# Descriptive names that tell you what the variable holds
device_ip = "10.0.0.1"          # Good — tells you it's an IP of a device
x = "10.0.0.1"                   # Bad — what is "x"?

device_list = ["10.0.0.1", "10.0.0.2"]  # Good
dl = ["10.0.0.1", "10.0.0.2"]            # Bad — what is "dl"?

is_reachable = True              # Good — boolean names start with is/has/can
flag = True                      # Bad — what flag?

MAX_RETRIES = 3                  # Good — UPPER_CASE for constants
max = 3                          # Bad — shadows the built-in max() function
```

**What is a "constant"?** A constant is a variable whose value should never change. Python doesn't enforce this (you CAN change it), but by convention, constants are written in `UPPER_CASE` to signal to other developers "don't modify this."

### 2.3 Comments — Explaining Your Intent

```python
# This is a single-line comment
# Python completely ignores everything after the # symbol

hostname = "core-rtr-01"  # This is an inline comment
```

**Why write comments?** Comments explain WHY your code does something, not WHAT it does. The code itself shows what it does. Comments explain the reasoning.

```python
# Bad comment — tells you what the code does (which is obvious)
vlan_id = 100  # Set vlan_id to 100

# Good comment — tells you WHY
vlan_id = 100  # Management VLAN per corporate standard SEC-2024-015

# Bad comment — obvious from the code
# Loop through devices
for device in device_list:
    ...

# Good comment — explains business logic
# Skip devices in maintenance window (ticket CHG-4521)
for device in device_list:
    if device in maintenance_devices:
        continue
    ...
```

**Analogy:** Comments are like interface descriptions on a switch. `description UPLINK-TO-CORE` is useful. `description THIS IS AN INTERFACE` is not.

**What about docstrings?**

```python
"""
This is a docstring.
It describes what a module, function, or class does.
Triple quotes allow multi-line text.
"""

def backup_device(hostname, ip):
    """Connect to a device and backup its running configuration.
    
    Args:
        hostname: The device hostname for naming the backup file.
        ip: The management IP address of the device.
    
    Returns:
        The file path of the saved backup.
    """
    # ... code here ...
```

**Why are docstrings different from comments?** Docstrings are part of the code — Python stores them and tools can read them. If you type `help(backup_device)` in the interpreter, Python will display the docstring. Comments are completely ignored by Python.

### 2.4 Indentation — Python's Most Important Syntax Rule

```python
if vlan_id == 100:
    print("Management VLAN")
    print("Check access policy")
else:
    print("User VLAN")
```

**Why does Python use indentation instead of braces `{}`?** This is a deliberate design choice by Python's creator, Guido van Rossum. In other languages (C, Java, JavaScript), code blocks are defined by curly braces:

```javascript
// JavaScript — braces define the block
if (vlan_id == 100) {
    console.log("Management VLAN");
    console.log("Check access policy");
}
```

In Python, the indentation IS the structure:

```python
# Python — indentation defines the block
if vlan_id == 100:
    print("Management VLAN")
    print("Check access policy")
```

**Why was this chosen?** Because programmers indent their code anyway for readability. Python simply makes it mandatory, ensuring that code looks the way it runs. There's no way to write "spaghetti code" where the indentation doesn't match the logic.

**How much indentation?** The standard is 4 spaces. Not 2 spaces, not 1 tab — exactly 4 spaces. Most editors can be configured to insert 4 spaces when you press the Tab key.

**What if I mix tabs and spaces?**

```python
if vlan_id == 100:
    print("This line uses 4 spaces")
	print("This line uses a tab")
```

```
TabError: inconsistent use of tabs and spaces in indentation
```

Python will refuse to run the code. This is actually helpful — it prevents subtle bugs where code looks correct but isn't.

**What if I get the indentation wrong?**

```python
if vlan_id == 100:
print("This line is not indented")
```

```
IndentationError: expected an indented block after 'if' statement
```

Python expected an indented block after the `if` statement (because of the colon `:`) but found code at the same indentation level.

**What does the colon `:` mean?** The colon at the end of an `if`, `for`, `while`, `def`, or `class` statement means "an indented block follows." It's Python's way of saying "the next lines belong to this statement."

**How does Python know where the block ends?** When the indentation returns to the previous level:

```python
if vlan_id == 100:
    print("This is inside the if block")      # 4 spaces in
    print("This is also inside the if block")  # 4 spaces in
print("This is OUTSIDE the if block")          # 0 spaces — back to base level
```

**What if I need nested blocks?** Each level adds 4 more spaces:

```python
for device in device_list:                        # Level 0
    print(f"Connecting to {device}")              # Level 1 (4 spaces)
    if device == "10.0.0.1":                      # Level 1
        print("This is the core router")          # Level 2 (8 spaces)
        if is_maintenance:                        # Level 2
            print("Skipping — in maintenance")    # Level 3 (12 spaces)
    print("Moving to next device")                # Level 1 (back to 4 spaces)
print("All done")                                 # Level 0 (back to 0 spaces)
```

**Analogy for network engineers:** Indentation in Python works like the hierarchical structure in Cisco IOS configuration:

```
router ospf 10                    ← Level 0 (the "statement")
 network 10.0.0.0 0.0.0.255 area 0    ← Level 1 (belongs to ospf 10)
 network 192.168.1.0 0.0.0.255 area 1 ← Level 1 (also belongs to ospf 10)
!
interface GigabitEthernet0/1      ← Level 0 (different statement)
 ip address 10.0.0.1 255.255.255.0    ← Level 1 (belongs to the interface)
```

In IOS, a single space of indentation means "this belongs to the previous command." In Python, 4 spaces of indentation means "this belongs to the previous statement."

### 2.5 The `print()` Function — Your First Debugging Tool

`print()` displays values to the terminal. It is the simplest and most frequently used debugging tool.

```python
# Print a string
print("Hello, Network Engineer!")

# Print a variable
hostname = "core-rtr-01"
print(hostname)

# Print multiple values (separated by spaces by default)
print("Device:", hostname, "is online")

# Print with a custom separator
print("10", "0", "0", "1", sep=".")    # Output: 10.0.0.1

# Print without a newline at the end
print("Loading", end="")
print(".", end="")
print(".", end="")
print(" Done!")
# Output: Loading.. Done!
```

**What does `print()` actually do?**
1. Takes one or more arguments (the values inside the parentheses)
2. Converts each value to a string (if it isn't already)
3. Joins them together with a separator (default is a space)
4. Adds a newline character (`\n`) at the end (unless you override with `end=""`)
5. Writes the result to "standard output" (your terminal)

**What if I print with no arguments?**

```python
>>> print()

>>>
```

It outputs a blank line. This is useful for visual spacing in your output.

**What if I try to print something that doesn't exist?**

```python
>>> print(undefined_variable)
NameError: name 'undefined_variable' is not defined
```

Python cannot print what doesn't exist. Define the variable first, then print it.

**What is `repr()`?** When debugging, `print()` can hide important details. The `repr()` function shows you the exact representation of a value:

```python
>>> line = "  hostname R1  \n"
>>> print(line)
  hostname R1  

>>> print(repr(line))
'  hostname R1  \n'
```

With `print()`, you can't see the leading spaces, trailing spaces, or newline character. With `repr()`, everything is visible. This is critical when debugging text parsing from network device output.

### 2.6 Python's Type System — Everything is an Object

In Python, every value has a "type" that determines what you can do with it:

```python
>>> type("hello")
<class 'str'>

>>> type(42)
<class 'int'>

>>> type(3.14)
<class 'float'>

>>> type(True)
<class 'bool'>

>>> type([1, 2, 3])
<class 'list'>

>>> type({"key": "value"})
<class 'dict'>
```

**Why do types matter?** Because different types support different operations:

```python
# Strings can be concatenated
>>> "Hello" + " " + "World"
'Hello World'

# Numbers can be added
>>> 10 + 20
30

# But you can't add a string and a number
>>> "VLAN" + 10
TypeError: can only concatenate str (not "int") to str
```

**How to convert between types:**

```python
# String to integer
>>> int("100")
100

# Integer to string
>>> str(100)
'100'

# String to float
>>> float("3.14")
3.14

# This is important! Data from files and user input is ALWAYS a string
>>> vlan_input = input("Enter VLAN: ")    # User types: 100
>>> type(vlan_input)
<class 'str'>                              # It's a string, not a number!
>>> vlan_id = int(vlan_input)              # Convert to integer
>>> type(vlan_id)
<class 'int'>                              # Now it's a number
```

**What if the conversion fails?**

```python
>>> int("hello")
ValueError: invalid literal for int() with base 10: 'hello'
```

You can't convert `"hello"` to a number because it's not a number. This is a `ValueError`, and you'll learn to handle it gracefully in Chapter 11 (Exception Handling).

**Why does this matter for networking?** When you read an IP address from a file, it's a string `"192.168.1.1"`, not four numbers. When you read a VLAN ID from user input, it's the string `"100"`, not the number `100`. You must convert types when needed.

---

## Chapter 3: Data Types — Numbers and Strings

### 3.1 Numbers — Counting and Calculating in Network Automation

Python has two main number types: **integers** (whole numbers) and **floats** (decimal numbers).

```python
vlan_id = 100                # int — a whole number, no decimal point
subnet_mask_bits = 24        # int
bandwidth_gbps = 10.5        # float — has a decimal point
packet_loss_percent = 0.02   # float
```

**Why two types?** Integers are exact. The number `100` is exactly `100`, always. Floats are approximations — the number `0.1` cannot be represented exactly in binary (just like 1/3 cannot be represented exactly in decimal). For most networking tasks, this doesn't matter, but it's important to know.

```python
>>> 0.1 + 0.2
0.30000000000000004    # Not exactly 0.3!
```

**When does this matter?** Almost never for network automation. But if you're doing financial calculations or comparing decimal values for equality, be aware of this.

**Arithmetic operations:**

```python
# Addition
total_vlans = 50 + 25        # 75

# Subtraction
available_ports = 48 - 3     # 45

# Multiplication
total_bandwidth = 4 * 10     # 40 (four 10G links)

# Division (always returns a float)
per_link = 100 / 4           # 25.0 (note: it's a float!)

# Integer division (drops the decimal)
per_link = 100 // 4          # 25 (integer)

# Modulo (remainder after division)
remainder = 100 % 3          # 1 (100 ÷ 3 = 33 remainder 1)

# Exponentiation (power)
subnet_hosts = 2 ** 8        # 256 (2 to the 8th power)
usable_hosts = 2 ** 8 - 2    # 254 (subtract network and broadcast)
```

**What is modulo `%` used for in networking?** It's surprisingly useful:

```python
# Check if a number is even or odd
>>> 10 % 2    # 0 means even
0
>>> 11 % 2    # 1 means odd
1

# Distribute devices across groups
device_number = 15
group = device_number % 4    # Group 3 (15 ÷ 4 = 3 remainder 3)
```

**What if I divide by zero?**

```python
>>> 10 / 0
ZeroDivisionError: division by zero
```

Python crashes. This can happen if you calculate something like "packets per device" when the device count is zero. You'll learn to handle this with try/except in Chapter 11.

**Comparing numbers:**

```python
>>> 10 == 10      # Equal?
True
>>> 10 != 20      # Not equal?
True
>>> 10 > 5        # Greater than?
True
>>> 10 < 5        # Less than?
False
>>> 10 >= 10      # Greater than or equal?
True
>>> 10 <= 5       # Less than or equal?
False
```

**Important: `==` vs `=`**
- `=` is assignment: "put this value into this variable"
- `==` is comparison: "are these two values equal?"

This is a common source of bugs:
```python
vlan_id = 100      # Assigns 100 to vlan_id
vlan_id == 100     # Checks if vlan_id equals 100 (returns True or False)
```

### 3.2 Strings — The Most Important Data Type for Network Engineers

**Why are strings the most important type?** Because network automation is fundamentally about working with text:

- Every CLI command you send is a string: `"show ip interface brief"`
- Every line of output you receive is a string: `"GigabitEthernet0/1   10.0.0.1   YES manual up   up"`
- Every configuration file is a collection of strings
- Every IP address is a string (until you parse it into numbers)
- Every hostname, interface name, VLAN name — all strings

If you master string operations, you can automate anything on a network device.

### 3.3 Creating Strings

There are multiple ways to create strings in Python. Each exists for a specific reason.

```python
# Single quotes
hostname = 'core-rtr-01'

# Double quotes
hostname = "core-rtr-01"

# These are identical — use whichever you prefer
```

**Why two types of quotes?** So you can include one type inside the other:

```python
# Need to include a single quote? Use double quotes outside
description = "It's the management interface"

# Need to include double quotes? Use single quotes outside
command = 'show interface "status"'

# What if you need both? Use escape characters
mixed = "He said \"it\'s working\""
```

**What is an escape character?** The backslash `\` tells Python "the next character is special, don't treat it normally."

```python
\n    — Newline (start a new line)
\t    — Tab
\\    — A literal backslash
\"    — A literal double quote inside a double-quoted string
\'    — A literal single quote inside a single-quoted string
```

```python
>>> print("Line 1\nLine 2\nLine 3")
Line 1
Line 2
Line 3

>>> print("Column1\tColumn2\tColumn3")
Column1	Column2	Column3
```

**Triple-quoted strings** — for multi-line text:

```python
show_output = """Interface              IP-Address      OK?
GigabitEthernet0/0     10.0.12.1       YES
GigabitEthernet0/1     10.0.13.1       YES
Loopback0              10.1.1.1        YES"""

print(show_output)
```

**Why triple quotes?** They preserve newlines and formatting exactly as written. This is invaluable for storing multi-line command output in variables for testing.

**What if I want to concatenate (join) strings?**

```python
# Method 1: The + operator
greeting = "Hello" + " " + "World"
# Result: "Hello World"

# Method 2: f-strings (preferred)
name = "World"
greeting = f"Hello {name}"
# Result: "Hello World"

# Method 3: The .join() method (for lists of strings)
parts = ["show", "ip", "interface", "brief"]
command = " ".join(parts)
# Result: "show ip interface brief"
```

**Which method should I use?**
- For combining a few known strings: use f-strings
- For combining a list of strings: use `.join()`
- For simple cases: `+` works fine

**What if I try to concatenate a string and a number?**

```python
>>> "VLAN" + 100
TypeError: can only concatenate str (not "int") to str
```

Python won't guess what you mean. You must explicitly convert:

```python
>>> "VLAN" + str(100)
'VLAN100'

# Or better, use an f-string (it converts automatically):
>>> f"VLAN{100}"
'VLAN100'
```

### 3.4 String Indexing and Slicing — Accessing Parts of a String

Every character in a string has a position number called an "index." **Indexing starts at 0, not 1.**

```python
hostname = "core-rtr-01"
#           c o r e - r t r - 0  1
# Index:    0 1 2 3 4 5 6 7 8 9 10
# Negative: -11 -10 -9 ...     -2 -1
```

**Why does indexing start at 0?** This is a convention from the C programming language that most modern languages follow. Think of the index as "how many positions from the start" — the first character is 0 positions from the start.

```python
>>> hostname = "core-rtr-01"
>>> hostname[0]       # First character
'c'
>>> hostname[4]       # Fifth character (index 4 = 5th position)
'-'
>>> hostname[-1]      # Last character
'1'
>>> hostname[-2]      # Second to last
'0'
```

**Why negative indexing?** Because you often need the last character, and you don't want to calculate `len(hostname) - 1` every time. `hostname[-1]` is cleaner and less error-prone.

**What if the index is out of range?**

```python
>>> hostname = "core-rtr-01"
>>> hostname[50]
IndexError: string index out of range
```

Python crashes because position 50 doesn't exist in an 11-character string.

**Slicing** extracts a substring:

```python
>>> hostname = "core-rtr-01"
>>> hostname[0:4]     # Characters from index 0 up to (NOT including) 4
'core'
>>> hostname[5:8]     # Characters from index 5 up to 8
'rtr'
>>> hostname[:4]      # From the start up to 4 (shorthand for [0:4])
'core'
>>> hostname[5:]      # From index 5 to the end
'rtr-01'
>>> hostname[-2:]     # Last 2 characters
'01'
```

**Why is the end index exclusive?** So that `hostname[:4] + hostname[4:]` equals `hostname`. This makes slicing math clean: the slice `[start:end]` contains `end - start` characters.

**Network application — Extracting hostname parts:**

```python
prompt = "core-rtr-01#"
hostname = prompt[:-1]    # Everything except the last character
print(hostname)           # "core-rtr-01"

# This is exactly what Netmiko's find_prompt() does, 
# and why the capstone project uses: hostname = net_connect.find_prompt()[:-1]
```

### 3.5 String Methods — Your Parsing Toolkit

Methods are actions you can perform on a string. They are called with dot notation: `string.method()`.

**Why are these important?** Because 90% of network automation is parsing text output from devices. String methods are your primary tools for this.

#### 3.5.1 `split()` — Breaking Strings Apart

`split()` divides a string into a list of parts based on a delimiter.

```python
>>> ip_addr = "192.168.1.1"
>>> ip_addr.split(".")
['192', '168', '1', '1']
```

**How does it work?**
1. Python scans the string from left to right
2. Every time it finds the delimiter (`"."`), it cuts the string at that point
3. The pieces go into a list
4. The delimiter itself is removed

**What if I don't pass an argument?**

```python
>>> "  show  ip   interface  brief  ".split()
['show', 'ip', 'interface', 'brief']
```

Without an argument, `split()` splits on ANY whitespace (spaces, tabs, newlines) and removes empty strings from the result. This is incredibly useful for parsing command output where columns are separated by varying amounts of whitespace.

**What if I split with an argument?**

```python
>>> "show  ip   interface  brief".split(" ")
['show', '', 'ip', '', '', 'interface', '', 'brief']
```

With a specific delimiter, `split(" ")` splits on EACH single space, creating empty strings between consecutive spaces. This is usually NOT what you want for parsing command output. Use `split()` without arguments instead.

**Network application — Parsing "show ip int brief" output:**

```python
line = "GigabitEthernet0/0     10.0.12.1       YES manual up         up"
fields = line.split()
print(fields)
# ['GigabitEthernet0/0', '10.0.12.1', 'YES', 'manual', 'up', 'up']

interface = fields[0]    # 'GigabitEthernet0/0'
ip = fields[1]           # '10.0.12.1'
status = fields[4]       # 'up'
protocol = fields[5]     # 'up'
```

**Twin Bridges Course** (`class1/strings/f_strings.py`) — Splitting an IP address and formatting:

```python
#!/usr/bin/env python

ip_addr = "142.251.141.110"
fields = ip_addr.split(".")
print(fields)
# Output: ['142', '251', '141', '110']
```

**Line-by-line explanation:**
- `ip_addr = "142.251.141.110"` — Create a string variable containing an IP address
- `fields = ip_addr.split(".")` — Split the IP on dots. This creates a list of 4 strings: `['142', '251', '141', '110']`
- `print(fields)` — Display the list

**What if the IP has no dots?**

```python
>>> "10001".split(".")
['10001']
```

If the delimiter isn't found, `split()` returns a list with the original string as its only element. It doesn't crash.

**Tuple unpacking with split:**

```python
octet1, octet2, octet3, octet4 = ip_addr.split(".")
```

**What is tuple unpacking?** When a function returns multiple values (or you have a list/tuple), you can assign each value to a separate variable in one line. The number of variables on the left MUST match the number of items on the right.

**What if they don't match?**

```python
>>> a, b = "10.0.0.1".split(".")
ValueError: too many values to unpack (expected 2)
```

There are 4 octets but only 2 variables. Python doesn't know which values to discard.

**Twin Bridges Exercise** (`class1/exercises/string_ex/strings_ex1.py`) — Full IP parsing example:

```python
#!/usr/bin/env python

ip_address = "198.51.100.0/24"
ipv6_address = "2001:db8:1:1::/64"

# Divide the network from the mask
ipv4_network, ipv4_mask = ip_address.split("/")
```

**Line-by-line:**
- `ip_address = "198.51.100.0/24"` — A CIDR notation IP address as a string
- `ipv4_network, ipv4_mask = ip_address.split("/")` — Split on `/`. The result is `['198.51.100.0', '24']`. Tuple unpacking assigns `'198.51.100.0'` to `ipv4_network` and `'24'` to `ipv4_mask`.

```python
# Obtain the octets
octet1, octet2, octet3, octet4 = ipv4_network.split(".")
```

Now `ipv4_network` is `'198.51.100.0'`. Splitting on `"."` gives `['198', '51', '100', '0']`, which unpacks into 4 variables.

```python
divider = "-" * 15
```

**What does `"-" * 15` do?** String multiplication repeats the string. `"-" * 15` creates `"---------------"` (15 dashes). This is useful for creating visual separators in output.

```python
print(f"{'octet1':^15} {'octet2':^15} {'octet3':^15} {'octet4':^15}")
print(f"{divider:15} {divider:15} {divider:15} {divider:15}")
print(f"{octet1:^15} {octet2:^15} {octet3:^15} {octet4:^15}")
```

**What does `:^15` mean in an f-string?** It's a format specification:
- `^` means center-align
- `15` means the total width is 15 characters
- So `{octet1:^15}` displays the value of `octet1` centered in a 15-character-wide field

Other alignment options:
- `<` left-align (default for strings)
- `>` right-align (default for numbers)
- `^` center-align

#### 3.5.2 `strip()` — Removing Whitespace

```python
>>> line = "  hostname R1  \n"
>>> line.strip()
'hostname R1'
```

**Why is this important?** Every line of output from a network device ends with a newline character `\n` (and sometimes has leading/trailing spaces). `strip()` removes all leading and trailing whitespace.

```python
>>> "  hello  ".strip()    # Remove both sides
'hello'
>>> "  hello  ".lstrip()   # Remove left side only
'hello  '
>>> "  hello  ".rstrip()   # Remove right side only
'  hello'
```

**When do you use it?** Almost always when reading lines from a file:

```python
with open('device_list') as f:
    for line in f:
        device_ip = line.strip()    # Remove the \n at the end
        print(device_ip)
```

**What if I don't strip?** Your IP addresses will have invisible newline characters attached: `"10.0.0.1\n"`. This will cause SSH connections to fail because `"10.0.0.1\n"` is not a valid hostname.

#### 3.5.3 `startswith()` and `endswith()` — Pattern Matching

```python
>>> "GigabitEthernet0/1".startswith("Gig")
True
>>> "GigabitEthernet0/1".startswith("Fast")
False
>>> "core-rtr-01.cfg".endswith(".cfg")
True
```

**Network application — Filtering interfaces by type:**

```python
interfaces = [
    "GigabitEthernet0/0",
    "GigabitEthernet0/1",
    "FastEthernet0/0",
    "Loopback0",
    "Loopback100",
]

# Find all Gigabit interfaces
gig_interfaces = []
for intf in interfaces:
    if intf.startswith("Gig"):
        gig_interfaces.append(intf)
print(gig_interfaces)
# ['GigabitEthernet0/0', 'GigabitEthernet0/1']

# Find all Loopback interfaces
loopbacks = [intf for intf in interfaces if intf.startswith("Loop")]
print(loopbacks)
# ['Loopback0', 'Loopback100']
```

#### 3.5.4 `replace()` — Search and Replace

```python
>>> "hostname OLD-ROUTER".replace("OLD-ROUTER", "NEW-ROUTER")
'hostname NEW-ROUTER'
```

**Why is this useful?** For config templates:

```python
template = """hostname DEVICE_NAME
interface Loopback0
 ip address LOOPBACK_IP 255.255.255.255
 description DEVICE_NAME management"""

config = template.replace("DEVICE_NAME", "core-rtr-01")
config = config.replace("LOOPBACK_IP", "10.255.0.1")
print(config)
```

**Output:**
```
hostname core-rtr-01
interface Loopback0
 ip address 10.255.0.1 255.255.255.255
 description core-rtr-01 management
```

**What if the search string isn't found?** Nothing happens. The original string is returned unchanged. No error.

```python
>>> "hello world".replace("xyz", "abc")
'hello world'    # Unchanged — "xyz" wasn't found
```

#### 3.5.5 `upper()`, `lower()`, `title()` — Case Conversion

```python
>>> "cisco".upper()
'CISCO'
>>> "CISCO".lower()
'cisco'
>>> "show ip interface brief".title()
'Show Ip Interface Brief'
```

**Network application — Case-insensitive comparison:**

```python
user_input = "Cisco"
if user_input.lower() == "cisco":
    print("Cisco device detected")
```

**Why convert to lowercase for comparison?** Because `"Cisco"`, `"cisco"`, `"CISCO"`, and `"CiScO"` should all match. Converting both sides to the same case ensures the comparison works regardless of how the user typed it.

#### 3.5.6 `join()` — Assembling Strings from Lists

```python
>>> vlans = ['10', '20', '30']
>>> ','.join(vlans)
'10,20,30'
```

**How does it work?** The string BEFORE `.join()` becomes the separator. The list INSIDE `.join()` provides the pieces. Python inserts the separator between each piece.

**Why is `join()` a string method and not a list method?** Because the separator is a string, and Python attaches the method to the type that controls the operation. The separator determines how the pieces are joined.

```python
# Different separators for different uses
>>> ' '.join(['show', 'ip', 'int', 'brief'])
'show ip int brief'

>>> '\n'.join(['line 1', 'line 2', 'line 3'])
'line 1\nline 2\nline 3'

>>> ', '.join(['R1', 'R2', 'R3'])
'R1, R2, R3'
```

**What if the list contains non-strings?**

```python
>>> ','.join([10, 20, 30])
TypeError: sequence item 0: expected str instance, int found
```

`join()` only works with strings. Convert numbers first:

```python
>>> vlans = [10, 20, 30]
>>> ','.join(str(v) for v in vlans)
'10,20,30'
```

#### 3.5.7 `count()`, `find()`, `in` — Searching Within Strings

```python
# count() — how many times does a substring appear?
>>> "up up down up".count("up")
3

# find() — where does the substring first appear? (-1 if not found)
>>> "GigabitEthernet0/1".find("Ethernet")
7

# 'in' operator — does the substring exist? (returns True/False)
>>> "up" in "Interface is up"
True
>>> "down" in "Interface is up"
False
```

**Which should I use?**
- Use `in` when you just need True/False (most common)
- Use `count()` when you need to know how many times
- Use `find()` when you need to know WHERE it appears

#### 3.5.8 `isdigit()`, `isalpha()` — Type Checking

```python
>>> "100".isdigit()      # Is it all digits?
True
>>> "VLAN100".isdigit()
False
>>> "VLAN".isalpha()     # Is it all letters?
True
>>> "VLAN100".isalpha()
False
>>> "VLAN100".isalnum()  # Is it all letters or digits?
True
```

**Network application — Validating user input:**

```python
user_input = input("Enter VLAN ID: ")
if user_input.isdigit():
    vlan_id = int(user_input)
    if 1 <= vlan_id <= 4094:
        print(f"Valid VLAN: {vlan_id}")
    else:
        print("VLAN must be between 1 and 4094")
else:
    print("Please enter a number")
```

### 3.6 String Formatting — Three Approaches

Python has evolved three ways to format strings. Understanding all three helps you read other people's code.

**Method 1: f-strings (Python 3.6+, RECOMMENDED)**

```python
hostname = "R1"
ip = "10.0.0.1"
print(f"Device {hostname} has IP {ip}")
# Output: Device R1 has IP 10.0.0.1
```

**Why are f-strings preferred?** They are the most readable — the variable names appear right where their values will be inserted.

**Method 2: `.format()` (Python 2.7+)**

```python
print("Device {} has IP {}".format(hostname, ip))
# Output: Device R1 has IP 10.0.0.1
```

**When do you see this?** In older code, or when the format string is stored separately from the data.

**Method 3: `%` operator (C-style, oldest)**

```python
print("Device %s has IP %s" % (hostname, ip))
# Output: Device R1 has IP 10.0.0.1
```

**When do you see this?** In very old Python code or code written by developers who came from C.

**Which should you use?** Always use f-strings for new code. Know the others so you can read existing code.

### 3.7 Strings are Immutable — What Does That Mean?

```python
>>> hostname = "core-rtr-01"
>>> hostname[0] = "C"
TypeError: 'str' object does not support item assignment
```

**What does "immutable" mean?** Once a string is created, you cannot change individual characters. This is a fundamental property of strings in Python.

**Then how do I modify strings?** You create a NEW string:

```python
>>> hostname = "core-rtr-01"
>>> new_hostname = "C" + hostname[1:]    # New string
>>> print(new_hostname)
'Core-rtr-01'

# Or use replace()
>>> hostname = hostname.replace("core", "CORE")
>>> print(hostname)
'CORE-rtr-01'
```

**What's actually happening?** When you write `hostname = hostname.replace(...)`, Python:
1. Creates a brand new string with the replacement applied
2. Points the variable `hostname` to this new string
3. The old string is eventually garbage-collected (deleted from memory)

The variable `hostname` now points to a different string object. The original string was never modified.

**Why does this matter?** Because string methods NEVER modify the original string. They always return a NEW string. This is a common source of confusion:

```python
>>> name = "  hostname R1  "
>>> name.strip()         # Returns a new string, but doesn't change 'name'
'hostname R1'
>>> print(name)          # 'name' is unchanged!
'  hostname R1  '

# You must assign the result back:
>>> name = name.strip()  # NOW name is updated
>>> print(name)
'hostname R1'
```

**This applies to ALL string methods:** `split()`, `replace()`, `upper()`, `lower()`, `strip()` — none of them modify the original string. They all return new strings.

---

## Chapter 4: Data Types — Lists, Dictionaries, Tuples, and Sets

### 4.1 Lists — Your Device Inventory

**What is a list?** A list is an ordered, mutable collection of items. Think of it as a spreadsheet column — items have a position (row number), you can add rows, remove rows, and change values.

**Why do network engineers need lists?** Because you constantly work with collections:
- A list of device IP addresses to connect to
- A list of VLANs to configure
- A list of interfaces to check
- A list of configuration commands to send

```python
vlans = [10, 20, 30, 40, 50]
```

**What do the square brackets `[]` mean?** Square brackets define a list. The items inside are separated by commas.

**Can a list contain different types?** Yes, but in practice, you usually store items of the same type:

```python
# Mixed types (valid but uncommon)
mixed = ["hello", 42, True, 3.14, None]

# Same types (recommended)
device_ips = ["10.0.0.1", "10.0.0.2", "10.0.0.3"]
vlan_ids = [10, 20, 30, 40]
```

**What is an empty list?**

```python
results = []    # An empty list — you'll add items later
```

**Why start with an empty list?** Because you often build lists dynamically:

```python
failed_devices = []
for device in all_devices:
    if not can_connect(device):
        failed_devices.append(device)
print(f"Failed: {failed_devices}")
```

#### 4.1.1 Accessing List Items

Lists use the same indexing as strings (starting at 0):

```python
devices = ["R1", "R2", "SW1", "SW2", "FW1"]
#           0      1     2      3      4
#          -5     -4    -3     -2     -1

>>> devices[0]       # First item
'R1'
>>> devices[-1]      # Last item
'FW1'
>>> devices[1:3]     # Slice: items at index 1 and 2 (not 3!)
['R2', 'SW1']
>>> devices[:2]      # First 2 items
['R1', 'R2']
>>> devices[2:]      # Everything from index 2 onward
['SW1', 'SW2', 'FW1']
```

**What if I access an index that doesn't exist?**

```python
>>> devices[10]
IndexError: list index out of range
```

Python crashes. Always check `len(devices)` if you're not sure how many items exist.

#### 4.1.2 Modifying Lists

**Unlike strings, lists ARE mutable — you CAN change them in place:**

```python
>>> devices = ["R1", "R2", "SW1"]
>>> devices[0] = "CORE-R1"       # Change first item
>>> print(devices)
['CORE-R1', 'R2', 'SW1']
```

**Why does this work for lists but not strings?** It's a design choice. Strings are immutable because they're used as dictionary keys and in many places where stability is needed. Lists are mutable because their primary purpose is to be modified — adding, removing, and changing items is what lists are for.

**Twin Bridges Course** (`class1/lists/list_ex.py`) — List basics:

```python
#!/usr/bin/env python

my_list = ["zzz", "world", "foo", 22, None]
```

**What is `None`?** It's Python's way of saying "no value" or "nothing." It's like a null value in a database. You use it when a variable exists but doesn't have a meaningful value yet.

```python
print(type(my_list))     # <class 'list'>
print(my_list)           # ['zzz', 'world', 'foo', 22, None]
print(my_list[0])        # 'zzz'
print(my_list[2])        # 'foo'
print(my_list[-1])       # None
```

**Why `print(type(my_list))`?** The `type()` function tells you what kind of object you're looking at. This is essential for debugging — if your code isn't working, the first question is "what type is this variable?"

```python
my_list[0] = "new value"       # Change index 0
print(my_list)                 # ['new value', 'world', 'foo', 22, None]

some_list = [42, "a string"]
my_list = my_list + some_list  # Concatenation creates a NEW list
print(my_list)
# ['new value', 'world', 'foo', 22, None, 42, 'a string']
```

**What does `+` do with lists?** It creates a new list containing all items from both lists. The original lists are not modified.

**What about `+=`?**

```python
my_list += some_list    # Equivalent to my_list.extend(some_list)
```

`+=` modifies `my_list` in place instead of creating a new list. This is a subtle but important difference.

#### 4.1.3 List Methods — Every Method Explained

**Twin Bridges Course** (`class1/lists/list_methods.py`):

```python
my_list = ["zzz", "world", "foo", 22, None]

# append() — Add ONE item to the END of the list
my_list.append(42)
print(my_list)
# ['zzz', 'world', 'foo', 22, None, 42]
```

**What does append() return?** Nothing (`None`). It modifies the list in place. This is a common mistake:

```python
# WRONG — result will be None
result = my_list.append(42)
print(result)    # None! Not the list!

# RIGHT — append modifies the list directly
my_list.append(42)
print(my_list)   # The list now has 42 at the end
```

**What if I append a list to a list?**

```python
>>> my_list = [1, 2, 3]
>>> my_list.append([4, 5])
>>> print(my_list)
[1, 2, 3, [4, 5]]    # A nested list! Not [1, 2, 3, 4, 5]
```

If you want to add the ITEMS of a list (not the list itself), use `extend()`:

```python
# extend() — Add ALL items from another list
some_list = [0, "hello"]
my_list.extend(some_list)
print(my_list)
# ['zzz', 'world', 'foo', 22, None, 42, 0, 'hello']
```

```python
# pop() — Remove and RETURN the last item (or item at index)
pop_val = my_list.pop()     # Remove last item
print(f"{pop_val=}")        # pop_val='hello'
print(f"{my_list=}")        # list without 'hello'

pop_val = my_list.pop(0)    # Remove item at index 0
print(f"{pop_val=}")        # pop_val='zzz'
print(f"{my_list=}")        # list without 'zzz'
```

**Why does `pop()` return the removed value?** So you can use it. For example, when processing a queue of tasks:

```python
pending_tasks = ["backup R1", "backup R2", "backup R3"]
while pending_tasks:
    task = pending_tasks.pop(0)    # Take the first task
    print(f"Processing: {task}")
```

```python
# insert() — Add an item at a specific position
my_list.insert(0, "first val")    # Insert at the beginning
print(f"{my_list=}")

# remove() — Remove the FIRST occurrence of a value
my_list.remove("foo")
print(f"{my_list=}")
```

**What if the value doesn't exist in the list?**

```python
>>> [1, 2, 3].remove(99)
ValueError: list.remove(x): x not in list
```

Python crashes. Check with `if 99 in my_list:` before removing, or use try/except.

**Other useful list operations:**

```python
>>> devices = ["R2", "R1", "SW2", "SW1"]

# Sort in place
>>> devices.sort()
>>> print(devices)
['R1', 'R2', 'SW1', 'SW2']

# Reverse in place
>>> devices.reverse()
>>> print(devices)
['SW2', 'SW1', 'R2', 'R1']

# Get length
>>> len(devices)
4

# Check membership
>>> "R1" in devices
True
>>> "FW1" in devices
False
```

#### 4.1.4 Reading a Device List from a File — The Critical Pattern

This pattern appears in EVERY script of the capstone project:

```python
with open('device_list') as f:
    device_list = f.read().splitlines()
```

**What does each part do?**

1. `open('device_list')` — Opens the file named `device_list` for reading
2. `as f` — Gives the file object the name `f`
3. `f.read()` — Reads the ENTIRE file into a single string
4. `.splitlines()` — Splits that string on newline characters, creating a list

**What's inside `device_list`?**
```
198.18.1.11
198.18.1.12
```

**What does `device_list` look like after?**
```python
['198.18.1.11', '198.18.1.12']
```

**What if I used `readlines()` instead of `read().splitlines()`?**

```python
>>> f.readlines()
['198.18.1.11\n', '198.18.1.12\n']    # Newlines included!
```

`readlines()` keeps the `\n` at the end of each line. `read().splitlines()` removes them. The second approach is almost always what you want.

### 4.2 Dictionaries — Your Device Connection Parameters

**What is a dictionary?** A dictionary stores key-value pairs. Think of it as a lookup table — given a key, you can instantly find its corresponding value.

**Why do network engineers need dictionaries?** Because network device data is naturally organized as key-value pairs:
- `hostname` → `"core-rtr-01"`
- `ip` → `"10.0.0.1"`
- `device_type` → `"cisco_ios"`
- `vendor` → `"Cisco"`

```python
ios_device = {
    'device_type': 'cisco_ios',
    'ip': '198.18.1.11',
    'username': 'cisco',
    'password': 'cisco',
}
```

**What do the curly braces `{}` mean?** They define a dictionary. Each entry is a `key: value` pair, separated by commas.

**What can be a key?** Strings, numbers, and tuples (anything "immutable"). In practice, keys are almost always strings.

**What can be a value?** Anything — strings, numbers, lists, other dictionaries, even functions.

#### 4.2.1 Accessing Dictionary Values

```python
>>> ios_device = {
...     'device_type': 'cisco_ios',
...     'ip': '198.18.1.11',
...     'username': 'cisco',
...     'password': 'cisco',
... }

>>> ios_device['ip']
'198.18.1.11'

>>> ios_device['device_type']
'cisco_ios'
```

**What if the key doesn't exist?**

```python
>>> ios_device['hostname']
KeyError: 'hostname'
```

Python crashes with a `KeyError`. This is different from lists (which give `IndexError`).

**How to avoid KeyError — the `get()` method:**

```python
>>> ios_device.get('hostname')           # Returns None if key missing
>>> ios_device.get('hostname', 'unknown')  # Returns 'unknown' if key missing
'unknown'
```

**When do you use `[]` vs `get()`?**
- Use `[]` when the key MUST exist (crash if it doesn't — that's a bug)
- Use `get()` when the key MIGHT not exist (provide a default value)

#### 4.2.2 Modifying Dictionaries

```python
# Add a new key
ios_device['hostname'] = 'csr1'

# Change an existing key
ios_device['password'] = 'new_password'

# Delete a key
del ios_device['password']
# Or:
ios_device.pop('password')    # Returns the value before deleting

# Check if a key exists
if 'hostname' in ios_device:
    print(f"Hostname: {ios_device['hostname']}")
```

#### 4.2.3 Dictionary Unpacking — The `**` Operator

This is the most important dictionary concept for Netmiko:

```python
ios_device = {
    'device_type': 'cisco_ios',
    'ip': '198.18.1.11',
    'username': 'cisco',
    'password': 'cisco',
}

# These two lines are IDENTICAL:
net_connect = ConnectHandler(**ios_device)
net_connect = ConnectHandler(device_type='cisco_ios', ip='198.18.1.11', 
                             username='cisco', password='cisco')
```

**What does `**` do?** It "unpacks" the dictionary into keyword arguments. Each key becomes a parameter name, and each value becomes the parameter value.

**Why use this?** Because it's much cleaner than passing each parameter individually, especially when you have many parameters. And because you can store the dictionary in a variable, file, or database and pass it dynamically.

**What if the dictionary has a key that the function doesn't accept?**

```python
ios_device = {
    'device_type': 'cisco_ios',
    'ip': '198.18.1.11',
    'username': 'cisco',
    'password': 'cisco',
    'favorite_color': 'blue',    # ConnectHandler doesn't have this parameter
}
net_connect = ConnectHandler(**ios_device)
# TypeError: __init__() got an unexpected keyword argument 'favorite_color'
```

The function rejects the unknown parameter. Only include keys that the function expects.

#### 4.2.4 Nested Dictionaries — Real-World Device Inventories

**Twin Bridges Course** (`class1/dict/dict_ex.py`) — Nested dictionary:

```python
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
```

**What is a "nested dictionary"?** A dictionary where one of the values is another dictionary. The `"domain"` key's value is itself a dictionary with `"uid"`, `"name"`, and `"domain-type"` keys.

**How to access nested values?** Chain the key access:

```python
>>> ftp_service["domain"]["name"]
'Check Point Data'

>>> ftp_service["domain"]["uid"]
'a0bbbc99-adef-4ef8-bb6d-defdefdefdef'
```

**Read it left to right:**
1. `ftp_service["domain"]` → returns the inner dictionary
2. `...["name"]` → access the `"name"` key of that inner dictionary

**This is exactly how you navigate Genie-parsed output** in the capstone project:

```python
output = net_connect.send_command('show version', use_genie=True)
hostname = output["version"]["hostname"]
chassis = output["version"]["chassis"]
serial = output["version"]["chassis_sn"]
```

### 4.3 Sets — Finding Differences Between Configurations

**What is a set?** An unordered collection of unique items. Sets automatically remove duplicates.

**Why do network engineers need sets?** For comparing things:
- Which VLANs are on switch A but not switch B?
- Which ACL entries are in the running config but not in the policy?
- Which devices responded but weren't in the inventory?

```python
# Remove duplicates from a list
>>> vlan_list = [10, 20, 30, 10, 20, 50]
>>> set(vlan_list)
{10, 20, 30, 50}    # Duplicates removed
```

**Twin Bridges Course** (`class3/sets/set_ex.py`):

```python
my_list = [1, 1, 3, 4, 7, 6, 7, 8, 3, 10]
my_list2 = [1, 1, 7, 6, 7, 8, 3, 10, 20, 45, 81, 99]

my_set1 = set(my_list)     # {1, 3, 4, 6, 7, 8, 10}
my_set2 = set(my_list2)    # {1, 3, 6, 7, 8, 10, 20, 45, 81, 99}

# Union — all unique items from both sets
union_sets = my_set1 | my_set2
print(union_sets)

# Intersection — items in BOTH sets
intersect_sets = my_set1 & my_set2
print(intersect_sets)

# Difference — items in set1 but NOT in set2
set_diff1 = my_set1 - my_set2
print(set_diff1)             # {4} — only 4 is in set1 but not set2
```

**Network application — VLAN compliance audit:**

```python
required_vlans = {10, 20, 30, 40, 50, 100}  # Corporate policy
actual_vlans = {10, 20, 30, 99, 200}         # What's on the switch

missing = required_vlans - actual_vlans
print(f"Missing VLANs: {missing}")      # {40, 50, 100}

unauthorized = actual_vlans - required_vlans
print(f"Unauthorized VLANs: {unauthorized}")  # {99, 200}

compliant = required_vlans & actual_vlans
print(f"Compliant VLANs: {compliant}")  # {10, 20, 30}
```

### 4.4 Tuples — Immutable Sequences

**What is a tuple?** Like a list, but immutable (cannot be changed after creation).

**Why use tuples instead of lists?** When the data should not change:

```python
# Allowed device types — this should never be modified at runtime
ALLOWED_PLATFORMS = ('cisco_ios', 'cisco_nxos', 'arista_eos', 'juniper_junos')

# Coordinates, versions, or any fixed grouping
DEVICE_INFO = ('core-rtr-01', '10.0.0.1', 'cisco_ios')
```

**What if I try to modify a tuple?**

```python
>>> t = (1, 2, 3)
>>> t[0] = 99
TypeError: 'tuple' object does not support item assignment
```

Python prevents the modification. This is a feature, not a bug — it protects data that shouldn't change.

**Tuple unpacking — a common pattern:**

```python
# Unpack into named variables
hostname, ip, platform = DEVICE_INFO
print(f"{hostname} at {ip} running {platform}")
# core-rtr-01 at 10.0.0.1 running cisco_ios
```

**When is a tuple created without parentheses?**

```python
# This creates a tuple (the comma makes it a tuple, not the parentheses)
>>> x = 1, 2, 3
>>> type(x)
<class 'tuple'>

# Single-item tuple needs a trailing comma
>>> single = (42,)     # Tuple
>>> not_tuple = (42)   # Just an integer in parentheses!
```

---

## Chapter 5: Control Flow — if/elif/else

### 5.1 What is Control Flow and Why Does It Matter?

Every script you've written so far executes top-to-bottom, every line, every time. But real network automation requires decisions:

- Is the device reachable? → Connect. If not → Skip it.
- Is the interface up? → Collect stats. If down → Log a warning.
- Is the firmware version correct? → Move on. If outdated → Schedule upgrade.

Control flow statements (`if`, `elif`, `else`) let your code make these decisions. Without them, your script treats every device, every interface, and every situation identically — which is useless in a real network.

**Analogy:** Control flow is like a route-map on a Cisco router. A route-map evaluates conditions and takes different actions depending on the match. An `if` statement does the same thing for your Python code.

### 5.2 The `if` Statement — Making a Single Decision

```python
vlan_id = 100

if vlan_id == 100:
    print("This is the management VLAN")
```

**Line-by-line explanation:**

**Line 1: `vlan_id = 100`**
Creates a variable `vlan_id` with the integer value `100`.

**Line 3: `if vlan_id == 100:`**
This is the `if` statement. Let's break it apart:
- `if` — The keyword that starts a conditional check
- `vlan_id == 100` — The **condition** being tested. `==` checks if the left side equals the right side. This evaluates to either `True` or `False`.
- `:` — The colon is REQUIRED. It tells Python "an indented block follows." Forgetting the colon is one of the most common syntax errors.

**What happens at runtime?**
1. Python evaluates `vlan_id == 100` → `100 == 100` → `True`
2. Because the condition is `True`, Python executes the indented block below
3. `print("This is the management VLAN")` runs

**Line 4: `print("This is the management VLAN")`**
This line is indented (4 spaces), meaning it belongs to the `if` block. It only executes when the condition is `True`.

**What if the condition is False?**

```python
vlan_id = 200

if vlan_id == 100:
    print("This is the management VLAN")    # This line is SKIPPED

print("Script continues here")    # This ALWAYS runs (not indented under if)
```

When `vlan_id` is `200`, the condition `200 == 100` is `False`, so the indented block is skipped entirely. Execution continues at the next unindented line.

**What if I forget the colon?**

```python
if vlan_id == 100
    print("Management VLAN")
```

```
SyntaxError: expected ':'
```

Python tells you exactly what's missing. Always end `if`, `elif`, `else`, `for`, `while`, `def`, and `class` lines with a colon.

**What if I forget to indent?**

```python
if vlan_id == 100:
print("Management VLAN")
```

```
IndentationError: expected an indented block after 'if' statement on line 1
```

Python expected indented code after the colon but found code at the same level.

### 5.3 The `if/else` Statement — Two Paths

```python
interface_status = "up"

if interface_status == "up":
    print("Interface is operational")
else:
    print("Interface is DOWN — investigate!")
```

**How does `else` work?** The `else` block runs when the `if` condition is `False`. Exactly one of the two blocks always executes — never both, never neither.

**Think of it as a fork in the road:** You evaluate the condition at the fork. If `True`, you go left (the `if` block). If `False`, you go right (the `else` block). You always take exactly one path.

**What if I put code between `if` and `else`?**

```python
if interface_status == "up":
    print("Up")
print("This line breaks things")    # NOT indented under if or else
else:                                # SyntaxError!
    print("Down")
```

```
SyntaxError: invalid syntax
```

The `else` must immediately follow the `if` block (at the same indentation level). You cannot put unindented code between them.

### 5.4 The `if/elif/else` Statement — Multiple Conditions

**What if you have more than two possibilities?** Use `elif` (short for "else if"):

```python
interface_status = "up"
protocol_status = "up"

if interface_status == "up" and protocol_status == "up":
    print("Interface is fully operational")
elif interface_status == "up" and protocol_status == "down":
    print("Layer 1 up, Layer 2 problem — check encapsulation")
elif interface_status == "administratively down":
    print("Interface is shutdown — check change tickets")
else:
    print("Interface is down — check cabling")
```

**How does elif work?** Python checks conditions top-to-bottom:
1. Check `if` condition → If `True`, run its block and SKIP everything else
2. If `False`, check the first `elif` condition → If `True`, run its block and SKIP the rest
3. If `False`, check the next `elif` → and so on...
4. If ALL conditions are `False`, run the `else` block

**Key insight: Only ONE block ever runs.** Once Python finds a `True` condition, it runs that block and skips all remaining `elif` and `else` blocks. This is why order matters.

**What if I have overlapping conditions?**

```python
temperature = 75

if temperature > 50:
    print("Above 50")    # This runs
elif temperature > 60:
    print("Above 60")    # This is NEVER reached even though 75 > 60!
elif temperature > 70:
    print("Above 70")    # This is NEVER reached even though 75 > 70!
```

Because `75 > 50` is `True`, Python runs the first block and skips everything else. If you want to find the most specific match, put the most specific conditions FIRST:

```python
if temperature > 70:
    print("Above 70")    # Most specific first
elif temperature > 60:
    print("Above 60")
elif temperature > 50:
    print("Above 50")    # Most general last
```

**Is `else` required?** No. You can have `if` alone, `if/else`, `if/elif`, or `if/elif/else`. The `else` is optional — it's a catch-all for when no condition matches.

**Twin Bridges Course** (`class1/cond/cond_ex1.py`) — Filtering firewall services:

```python
#!/usr/bin/env python
import json

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

**Line-by-line explanation:**

**`import json`** — Loads the `json` module so we can read JSON files. We covered this in Chapter 7 (Files), but here's a preview.

**`with open("tcp_services.json") as f:`** — Opens a JSON file for reading. The `with` statement ensures the file is automatically closed when done.

**`services = json.load(f)`** — Reads the entire JSON file and converts it into a Python dictionary. Now `services` is a dictionary.

**`service_list = services["objects"]`** — Accesses the `"objects"` key of the dictionary, which contains a list of service dictionaries.

**`print(len(service_list))`** — `len()` returns the number of items in the list. This tells us how many services exist.

**`for service in service_list:`** — Iterates through each service in the list. We'll cover `for` loops in detail in Chapter 6. For now, understand that this runs the indented block once for each service.

**`service_name = service["name"]`** — Each `service` is a dictionary. This extracts the `"name"` key.

**`if service_name == "ftp":`** — Checks if this service is FTP.

**`elif service_name == "domain-tcp":`** — If not FTP, checks if it's DNS over TCP.

**`else: print(service_name)`** — If neither FTP nor DNS, just print the service name.

**Why is this useful?** This is exactly how you'd process output from a network device API — load JSON, iterate through the results, and take different actions based on what you find.

### 5.5 Comparison Operators — The Building Blocks of Conditions

Every `if` statement needs a condition that evaluates to `True` or `False`. Here are all the comparison operators:

```python
# Equal
>>> 10 == 10
True
>>> "cisco" == "Cisco"    # Case-sensitive!
False

# Not equal
>>> 10 != 20
True

# Greater than / Less than
>>> 10 > 5
True
>>> 10 < 5
False

# Greater than or equal / Less than or equal
>>> 10 >= 10
True
>>> 10 <= 9
False
```

**Why is `==` two equals signs?** Because a single `=` is assignment (putting a value into a variable). `==` is comparison (checking if two values are the same). This distinction is critical:

```python
vlan_id = 100      # ASSIGNS the value 100 to vlan_id
vlan_id == 100     # CHECKS if vlan_id equals 100 (returns True or False)
```

**What if I accidentally use `=` instead of `==` in an `if` statement?**

```python
if vlan_id = 100:    # WRONG!
```

```
SyntaxError: invalid syntax. Maybe you meant '==' or ':=' instead of '='?
```

Python catches this mistake and even suggests the fix!

**String comparison is case-sensitive:**

```python
>>> "Cisco" == "cisco"
False
>>> "Cisco".lower() == "cisco".lower()
True    # Convert both to lowercase for case-insensitive comparison
```

**What if I compare different types?**

```python
>>> 10 == "10"
False    # An integer is NEVER equal to a string
>>> 10 == 10.0
True     # Integer and float comparison works
```

### 5.6 Logical Operators — Combining Conditions

**`and`** — Both conditions must be True:

```python
if interface_status == "up" and protocol_status == "up":
    print("Fully operational")
```

**How to read this:** "If the interface status is 'up' AND the protocol status is 'up', then print..."

**Truth table for `and`:**
```
True  and True  → True
True  and False → False
False and True  → False
False and False → False
```

**`or`** — At least one condition must be True:

```python
if device_type == "cisco_ios" or device_type == "cisco_nxos":
    print("Cisco platform")
```

**Truth table for `or`:**
```
True  or True  → True
True  or False → True
False or True  → True
False or False → False
```

**`not`** — Inverts True/False:

```python
if not is_reachable:
    print("Device is unreachable!")
```

**`not True` is `False`. `not False` is `True`.**

**Twin Bridges Course** (`class1/cond/cond_ex5.py`) — Compound conditions:

```python
#!/usr/bin/env python
import yaml

with open("api_support_versions.yml") as f:
    api_versions = yaml.safe_load(f)

supported_versions = api_versions["supported-versions"]
```

**What is this doing?** Reading a YAML file that contains a list of supported API versions. After this, `supported_versions` is a list like `['1', '1.1', '1.2', '1.3', '1.4', '1.5', '1.6', '1.7', '1.8']`.

```python
if "1.8" in supported_versions:
    api_version = "1.8"
```

**What does `in` do here?** The `in` operator checks if a value exists in a list (or string, or set, or any collection). If `"1.8"` is found in the `supported_versions` list, the condition is `True`.

**What if `"1.8"` is NOT in the list?** The `if` block is skipped, and `api_version` is never created. If you try to use `api_version` later, you'll get a `NameError`. This is why it's good practice to set a default value before the `if`:

```python
api_version = "1.0"    # Default
if "1.8" in supported_versions:
    api_version = "1.8"
```

```python
api_version = "1.8"
if "1." in api_version:
    base_api = "v1"
elif "2." in api_version:
    base_api = "v2"
```

**What does `"1." in api_version` mean?** It checks if the substring `"1."` appears anywhere in the string `api_version`. Since `"1.8"` contains `"1."`, this is `True`.

```python
if base_api == "v1" and float(api_version) >= 1.8:
    print("API Version 1.8 or later (not V2)")
```

**What does `float(api_version)` do?** Converts the string `"1.8"` to the floating-point number `1.8` so we can do numeric comparison with `>=`.

**Why can't we compare strings directly?** Because string comparison is alphabetical, not numerical:

```python
>>> "1.8" > "1.10"
True    # WRONG! Alphabetically, "8" > "1" 
>>> 1.8 > 1.10
True    # Correct numeric comparison
```

```python
if base_api == "v1" or base_api == "v2":
    print("API V1 or V2")
```

**This checks:** "Is it v1? OR is it v2?" If either is `True`, the whole condition is `True`.

### 5.7 Booleans and Truthiness — Understanding What Python Considers True/False

**What is a Boolean?** A data type with exactly two values: `True` and `False`. Every `if` condition ultimately evaluates to a Boolean.

**But what about non-boolean values?** Python has a concept called "truthiness" — every value can be evaluated as `True` or `False`:

**Twin Bridges Course** (`class1/booleans/truish.py`):

```python
#!/usr/bin/env python

# Strings — empty string is False
some_str = ""
print(bool(some_str))     # False

# Numbers — zero is False
some_int = 0
print(bool(some_int))     # False
some_float = 0.0
print(bool(some_float))   # False

# Lists — empty list is False
some_list = []
print(bool(some_list))    # False

# Dict — empty dict is False
some_dict = {}
print(bool(some_dict))    # False
```

**The rule is simple:** "Empty" or "zero" values are `False`. Everything else is `True`.

| Value | Boolean | Why? |
|-------|---------|------|
| `""` (empty string) | `False` | No characters |
| `"hello"` (any non-empty string) | `True` | Has characters |
| `0` or `0.0` | `False` | Zero |
| `42` or `3.14` (any non-zero number) | `True` | Non-zero |
| `[]` (empty list) | `False` | No items |
| `[1, 2]` (non-empty list) | `True` | Has items |
| `{}` (empty dict) | `False` | No entries |
| `{"key": "val"}` (non-empty dict) | `True` | Has entries |
| `None` | `False` | The "nothing" value |

**Why does this matter for network automation?** Because you can write cleaner code:

```python
# Instead of this (verbose and unnecessary):
if len(output) > 0:
    print("Got output from device")

# Write this (Pythonic):
if output:
    print("Got output from device")

# Instead of this:
if len(device_list) == 0:
    print("No devices to connect to!")

# Write this:
if not device_list:
    print("No devices to connect to!")
```

**What if** `output` **is** `None` **instead of an empty string?** It still works! `None` is also "falsy," so `if output:` catches both empty strings and `None`. This is useful because Netmiko sometimes returns `None` if a command fails.

**Twin Bridges Course** (`class1/booleans/show_circuit.py`) — Short-circuit evaluation:

```python
#!/usr/bin/env python

# and: if the first condition is False, we are done.
check_cond = False
if check_cond and my_func():
    print("Never printed")

# or: if the first condition is True, we are done.
skip_func = True
if skip_func or my_func():
    print("Always printed")
```

**What is short-circuit evaluation?** Python is lazy (in a good way):
- With `and`: If the first condition is `False`, the whole thing is `False` regardless of the second condition. Python doesn't even evaluate `my_func()`.
- With `or`: If the first condition is `True`, the whole thing is `True` regardless. Python doesn't evaluate the second part.

**Why does this matter?** Because you can write safe code like:

```python
# Safe — if device_list is empty, Python never evaluates device_list[0]
if device_list and device_list[0] == "10.0.0.1":
    print("First device is the core router")
```

Without short-circuiting, `device_list[0]` would crash with `IndexError` if the list is empty. But because `and` short-circuits, Python sees `device_list` is empty (falsy), knows the whole condition is `False`, and never tries to access `device_list[0]`.

### 5.8 The `in` Operator — Membership Testing

The `in` operator is one of the most powerful tools in Python. It checks whether a value exists inside a collection.

```python
# Check if a VLAN exists in a list
allowed_vlans = [10, 20, 30, 40, 50]
if 30 in allowed_vlans:
    print("VLAN 30 is allowed")
```

**What does `in` actually do?** It iterates through the collection and checks each item for equality. If it finds a match, it returns `True`. If it reaches the end without finding a match, it returns `False`.

```python
# Check if a keyword exists in command output
show_output = "Interface GigabitEthernet0/1 is up, line protocol is up"
if "is up" in show_output:
    print("Interface is operational")
```

**When used with strings, `in` checks for substrings.** It doesn't need to match a complete word — `"is up"` is found within the longer string.

**What if I check for something that's not there?**

```python
>>> "down" in "Interface is up"
False    # No crash, just returns False
```

The `in` operator never crashes. It always returns `True` or `False`.

```python
# Check if device type is supported
device_type = "cisco_ios"
if device_type in ('cisco_ios', 'cisco_nxos', 'arista_eos'):
    print(f"Supported platform: {device_type}")
```

**Why use a tuple here instead of a list?** Tuples are slightly faster for membership testing when the collection is small and fixed. But functionally, a list would work identically.

**`not in` — the inverse:**

```python
if "down" not in show_output:
    print("No interfaces are down")
```

**Twin Bridges Exercise** (`class1/exercises/cond_ex/cond_ex1.py`) — User input with conditionals:

```python
#!/usr/bin/env python

pod_numb = input("Enter pod number: ")
fw_name = f"chkpnt-pod{pod_numb}"

if fw_name == "chkpnt-pod1":
    print("Found pod1")
elif fw_name == "chkpnt-pod99":
    print("Found pod99")
else:
    print("Not my pod")
```

**Line-by-line:**

**`pod_numb = input("Enter pod number: ")`** — The `input()` function displays the prompt text, waits for the user to type something and press Enter, then returns what they typed as a **string**.

**Critical point:** `input()` ALWAYS returns a string. Even if the user types `99`, `pod_numb` will be the string `"99"`, not the number `99`. If you need to compare it as a number, you must convert: `int(pod_numb)`.

**`fw_name = f"chkpnt-pod{pod_numb}"`** — Creates a firewall name by inserting the user's input into an f-string. If the user typed `99`, `fw_name` becomes `"chkpnt-pod99"`.

**What if the user types nothing and just presses Enter?** `pod_numb` becomes an empty string `""`, and `fw_name` becomes `"chkpnt-pod"`. The `else` block would run.

**What if the user types something unexpected like `abc`?** `fw_name` becomes `"chkpnt-podabc"`. No error occurs — Python happily creates the string. The `else` block would run. In production code, you should validate the input.

---

## Chapter 6: Loops — Iterating Over Network Devices

### 6.1 What is a Loop and Why Do Network Engineers Need Them?

A loop repeats a block of code multiple times. Without loops, automating 100 devices would require writing the same code 100 times. With a loop, you write it once and it runs for each device.

**Analogy:** A loop is like a macro on a network management system — you define an action once, and it executes across every device in your inventory.

### 6.2 The `for` Loop — Iterating Over a Collection

The `for` loop is the workhorse of network automation. It takes a collection (list, string, dictionary, file) and executes a block of code once for each item.

**Twin Bridges Course** (`class1/loops/loop_ex1.py`):

```python
for loop_var in ["hello", "world", "something", "else"]:
    print(loop_var)
```

**Line-by-line explanation:**

**`for loop_var in ["hello", "world", "something", "else"]:`**

Let's break this apart:
- `for` — The keyword that starts a for loop
- `loop_var` — The **loop variable**. Each time through the loop, this variable takes on the next value from the collection. You choose the name — it could be `item`, `x`, `device`, anything. Choose something descriptive.
- `in` — Separates the loop variable from the collection
- `["hello", "world", "something", "else"]` — The **collection** to iterate over. This is a list with 4 items.
- `:` — Required colon, just like `if` statements

**What happens at runtime?**
1. **Iteration 1:** `loop_var = "hello"` → runs `print("hello")`
2. **Iteration 2:** `loop_var = "world"` → runs `print("world")`
3. **Iteration 3:** `loop_var = "something"` → runs `print("something")`
4. **Iteration 4:** `loop_var = "else"` → runs `print("else")`
5. No more items → loop ends, execution continues after the loop

**What if the list is empty?**

```python
for item in []:
    print(item)    # This line NEVER executes
print("Loop is done")    # This runs immediately
```

An empty list means zero iterations. The loop body is simply skipped. No error.

**Twin Bridges Course** (`class1/loops/loop_ex2.py`) — Accessing elements inside a loop:

```python
my_list = ["hello", "world", "something", "else"]
for loop_var in my_list:
    print(loop_var)
    print(loop_var[0])     # First character
    print(loop_var[-1])    # Last character
```

**What does `loop_var[0]` do inside the loop?** Since `loop_var` is a string in each iteration, `loop_var[0]` gets the first character. In iteration 1, `loop_var` is `"hello"`, so `loop_var[0]` is `"h"`.

**What if I modify the list while looping over it?** Don't. It leads to unpredictable behavior:

```python
# DANGEROUS — modifying a list while iterating over it
devices = ["R1", "R2", "R3"]
for d in devices:
    if d == "R2":
        devices.remove(d)    # BAD! Can skip items
```

If you need to filter items, create a new list instead:

```python
# SAFE — build a new list
devices = ["R1", "R2", "R3"]
keep = [d for d in devices if d != "R2"]
```

### 6.3 `break` — Stop the Loop Early

**Twin Bridges Course** (`class1/loops/loop_ex3.py`):

```python
my_list = ["hello", "world", "something", "else"]

for loop_var in my_list:
    if loop_var == "something":
        print("\n\nAll done!\n")
        break
    print(loop_var)
    print("...still in the loop")
```

**What does `break` do?** It immediately exits the loop. No more iterations happen. Execution continues at the first line AFTER the loop.

**Runtime walkthrough:**
1. `loop_var = "hello"` → not "something" → print "hello" and "...still in the loop"
2. `loop_var = "world"` → not "something" → print "world" and "...still in the loop"
3. `loop_var = "something"` → IS "something" → print "All done!" → `break` → **EXIT LOOP**
4. `loop_var = "else"` → **NEVER REACHED**

**When do you use `break` in network automation?** When you find what you're looking for and don't need to keep searching:

```python
# Find the first device that responds
for device_ip in device_list:
    if ping(device_ip):
        print(f"Found reachable device: {device_ip}")
        break    # No need to check the rest
```

### 6.4 `continue` — Skip This Iteration

**Twin Bridges Course** (`class1/loops/loop_ex4.py`):

```python
my_list = ["hello", "world", "something", "else"]

for loop_var in my_list:
    if loop_var == "something":
        print("<skip>")
        continue
    print(loop_var)
    print("...still in the loop")
```

**What does `continue` do?** It skips the REST of the current iteration and jumps to the NEXT iteration. The loop continues — it doesn't exit.

**Runtime walkthrough:**
1. `loop_var = "hello"` → not "something" → print "hello" and "...still in the loop"
2. `loop_var = "world"` → not "something" → print "world" and "...still in the loop"
3. `loop_var = "something"` → IS "something" → print "<skip>" → `continue` → **SKIP TO NEXT ITERATION**
4. `loop_var = "else"` → not "something" → print "else" and "...still in the loop"

**Key difference from `break`:** `continue` skips one iteration. `break` stops the entire loop.

**Twin Bridges Exercise** (`class1/exercises/loops_ex/loops_ex2.py`) — Both together:

```python
my_firewalls = [
    "pod1-gaia", "pod2-gaia", "pod3-gaia", "pod4-gaia",
    "pod5-gaia", "pod98-gaia", "pod99-gaia",
]

for fw in my_firewalls:
    if fw == "pod4-gaia":
        continue          # Skip pod4 (under maintenance)
    if fw == "pod98-gaia":
        break             # Stop processing at pod98
    print(fw)
```

**Output:**
```
pod1-gaia
pod2-gaia
pod3-gaia
pod5-gaia
```

**Why is pod4 missing?** `continue` skipped it.  
**Why are pod98 and pod99 missing?** `break` stopped the loop at pod98 before it could print.

**This is the exact pattern used in the LABATO-1010 capstone** for error handling — when a device connection fails, `continue` moves to the next device instead of crashing:

```python
for devices in device_list:
    try:
        net_connect = ConnectHandler(**ios_device)
    except NetmikoAuthenticationException:
        print('Authentication failure: ' + ip_address_of_device)
        continue    # Skip this device, try the next one
```

### 6.5 The `while` Loop — Repeat Until a Condition Changes

The `for` loop iterates over a collection. The `while` loop repeats as long as a condition is `True`.

```python
max_retries = 3
attempt = 0
connected = False

while attempt < max_retries and not connected:
    attempt += 1
    print(f"Connection attempt {attempt}...")
    if attempt == 2:
        connected = True
        print("Connected!")

if not connected:
    print("Failed to connect after max retries")
```

**Line-by-line:**

**`while attempt < max_retries and not connected:`** — Check TWO conditions:
1. Have we used all our retries? (`attempt < max_retries`)
2. Are we still not connected? (`not connected`)

Both must be `True` to keep looping. If either becomes `False`, the loop stops.

**`attempt += 1`** — This is shorthand for `attempt = attempt + 1`. It increases `attempt` by 1.

**What if I forget to update the condition?**

```python
# INFINITE LOOP — never changes 'attempt'
while attempt < max_retries:
    print("Trying...")    # Runs forever!
```

This runs forever because `attempt` never increases, so `attempt < max_retries` is always `True`. Press `Ctrl+C` to force-stop the script.

**When do you use `while` vs `for`?**
- Use `for` when you know the collection to iterate over (list of devices, lines in a file)
- Use `while` when you're waiting for a condition to change (retrying connections, polling for status)

### 6.6 Looping Patterns for Network Automation

#### Pattern 1: Building a device list and iterating (LABATO-1010 Script 3)

```python
#!/usr/bin/env python
from netmiko import ConnectHandler

ios1 = {
    'device_type': 'cisco_ios',
    'ip': '198.18.1.11',
    'username': 'cisco',
    'password': 'cisco',
}

ios2 = {
    'device_type': 'cisco_ios',
    'ip': '198.18.1.12',
    'username': 'cisco',
    'password': 'cisco',
}

devices = [ios1, ios2]

for device in devices:
    print('Connecting to device ' + device['ip'])
    net_connect = ConnectHandler(**device)
    output = net_connect.send_config_set('logging host 10.1.1.2')
    net_connect.disconnect()
    print(output)
```

**Why is this script important?** Because it combines FIVE concepts you've learned:
1. **Dictionaries** (Ch.4) — `ios1` and `ios2` store connection parameters
2. **Lists** (Ch.4) — `devices = [ios1, ios2]` collects them
3. **For loops** (this chapter) — `for device in devices:` iterates through each
4. **Dictionary access** (Ch.4) — `device['ip']` retrieves the IP
5. **Dictionary unpacking** (Ch.4) — `**device` passes all parameters to ConnectHandler

**What happens if one device is unreachable?** The script crashes at that device and never reaches the remaining devices. That's why Script 5 adds error handling (Chapter 11).

#### Pattern 2: `enumerate()` for numbered output

```python
interfaces = ["Gi0/0", "Gi0/1", "Gi0/2", "Lo0", "Lo100"]

for index, intf in enumerate(interfaces, start=1):
    print(f"{index}. {intf}")
```

**What is `enumerate()`?** It wraps a collection and provides both the index AND the value on each iteration. Without `enumerate()`, you'd have to track the index manually.

**What does `start=1` do?** By default, numbering starts at 0. `start=1` makes it start at 1, which is more natural for human-readable output.

**Output:**
```
1. Gi0/0
2. Gi0/1
3. Gi0/2
4. Lo0
5. Lo100
```

#### Pattern 3: Iterating through a dictionary with `.items()`

```python
london_co = {
    'r1': {'hostname': 'london_r1', 'IP': '10.255.0.1', 'vendor': 'Cisco'},
    'r2': {'hostname': 'london_r2', 'IP': '10.255.0.2', 'vendor': 'Cisco'},
    'sw1': {'hostname': 'london_sw1', 'IP': '10.255.0.101', 'vendor': 'Cisco'},
}

for device_id, params in london_co.items():
    print(f"Device: {params['hostname']}, IP: {params['IP']}")
```

**What does `.items()` return?** A sequence of `(key, value)` pairs. On each iteration, `device_id` gets the key (like `'r1'`) and `params` gets the value (the nested dictionary).

**What if I iterate over a dictionary without `.items()`?**

```python
for key in london_co:
    print(key)    # Only prints keys: 'r1', 'r2', 'sw1'
```

Without `.items()`, you only get the keys. You'd need `london_co[key]` to access the values.

---

## Chapter 7: Working with Files

### 7.1 Why Do Network Engineers Need File Operations?

File operations are essential because:
- **Device lists** are stored in files (IP addresses, one per line)
- **Configuration commands** are stored in files (so you can review them before pushing)
- **Backup configs** are saved to files
- **Inventory data** is read from and written to JSON, YAML, and CSV files
- **Credentials** can come from environment files

### 7.2 Reading Files — Three Approaches

**Twin Bridges Course** (`class1/files/read_file.py`):

```python
#!/usr/bin/env python

# Open file
f = open("my_file.txt", "r")
```

**What does `open()` do?** It creates a "file object" — a connection to a file on disk. Think of it like establishing an SSH session to a file.

**What does `"r"` mean?** It's the "mode":
- `"r"` — Read only (default). You can read but not write.
- `"w"` — Write only. Creates a new file (or OVERWRITES an existing one!).
- `"a"` — Append. Adds to the end of an existing file.
- `"r+"` — Read and write.

**What if the file doesn't exist?**

```python
>>> f = open("nonexistent.txt", "r")
FileNotFoundError: [Errno 2] No such file or directory: 'nonexistent.txt'
```

Python crashes with `FileNotFoundError`. This is a common error — always check that the file exists or handle the exception.

```python
# Read entire file contents into a single string
data = f.read()
print(data)
```

**What does `f.read()` return?** The ENTIRE contents of the file as one big string, including all newline characters. If the file is 1,000 lines, you get one string with 999 `\n` characters embedded in it.

```python
# Go back to start of the file
f.seek(0)
```

**Why do we need `seek(0)`?** After `read()`, the "cursor" is at the end of the file. If you try to read again without resetting, you get an empty string (there's nothing left to read). `seek(0)` moves the cursor back to the beginning.

**Analogy:** It's like rewinding a tape. After playing the whole tape, you need to rewind before you can play it again.

```python
# Read the entire file, but as a list of lines
data = f.readlines()
print(type(data))    # <class 'list'>
print(data)          # ['line 1\n', 'line 2\n', 'line 3\n']
```

**What's the difference between `read()` and `readlines()`?**
- `read()` → Returns one big string
- `readlines()` → Returns a list of strings, one per line

**Important: `readlines()` keeps the `\n` at the end of each line!** This is almost never what you want. Use `read().splitlines()` instead:

```python
data = f.read().splitlines()
# ['line 1', 'line 2', 'line 3']    — No trailing \n!
```

```python
# Loop over the file line by line
f.seek(0)
print("Looping over file")
for line in f:
    line = line.strip()
    print(repr(line))
```

**What does `for line in f:` do?** Files are "iterable" — you can loop over them directly. Each iteration gives you one line. This is memory-efficient for large files because it reads one line at a time instead of loading the entire file into memory.

**Why `line.strip()`?** Each line from the file includes a trailing `\n` (newline character). `strip()` removes it. Without `strip()`, your lines would have invisible newlines attached.

**Why `repr(line)`?** `repr()` shows the exact string representation, including hidden characters like `\n` and spaces. This is essential for debugging file parsing.

```python
# Close file
f.close()
```

**Why close the file?** Every open file uses a system resource (a "file descriptor"). If you open many files without closing them, you can run out of resources. Closing releases the resource.

**What if I forget to close?** It usually works fine for small scripts, but it's a bad habit. And if you're writing to a file, data might not actually be saved until you close it.

### 7.3 The `with` Statement — The Right Way to Handle Files

```python
with open('device_list') as f:
    device_list = f.read().splitlines()
```

**What does `with` do?** It creates a "context manager" that automatically closes the file when the indented block ends — even if an error occurs inside the block.

**This is ALWAYS better than manual `open()`/`close()` because:**
1. You can't forget to close the file
2. The file is closed even if an exception occurs
3. The code is cleaner

**From LABATO-1010 — reading the device list:**

```python
with open('device_list') as f:
    device_list = f.read().splitlines()

print(device_list)
# ['198.18.1.11', '198.18.1.12']
```

**What does each part do?**
1. `open('device_list')` — Opens the file named `device_list` (no extension)
2. `as f` — Names the file object `f`
3. `f.read()` — Reads the entire file: `"198.18.1.11\n198.18.1.12\n"`
4. `.splitlines()` — Splits on newlines: `['198.18.1.11', '198.18.1.12']`

**What if the file has blank lines?**

```
198.18.1.11

198.18.1.12

```

```python
>>> "198.18.1.11\n\n198.18.1.12\n\n".splitlines()
['198.18.1.11', '', '198.18.1.12', '']
```

Empty strings appear! Filter them out:

```python
device_list = [line for line in f.read().splitlines() if line.strip()]
```

### 7.4 Writing Files

**Twin Bridges Course** (`class1/files/write_file.py`):

```python
#!/usr/bin/env python

f = open("new_file.txt", "w")
f.write("hello world\n")
f.write("something else\n")
f.write("one last line\n")
f.close()
```

**What does `"w"` mode do?** Creates the file if it doesn't exist. If it DOES exist, it **deletes all existing content** and starts fresh.

**THIS IS DANGEROUS!** If you accidentally open a backup config in write mode, you'll erase it:

```python
# DANGER: This erases the entire backup file!
f = open("backup/core-rtr-01.cfg", "w")
```

**What about `"a"` (append) mode?** It adds to the end of the file without erasing existing content:

```python
with open("log.txt", "a") as f:
    f.write("2024-03-15 10:30: Backup completed\n")
```

**Why do we need `\n` in `write()`?** Unlike `print()`, `write()` does NOT add a newline automatically. If you forget `\n`, all your text ends up on one line.

**The better approach with `with`:**

```python
with open("new_file.txt", "w") as f:
    f.write("hello world\n")
    f.write("something else\n")
    f.write("one last line\n")
# File is automatically closed here
```

### 7.5 Working with JSON Files

**Why JSON?** JSON (JavaScript Object Notation) is the standard data format for REST APIs. Cisco DNA Center, Meraki, ACI, and virtually every modern network platform uses JSON for API communication.

**Twin Bridges Course** (`class1/files/read_json.py`):

```python
import json

with open("gaia_api.json") as f:
    data = json.load(f)

print(data)
```

**What does `json.load(f)` do?** It reads the file and converts the JSON text into a Python data structure — typically a dictionary or a list. After this, `data` is a regular Python dictionary that you can access with `data["key"]`.

**What's the difference between `json.load()` and `json.loads()`?**
- `json.load(f)` — Reads from a **file** object
- `json.loads(s)` — Reads from a **string**

```python
# From a file
with open("data.json") as f:
    data = json.load(f)

# From a string (common when working with API responses)
json_string = '{"hostname": "R1", "ip": "10.0.0.1"}'
data = json.loads(json_string)
```

**Twin Bridges Course** (`class1/files/write_json.py`):

```python
import json

data = {
    "current-version": "1.8",
    "supported-versions": ["1", "1.1", "1.2", "1.3", "1.4",
                           "1.5", "1.6", "1.7", "1.8"],
}

with open("gaia_api.json", "w") as f:
    json.dump(data, f, indent=4)
```

**What does `json.dump(data, f, indent=4)` do?**
- `data` — The Python dictionary to save
- `f` — The file to write to
- `indent=4` — Format the output with 4-space indentation (human-readable)

**What if I don't use `indent=4`?** The entire JSON is written on one line, which is hard to read but smaller in file size. Use `indent` for files humans will read, omit it for machine-to-machine communication.

### 7.6 Working with YAML Files

**Why YAML?** YAML is the configuration format for Ansible, Nornir, and many DevOps tools. It's designed to be human-readable and easy to write by hand.

**Twin Bridges Course** (`class1/files/read_yaml.py`):

```python
import yaml

with open("gaia_api.yaml") as f:
    data = yaml.safe_load(f)

print(data)
```

**What does `yaml.safe_load()` do?** Reads the YAML file and converts it into a Python dictionary (or list). The `safe_` prefix means it only allows basic data types — no arbitrary Python code execution.

**Why `safe_load()` instead of `load()`?** `yaml.load()` can execute arbitrary Python code embedded in the YAML file, which is a security risk. ALWAYS use `yaml.safe_load()`.

**Twin Bridges Course** (`class1/files/write_yaml.py`):

```python
import yaml

data = {
    "current-version": "1.8",
    "supported-versions": ["1", "1.1", "1.2", "1.3", "1.4",
                           "1.5", "1.6", "1.7", "1.8"],
}

with open("gaia_api.yaml", "w") as f:
    yaml.dump(data, f, default_flow_style=False)
```

**What does `default_flow_style=False` do?** It forces YAML to use block style (one item per line) instead of flow style (JSON-like inline). Block style is much more readable:

```yaml
# Block style (default_flow_style=False) — READABLE
current-version: '1.8'
supported-versions:
- '1'
- '1.1'
- '1.2'

# Flow style (default_flow_style=True) — COMPACT
{current-version: '1.8', supported-versions: ['1', '1.1', '1.2']}
```

**Network Context — Nornir Inventory Files (from LABATO-1010):**

```yaml
# inventory/hosts.yml — defines each device
---
csr1:
  hostname: 198.18.1.11
  groups:
    - cisco

csr2:
  hostname: 198.18.1.12
  groups:
    - cisco
```

**What does `---` mean in YAML?** It marks the beginning of a YAML document. It's optional for single documents but good practice to include.

**What does the indentation mean in YAML?** Just like Python, YAML uses indentation to show hierarchy. `hostname: 198.18.1.11` is nested under `csr1:`, meaning it's a property of `csr1`.

When Python reads this with `yaml.safe_load()`, it becomes:

```python
{
    'csr1': {
        'hostname': '198.18.1.11',
        'groups': ['cisco']
    },
    'csr2': {
        'hostname': '198.18.1.12',
        'groups': ['cisco']
    }
}
```

**Twin Bridges Exercise** (`class1/exercises/file_ex/files_ex1.py`) — Understanding text vs. structured data:

```python
#!/usr/bin/env python
import json

filename = "network_objects.json"

# Read in file as text
with open(filename) as f:
    data = f.read()

print(f"\nRead in file({filename}) as a string")
print(f"Type 'data' var: {type(data)}")
```

**What is `data` at this point?** A string. The entire JSON file is one big string. You cannot access `data["objects"]` because strings don't support dictionary-style access.

```python
# Read in file as JSON
with open(filename) as f:
    data = json.load(f)
print(f"\nRead in file({filename}) as a data structure (dictionary)")
print(f"Type 'data' var: {type(data)}")
print(f"Type data['objects'] field: {type(data['objects'])}")
```

**Now what is `data`?** A dictionary. `json.load()` parsed the string into a Python data structure. Now you CAN access `data["objects"]` because it's a dictionary.

**This is a critical distinction:** Reading a file as text gives you a string. Parsing it with `json.load()` or `yaml.safe_load()` gives you structured data (dictionaries and lists). The structured version is what you need for automation.

---

## Chapter 8: Python Basic Examples — Bringing Concepts Together

### 8.1 What Are Comprehensions and Why Do They Exist?

A comprehension is a compact, one-line way to create a list, dictionary, or set from another collection. It replaces a multi-line `for` loop with a single, readable expression.

**Why do comprehensions exist?** Because building lists with `for` loops is so common that Python provides a shorthand. Comprehensions are not just shorter — they are also faster because Python optimizes them internally.

**Twin Bridges Course** (`class3/list_comprehenson/list_comp_ex.py`):

```python
my_list = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

squares = [x**2 for x in my_list]
print(squares)
# [1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
```

**How to read this comprehension:** `[x**2 for x in my_list]`
- Start from the middle: `for x in my_list` — "For each `x` in `my_list`..."
- Then the left side: `x**2` — "...compute `x` squared..."
- The square brackets: `[...]` — "...and put all results into a new list."

**The equivalent `for` loop:**

```python
squares = []
for x in my_list:
    squares.append(x**2)
```

**Which is better?** The comprehension is preferred when the logic is simple (one expression). The `for` loop is better when you need multiple lines of logic inside.

```python
evens = [x for x in my_list if x % 2 == 0]
print(evens)
# [2, 4, 6, 8, 10]
```

**How to read this:** "For each `x` in `my_list`, IF `x` is even (divisible by 2 with no remainder), include `x` in the new list."

**What does `x % 2 == 0` mean?** The `%` operator gives the remainder of division. `4 % 2` is `0` (4 divides evenly by 2). `5 % 2` is `1` (5 divided by 2 has remainder 1). So `x % 2 == 0` checks if `x` is even.

**Network application — Creating VLAN names:**

```python
vlans = [f'vlan {num}' for num in range(10, 16)]
print(vlans)
# ['vlan 10', 'vlan 11', 'vlan 12', 'vlan 13', 'vlan 14', 'vlan 15']
```

**What is `range(10, 16)`?** It generates numbers from 10 up to (not including) 16. So: 10, 11, 12, 13, 14, 15.

**Why not `range(10, 15)`?** Because `range()` excludes the end value. If you want VLANs 10 through 15, use `range(10, 16)`. This is consistent with slicing: `my_list[10:16]` also excludes index 16.

**Extracting IPs from a nested inventory:**

```python
london_co = {
    'r1': {'hostname': 'london_r1', 'IP': '10.255.0.1'},
    'r2': {'hostname': 'london_r2', 'IP': '10.255.0.2'},
    'sw1': {'hostname': 'london_sw1', 'IP': '10.255.0.101'},
}
ips = [london_co[device]['IP'] for device in london_co]
print(ips)
# ['10.255.0.1', '10.255.0.2', '10.255.0.101']
```

**How does this work?** `for device in london_co` iterates over the dictionary keys (`'r1'`, `'r2'`, `'sw1'`). For each key, `london_co[device]` gets the inner dictionary, and `['IP']` extracts the IP address.

**Dict comprehension — normalizing keys:**

```python
device = {'Hostname': 'R1', 'IOS': '15.4', 'IP': '10.0.0.1'}
normalized = {k.lower(): v for k, v in device.items()}
print(normalized)
# {'hostname': 'R1', 'ios': '15.4', 'ip': '10.0.0.1'}
```

**Why normalize keys?** Because API responses sometimes have inconsistent casing. Converting all keys to lowercase prevents `KeyError` when you access `data['hostname']` but the API returned `data['Hostname']`.

### 8.2 Complex Data Structures — Navigating Nested Data

**What is a "complex data structure"?** A dictionary containing lists of dictionaries, or any deeply nested combination of Python data types. This is what you get from API responses and parsed command output.

**From LABATO-1010 Script 9** — Genie-parsed output is a deeply nested dictionary:

```python
output = net_connect.send_command('show version', use_genie=True)
```

**What does `use_genie=True` do?** It tells Netmiko to parse the raw text output of `show version` into a structured Python dictionary using Cisco's Genie parser library.

**What does the output look like?** Instead of a raw text string, you get:

```python
{
    "version": {
        "hostname": "csr1",
        "chassis": "CSR1000V",
        "chassis_sn": "9FMKNB70YR1",
        "os": "IOS-XE",
        "version": "17.3.4a",
        "platform": "Virtual XE",
        ...
    }
}
```

**How do you navigate it?** Chain dictionary key access:

```python
hostname = output["version"]["hostname"]     # "csr1"
chassis = output["version"]["chassis"]       # "CSR1000V"
serial = output["version"]["chassis_sn"]     # "9FMKNB70YR1"
```

**What if a key doesn't exist in the parsed output?**

```python
>>> output["version"]["uptime"]
KeyError: 'uptime'
```

Use `get()` with a default:

```python
uptime = output["version"].get("uptime", "unknown")
```

**How do you explore an unfamiliar nested structure?** Use `pprint` (pretty print):

```python
from pprint import pprint
pprint(output)
```

This displays the dictionary with proper indentation so you can see the structure. Without `pprint`, a large dictionary is printed on one unreadable line.

---

## Chapter 9: Functions

### 9.1 What is a Function and Why Do You Need Them?

**A function is a named, reusable block of code.** You define it once, then call it whenever you need that behavior.

**Why do network engineers need functions?**
- You connect to devices in every script → write a `connect_device()` function
- You parse show output in multiple places → write a `parse_interfaces()` function
- You save configs to files repeatedly → write a `backup_config()` function

Without functions, you'd copy-paste the same code everywhere. When you need to change it, you'd have to find and update every copy. Functions solve this.

**Analogy:** A function is like a procedure in a runbook. "Step 3: Backup the running configuration" is defined once and referenced wherever needed. If the procedure changes, you update it in one place.

### 9.2 Creating Functions

**Twin Bridges Course** (`class1/functions/func_ex1.py`):

```python
def my_func(x, y):
    print(x)
    print(y)
    return x + y

ret_val = my_func(7, 2)
print(f"{ret_val=}")
```

**Line-by-line explanation:**

**`def my_func(x, y):`**
- `def` — Keyword that defines a new function
- `my_func` — The name of the function (follows `snake_case` convention)
- `(x, y)` — **Parameters** — the inputs the function expects
- `:` — Required colon (an indented block follows)

**What are parameters?** Placeholders for values that will be provided when the function is called. `x` and `y` don't have values yet — they'll be assigned when someone calls `my_func(7, 2)`.

**`print(x)` and `print(y)`** — These are the function body. They execute when the function is called.

**`return x + y`** — The `return` statement sends a value back to the caller. Without `return`, the function returns `None`.

**`ret_val = my_func(7, 2)`** — This CALLS the function:
1. `x` gets the value `7`, `y` gets the value `2`
2. `print(7)` runs, `print(2)` runs
3. `return 7 + 2` sends `9` back
4. `ret_val` receives the value `9`

**What if I call the function without enough arguments?**

```python
>>> my_func(7)
TypeError: my_func() missing 1 required positional argument: 'y'
```

**What if I call it with too many?**

```python
>>> my_func(7, 2, 3)
TypeError: my_func() takes 2 positional arguments but 3 were given
```

### 9.3 Keyword Arguments and Default Values

**Twin Bridges Course** (`class1/functions/func_ex2.py`) — Keyword arguments:

```python
def my_func(x, y):
    print(f"{x=}")
    print(f"{y=}")
    return x + y

# Keyword arguments — specify by name
ret_val = my_func(x=7, y=2)
print(f"{ret_val=}")

# Order doesn't matter with keyword arguments!
ret_val = my_func(y=42, x=0)
print(f"{ret_val=}")
```

**What are keyword arguments?** Instead of passing values by position (`my_func(7, 2)`), you pass them by name (`my_func(x=7, y=2)`). This makes the code more readable and order-independent.

**Why does order not matter with keyword arguments?** Because Python matches by name, not position. `my_func(y=42, x=0)` assigns `42` to `y` and `0` to `x` regardless of the order.

**Twin Bridges Course** (`class1/functions/func_ex3.py`) — Default values:

```python
def my_func(x, y, z=100):
    print(f"{x=}")
    print(f"{y=}")
    print(f"{z=}")
    return x + y + z

ret_val = my_func(x=7, y=2)
print(f"{ret_val=}")     # 109 (z defaults to 100)
```

**What is a default value?** If the caller doesn't provide a value for `z`, it automatically gets `100`. This makes `z` optional.

**When do you use defaults?** For parameters that usually have the same value but occasionally need to be different:

```python
def connect_device(host, username, password, device_type="cisco_ios", port=22):
    ...
```

Most devices are Cisco IOS on port 22, but you can override when needed:

```python
connect_device("10.0.0.1", "admin", "secret")                    # Uses defaults
connect_device("10.0.0.1", "admin", "secret", device_type="cisco_nxos")  # Override device_type
connect_device("10.0.0.1", "admin", "secret", port=2222)         # Override port
```

### 9.4 The `if __name__ == "__main__"` Pattern

You'll see this in professional code everywhere:

```python
def main():
    create_backups_dir()
    get_netmiko_backups()

if __name__ == "__main__":
    main()
```

**What does this mean?** Every Python file has a special variable called `__name__`. When you run a file directly (`python3 my_script.py`), `__name__` is set to `"__main__"`. When you import the file from another script, `__name__` is set to the file's name.

**Why does this matter?** It lets you write code that behaves differently when run directly vs. imported:

```python
# In backup_utils.py
def backup_device(hostname):
    """Backup a device config."""
    ...

if __name__ == "__main__":
    # Only runs when executed directly: python3 backup_utils.py
    backup_device("core-rtr-01")
```

If another script does `from backup_utils import backup_device`, the code under `if __name__ == "__main__"` does NOT run. This prevents unwanted side effects when importing.

### 9.5 Functions in the Capstone Project

**LABATO-1010 Script 12** (`12-nornir-backup.py`) — Function decomposition:

```python
BACKUP_DIR = "backup/"

def create_backups_dir():
    """Create backup folder if it doesn't exist."""
    if not os.path.exists(BACKUP_DIR):
        os.mkdir(BACKUP_DIR)
```

**Why is `BACKUP_DIR` defined outside the function?** It's a module-level constant (notice the `UPPER_CASE` name). All functions in the file can access it. This avoids hardcoding `"backup/"` in multiple places.

**Why `os.path.exists()` before `os.mkdir()`?** Because `os.mkdir()` crashes if the directory already exists:

```python
>>> os.mkdir("backup")    # First time: works
>>> os.mkdir("backup")    # Second time: crashes!
FileExistsError: [Errno 17] File exists: 'backup'
```

```python
def save_config_to_file(hostname, config):
    """Save a device configuration to a text file."""
    filename = f"{hostname}_nornir.txt"
    with open(os.path.join(BACKUP_DIR, filename), "w") as f:
        f.write(config)
```

**What does `os.path.join()` do?** It combines directory paths correctly for your operating system. `os.path.join("backup/", "csr1_nornir.txt")` produces `"backup/csr1_nornir.txt"`. This is safer than string concatenation because it handles path separators (`/` vs `\`) correctly.

```python
def main():
    """Main function to invoke other functions."""
    create_backups_dir()
    get_netmiko_backups()

if __name__ == "__main__":
    main()
```

**Why a `main()` function?** It gives you a clear entry point. Anyone reading the code immediately sees the high-level workflow: create the directory, then run the backups. The details are in the individual functions.

---

## Chapter 10: Useful Modules

### 10.1 What is a Module and Why Do Modules Exist?

A module is a Python file containing functions, classes, and variables that you can import and use in your own code. Modules prevent you from reinventing the wheel.

**Why do modules exist?** Because Python's philosophy is "batteries included." Instead of writing file-parsing code from scratch, you import `json` or `yaml`. Instead of writing SSH code, you import `netmiko`.

**How to import:**

```python
import os                         # Import the entire module
from getpass import getpass        # Import one specific function
from netmiko import ConnectHandler # Import one specific class
```

**What's the difference?** With `import os`, you access functions as `os.path.exists()`. With `from getpass import getpass`, you access the function directly as `getpass()`.

### 10.2 The `os` Module — Operating System Interactions

```python
import os

# Environment variables
password = os.getenv("NETMIKO_PASSWORD")
```

**What is an environment variable?** A value stored in your operating system's environment, accessible to any program. Think of it like a global variable for your entire system.

**Why use environment variables for passwords?** Because hardcoding passwords in scripts is a security risk. Anyone with access to the code can see the password. Environment variables keep credentials separate from code.

**How to set environment variables:**

```bash
# Linux/Mac — set for current session
$ export NETMIKO_PASSWORD="my_secret_password"

# Verify
$ echo $NETMIKO_PASSWORD
my_secret_password
```

**What if the environment variable isn't set?** `os.getenv()` returns `None`:

```python
>>> os.getenv("NONEXISTENT_VAR")
>>> print(os.getenv("NONEXISTENT_VAR"))
None
```

**The pattern from LABATO-1010:**

```python
password = os.getenv("NETMIKO_PASSWORD") if os.getenv("NETMIKO_PASSWORD") else getpass()
```

**How to read this:** "If the environment variable `NETMIKO_PASSWORD` exists and is not empty, use it. Otherwise, prompt the user with `getpass()`." This allows both automated (CI/CD) and interactive execution.

### 10.3 The `getpass` Module — Secure Password Input

```python
from getpass import getpass

password = getpass('Enter your password: ')
```

**What makes `getpass` different from `input()`?** When you type your password, `getpass()` does NOT display the characters on screen. `input()` shows everything you type.

**What if `getpass()` doesn't hide input?** In some environments (like certain IDEs or Jupyter notebooks), `getpass()` falls back to `input()` with a warning. It still works, but the password will be visible.

### 10.4 The `datetime` Module — Timestamps and Timing

```python
from datetime import datetime

# Current timestamp
print(datetime.now())
# 2024-03-15 14:30:22.123456

# Formatted timestamp for filenames
timestamp = datetime.now().strftime("%Y%m%d_%H%M%S")
backup_filename = f"config_backup_{timestamp}.cfg"
# config_backup_20240315_143022.cfg
```

**What does `strftime()` do?** Converts a datetime object to a formatted string. The format codes:
- `%Y` — 4-digit year (2024)
- `%m` — 2-digit month (03)
- `%d` — 2-digit day (15)
- `%H` — 2-digit hour, 24-hour format (14)
- `%M` — 2-digit minute (30)
- `%S` — 2-digit second (22)

**Measuring script execution time (from LABATO-1010 Script 8):**

```python
start_time = datetime.now()
# ... do work ...
end_time = datetime.now()
print(f"Elapsed: {end_time - start_time}")
# Elapsed: 0:00:45.123456
```

**What does subtracting datetimes give you?** A `timedelta` object representing the duration. Python handles the math automatically.

---

## Chapter 11: Exception Handling

### 11.1 What Are Exceptions and Why Must You Handle Them?

An exception is Python's way of saying "something went wrong." Without exception handling, any error crashes your entire script.

**Why is this critical for network automation?** Because errors are INEVITABLE:
- A device might be unreachable (timeout)
- Credentials might be wrong (authentication failure)
- A command might return unexpected output (parsing error)
- A file might not exist (FileNotFoundError)

If your script connects to 100 devices and the 3rd one is unreachable, you don't want to lose the other 97. Exception handling lets the script continue.

### 11.2 The `try/except` Block

**Twin Bridges Course** (`class1/try_except/try_except_ex1.py`):

```python
fw_service = {
    "uid": "97aeb3d1-9aea-11d5-bd16-0090272ccb30",
    "name": "ftp-port",
    "type": "service-tcp",
    "port": "21",
}

# Without try/except — this CRASHES:
# fw_service["service_type"]    # KeyError!

# With try/except — handled gracefully:
try:
    print("before KeyError")
    fw_service["service_type"]
    print("after KeyError")     # This line NEVER executes
except KeyError:
    print("Inside exception handler")
```

**How does try/except work?**
1. Python executes code inside the `try` block, line by line
2. If an exception occurs, Python IMMEDIATELY jumps to the `except` block
3. Lines after the exception in the `try` block are SKIPPED
4. After the `except` block, execution continues normally

**What happens in this example?**
1. `print("before KeyError")` → runs successfully
2. `fw_service["service_type"]` → KeyError! Key doesn't exist!
3. Python jumps to `except KeyError:` → prints "Inside exception handler"
4. `print("after KeyError")` → NEVER runs (it was after the error in the `try` block)

**What if no exception occurs?** The `except` block is skipped entirely:

```python
try:
    fw_service["name"]        # Key exists — no error
    print("No error occurred")
except KeyError:
    print("This never runs")
```

### 11.3 `try/except/finally` — Guaranteed Cleanup

**Twin Bridges Course** (`class1/try_except/try_except_ex2.py`):

```python
try:
    print("before KeyError")
    fw_service["service_type"]
    print("after KeyError")
except KeyError:
    print("Inside exception handler")
finally:
    print("Always happens")
```

**What does `finally` do?** The `finally` block ALWAYS runs — whether an exception occurred or not. It's for cleanup code that must execute no matter what.

**Why is this important for network automation?** Because you need to disconnect from devices even if an error occurs:

```python
net_connect = None
try:
    net_connect = ConnectHandler(**device)
    output = net_connect.send_command("show version")
    print(output)
except Exception as e:
    print(f"Error: {e}")
finally:
    if net_connect:
        net_connect.disconnect()
        print("Disconnected (cleanup)")
```

**What if I don't disconnect?** The SSH session stays open on the device. If this happens repeatedly, you can exhaust the device's SSH session limit (typically 5-16 sessions), preventing anyone from logging in.

### 11.4 Handling Multiple Exception Types

**LABATO-1010 Script 5** (`5-netmiko-final.py`) — Production error handling:

```python
from netmiko import ConnectHandler
from netmiko import NetmikoAuthenticationException
from netmiko import NetmikoTimeoutException
from paramiko.ssh_exception import SSHException
```

**Why import specific exception types?** So you can handle each type of failure differently. A timeout needs a different response than an authentication failure.

```python
try:
    net_connect = ConnectHandler(**ios_device)
except (NetmikoAuthenticationException):
    print('Authentication failure: ' + ip_address_of_device)
    continue
except (NetmikoTimeoutException):
    print('Timeout to device: ' + ip_address_of_device)
    continue
except (EOFError):
    print("End of file while attempting device " + ip_address_of_device)
    continue
except (SSHException):
    print('SSH Issue. Are you sure SSH is enabled? ' + ip_address_of_device)
    continue
except Exception as unknown_error:
    print('Some other error: ' + str(unknown_error))
    continue
```

**Line-by-line:**

**`except (NetmikoAuthenticationException):`** — Catches wrong username/password. The device rejected our credentials.

**`except (NetmikoTimeoutException):`** — Catches connection timeouts. The device didn't respond within the time limit. This usually means the device is unreachable or the IP is wrong.

**`except (EOFError):`** — Catches "End of File" errors. The SSH connection was established but terminated unexpectedly. This can happen with misconfigured devices.

**`except (SSHException):`** — Catches SSH protocol errors. The TCP connection succeeded but SSH negotiation failed. This happens when SSH is disabled on the device.

**`except Exception as unknown_error:`** — The catch-all. Any exception not caught by the specific handlers above lands here. `as unknown_error` captures the exception object so you can print its message.

**Why `continue` after each exception?** Because this code is inside a `for` loop (iterating through devices). `continue` means "skip this device and move to the next one." Without `continue`, the script would either crash or stop processing devices.

**What is the order of except blocks important?** Yes! Python checks them top-to-bottom. Put the most SPECIFIC exceptions first and the most GENERAL last. If you put `except Exception:` first, it would catch everything, and the specific handlers would never run.

**Netmiko Course** (`class7/collateral/handle_failures.py`) — Same logic as a reusable function:

```python
def netmiko_conn(device):
    """Attempt to connect to a device, handling common failures."""
    try:
        conn = ConnectHandler(**device)
        return conn
    except NetmikoTimeoutException as e:
        if "DNS failure" in str(e):
            print("DNS failure")
        elif "TCP connection to device failed" in str(e):
            print("TCP connection failure")
        else:
            raise
    except NetmikoAuthenticationException:
        print("Authentication failure")
    except SSHException as e:
        if "Error reading SSH protocol banner" in str(e):
            print("SSH banner error")
        else:
            raise
    return None
```

**What does `raise` do?** It re-raises the exception that was caught. Use it when you catch an exception, check its message, and decide it's NOT one you can handle. `raise` passes it up to the caller.

**What does `return None` at the bottom mean?** If any exception was caught (and not re-raised), the function returns `None` to indicate "connection failed." The caller can check for this:

```python
conn = netmiko_conn(device)
if conn is None:
    continue    # Skip this device
print(conn.find_prompt())
```

**Why is this function better than inline error handling?** Because you write the error handling ONCE and reuse it in every script. The LABATO script has the same error handling repeated in scripts 5, 6, and 7. The Netmiko course version extracts it into a function — cleaner, DRY (Don't Repeat Yourself), and easier to maintain.

---

## Chapter 12: Regular Expressions

### 12.1 What Are Regular Expressions and Why Do Network Engineers Need Them?

A regular expression (regex) is a pattern that matches text. Since network device output is unstructured text, regex is one of your primary tools for extracting specific data from show commands.

**When do you need regex?** When string methods like `split()` and `find()` aren't powerful enough. For example, extracting all IP addresses from a block of text — you need a pattern that says "find any sequence of digits.digits.digits.digits."

**When do you NOT need regex?** When simpler tools work. If you just need to check if "up" appears in a string, `"up" in output` is simpler than `re.search(r"up", output)`. Don't use regex when basic string methods suffice.

```python
import re
```

**What is the `re` module?** Python's built-in module for regular expressions. You must import it before using any regex functions.

### 12.2 `re.search()` — Finding the First Match

```python
line = "Interface GigabitEthernet0/1 is up, line protocol is up"
match = re.search(r'Interface (\S+) is (\w+)', line)
if match:
    interface = match.group(1)    # 'GigabitEthernet0/1'
    status = match.group(2)       # 'up'
```

**What does each part mean?**

**`r'Interface (\S+) is (\w+)'`** — The regex pattern. The `r` prefix means "raw string" — backslashes are treated literally, not as escape characters. Always use `r` for regex patterns.

**`Interface `** — Matches the literal text "Interface " (with a space).

**`(\S+)`** — A "capture group" (parentheses) containing `\S+`:
- `\S` means "any non-whitespace character"
- `+` means "one or more"
- So `\S+` matches one or more non-whitespace characters — like `GigabitEthernet0/1`
- The parentheses capture this match so you can retrieve it later with `match.group(1)`

**` is `** — Matches the literal text " is ".

**`(\w+)`** — Another capture group:
- `\w` means "any word character" (letters, digits, underscore)
- `+` means "one or more"
- Captures "up" or "down"

**`match.group(1)`** — Returns the text matched by the first `()` group.
**`match.group(2)`** — Returns the text matched by the second `()` group.
**`match.group(0)`** — Returns the entire match.

**What if the pattern doesn't match?** `re.search()` returns `None`:

```python
match = re.search(r'Interface (\S+)', "No interfaces here")
if match:
    print("Found!")      # Doesn't run
else:
    print("No match")    # This runs
```

**Always check if `match` is not `None` before calling `.group()`!** Otherwise:

```python
match.group(1)    # AttributeError: 'NoneType' object has no attribute 'group'
```

### 12.3 `re.findall()` — Finding All Matches

```python
output = """
Interface         IP-Address      OK? Method Status   Protocol
GigabitEthernet1  10.0.0.1        YES manual up       up
GigabitEthernet2  192.168.1.1     YES manual up       up
Loopback0         1.1.1.1         YES manual up       up
"""

ip_pattern = r'\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}'
ips = re.findall(ip_pattern, output)
print(ips)
# ['10.0.0.1', '192.168.1.1', '1.1.1.1']
```

**What does `\d{1,3}` mean?**
- `\d` — Any digit (0-9)
- `{1,3}` — Between 1 and 3 repetitions
- So `\d{1,3}` matches 1, 2, or 3 digits: "1", "10", "192"

**What does `\.` mean?** A literal dot. Without the backslash, `.` in regex means "any character." We need `\.` to match an actual period.

**Why does `re.findall()` return a list?** Because there can be multiple matches. `re.search()` stops at the first match; `re.findall()` finds all of them.

### 12.4 `re.sub()` — Search and Replace

```python
old_config = "hostname OLD-ROUTER"
new_config = re.sub(r'hostname \S+', 'hostname NEW-ROUTER', old_config)
print(new_config)
# hostname NEW-ROUTER
```

**What does `re.sub()` do?** Finds all occurrences of the pattern and replaces them. The arguments are: `re.sub(pattern, replacement, string)`.

**When is this better than `str.replace()`?** When you need pattern matching. `str.replace()` only matches exact text. `re.sub()` can match patterns like "any hostname" (`\S+`).

### 12.5 Common Regex Patterns for Network Engineers

| Pattern | Meaning | Example Match |
|---------|---------|---------------|
| `\d` | Any digit | `0`, `9` |
| `\d+` | One or more digits | `100`, `4094` |
| `\S+` | One or more non-whitespace | `GigabitEthernet0/1` |
| `\s+` | One or more whitespace | spaces, tabs |
| `\w+` | One or more word characters | `hostname`, `vlan_100` |
| `.+` | One or more of any character | (matches almost anything) |
| `.*` | Zero or more of any character | (matches anything, including empty) |
| `\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}` | IP address pattern | `192.168.1.1` |
| `^` | Start of line | `^interface` matches lines starting with "interface" |
| `$` | End of line | `up$` matches lines ending with "up" |

---

## Chapter 13: CSV, JSON, and YAML — Data Formats for Network Automation

### 13.1 CSV — Spreadsheet-Compatible Reports

**LABATO-1010 Script 10** (`10-netmiko-report.py`) — Writing inventory to CSV:

```python
import csv

inventory = []
title = ["Hostname", "Chassis", "Serial No", "OS", "Version"]
inventory.append(title)
```

**What is `inventory` at this point?** A list containing one list (the header row): `[["Hostname", "Chassis", "Serial No", "OS", "Version"]]`.

**Why a "list of lists"?** Because CSV represents a table. Each inner list is one row. The outer list contains all rows.

```python
# After collecting data from each device:
device_details = ["csr1", "CSR1000V", "9FMKNB70YR1", "IOS-XE", "17.3.4a"]
inventory.append(device_details)
```

Now `inventory` is:
```python
[
    ["Hostname", "Chassis", "Serial No", "OS", "Version"],
    ["csr1", "CSR1000V", "9FMKNB70YR1", "IOS-XE", "17.3.4a"]
]
```

```python
with open("inventory.csv", "w", newline="") as f:
    writer = csv.writer(f)
    writer.writerows(inventory)
```

**What does `newline=""`do?** It prevents the CSV writer from adding extra blank lines between rows on Windows. Always include it.

**What does `writer.writerows()` do?** Writes ALL rows at once. `writer.writerow()` (singular) writes one row at a time.

**The resulting CSV file:**
```
Hostname,Chassis,Serial No,OS,Version
csr1,CSR1000V,9FMKNB70YR1,IOS-XE,17.3.4a
```

This file can be opened directly in Excel or Google Sheets.

---

## Chapter 14: Connecting to Devices with Netmiko

### 14.1 Your First Netmiko Connection — Every Line Explained

**LABATO-1010 Script 1** (`1-netmiko-show.py`):

```python
#!/usr/bin/env python
from netmiko import ConnectHandler
```

**What does this import do?** It brings in the `ConnectHandler` class from the `netmiko` library. `ConnectHandler` is the main object that establishes SSH connections to network devices.

**What if Netmiko isn't installed?**

```python
ModuleNotFoundError: No module named 'netmiko'
```

Fix: `pip install netmiko` (inside your virtual environment).

```python
ios1 = {
    'device_type': 'cisco_ios',
    'ip': '198.18.1.11',
    'username': 'cisco',
    'password': 'cisco',
}
```

**What is `device_type`?** It tells Netmiko what kind of device you're connecting to. Netmiko supports 100+ device types. The `device_type` determines:
- What SSH parameters to use
- What the command prompt looks like
- How to enter config mode
- How to save configuration

**What happens if I use the wrong `device_type`?** Netmiko will connect via SSH but may hang waiting for a prompt it doesn't recognize, or send incorrect commands. Always verify the correct `device_type`.

**Common device types:** `cisco_ios`, `cisco_nxos`, `cisco_xr`, `arista_eos`, `juniper_junos`, `paloalto_panos`, `checkpoint_gaia`

```python
net_connect = ConnectHandler(**ios1)
```

**What happens when this line executes?**
1. Netmiko resolves the hostname/IP to a network address
2. Opens a TCP connection to port 22 (SSH)
3. Performs SSH key exchange and authentication
4. Logs in with the provided username/password
5. Detects the device prompt (e.g., `Router#`)
6. Returns a connection object

**How long does this take?** Typically 2-10 seconds, depending on network latency and device response time.

**What if the device is unreachable?** After a timeout (default ~10 seconds), Netmiko raises `NetmikoTimeoutException`.

```python
output = net_connect.send_command('show version')
```

**What does `send_command()` do step by step?**
1. Sends the string `"show version"` to the device via SSH
2. Presses Enter (sends `\n`)
3. Waits for the device to respond
4. Collects ALL output until the device prompt reappears
5. Returns the output as a string (WITHOUT the command itself or the prompt)

**What if the command produces a lot of output?** Netmiko handles paging automatically. If the device shows `--More--`, Netmiko sends a space to continue. You don't need to worry about `terminal length 0`.

**What if the command takes a long time?** By default, Netmiko waits up to 100 seconds. If the command takes longer (like a large `show tech-support`), you can increase it: `net_connect.send_command('show tech', read_timeout=300)`.

```python
net_connect.disconnect()
```

**Why disconnect?** To close the SSH session and free up resources on both the device and your machine. Network devices have limited SSH session slots (typically 5-16). If you don't disconnect, you'll eventually exhaust them.

```python
print(output)
```

**What does `output` contain?** The raw text output of `show version`, exactly as it would appear on the device CLI, minus the command echo and prompt.

### 14.2 Context Manager Connection

**Netmiko Course** (`class1/collateral/simple_conn_cm.py`):

```python
my_device = {
    "device_type": "cisco_ios",
    "host": "cisco3.lasthop.io",
    "username": "pyclass",
    "password": password,
}

with ConnectHandler(**my_device) as net_connect:
    print(net_connect.find_prompt())

print("Connection automatically closed")
```

**Why use `with`?** The `with` statement automatically calls `disconnect()` when the indented block ends — even if an error occurs inside the block. This is safer than manual `disconnect()`.

**What does `find_prompt()` return?** The current device prompt as a string, like `"cisco3#"` or `"core-rtr-01>"`. The capstone project uses `find_prompt()[:-1]` to get the hostname without the trailing `#` or `>`.

### 14.3 Parsing Output with TextFSM

**Netmiko Course** (`class3/collateral/show_textfsm.py`):

```python
output = net_connect.send_command("show ip int brief", use_textfsm=True)
pprint(output)
```

**What does `use_textfsm=True` do?** Instead of returning raw text, Netmiko uses TextFSM templates to parse the output into a list of dictionaries:

```python
[{'intf': 'GigabitEthernet0/0', 'ipaddr': '10.0.12.1', 'proto': 'up', 'status': 'up'},
 {'intf': 'GigabitEthernet0/1', 'ipaddr': '10.0.13.1', 'proto': 'up', 'status': 'up'}]
```

**Why is this better than raw text?** Because you can access fields by name instead of parsing columns:

```python
for interface in output:
    if interface['status'] == 'up':
        print(f"{interface['intf']} - {interface['ipaddr']}")
```

**What if TextFSM doesn't have a template for your command?** It returns the raw text string as a fallback. Your code should handle both cases.

---

## Chapter 15: Sending Configuration Commands

### 15.1 `send_config_set()` — Pushing Configuration

**LABATO-1010 Script 2** (`2-netmiko-config.py`):

```python
net_connect = ConnectHandler(**ios1)
output = net_connect.send_config_set('logging host 10.1.1.1')
net_connect.disconnect()
print(output)
```

**What does `send_config_set()` do step by step?**
1. Enters configuration mode (`configure terminal`)
2. Sends the command(s) you specified
3. Exits configuration mode (`end`)
4. Returns all the output from the session

**What's the difference between `send_command()` and `send_config_set()`?**
- `send_command()` — For show commands (privileged exec mode)
- `send_config_set()` — For configuration commands (global config mode)

**Can I send multiple commands?** Yes, pass a list:

```python
commands = ['logging host 10.1.1.1', 'ntp server 10.1.1.2', 'no ip http server']
output = net_connect.send_config_set(commands)
```

### 15.2 `send_config_from_file()` — Configuration from a File

**LABATO-1010 Script 4** (`4-netmiko-config.py`):

```python
net_connect = ConnectHandler(**ios_device)
output = net_connect.send_config_from_file('config_commands')
net_connect.disconnect()
```

**What does `send_config_from_file()` do?** It reads configuration commands from a text file (one command per line) and sends them to the device. It's equivalent to reading the file yourself and passing the lines to `send_config_set()`.

**Why use a file instead of a list?** Because configuration files can be:
- Reviewed before execution (peer review, change management)
- Version-controlled in Git
- Reused across multiple scripts
- Edited without modifying Python code

### 15.3 `save_config()` — Writing Memory

```python
output = net_connect.send_config_from_file('config_commands')
output += net_connect.save_config()
```

**What does `save_config()` do?** It runs `write memory` (or `copy running-config startup-config`) on the device to persist the configuration.

**Why `output +=`?** The `+=` operator appends the save_config output to the existing output string. This gives you a complete log of everything that happened.

**What if I don't call `save_config()`?** Your changes only exist in the running-config. If the device reboots, all changes are lost. Always save after configuring.

---

## Chapter 16: Configuration Backup

### 16.1 The Complete Backup Script — Every Line Explained

**LABATO-1010 Script 8** (`8-netmiko_backup.py`):

```python
#!/usr/bin/env python
import os, time
from datetime import datetime
from getpass import getpass
from netmiko import ConnectHandler

print(datetime.now())
```

**Why print the timestamp?** To record when the backup operation started. Combined with the timestamp at the end, you can measure how long the entire backup took.

```python
password = os.getenv("NETMIKO_PASSWORD") if os.getenv("NETMIKO_PASSWORD") else getpass()
username = os.getenv("NETMIKO_USERNAME") if os.getenv("NETMIKO_USERNAME") else input('Enter username: ')
```

**What is this pattern?** A ternary expression (conditional expression). Read it as: "If the environment variable exists, use it. Otherwise, prompt the user."

```python
if not os.path.exists('backup/'):
    os.mkdir('backup')
```

**Why check before creating?** Because `os.mkdir()` raises `FileExistsError` if the directory already exists. Checking first prevents the error.

```python
with open('device_list') as f:
    device_list = f.read().splitlines()
```

**We've seen this pattern many times now.** It reads IP addresses from a file into a list. This is the standard way to get a device list in network automation.

```python
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
```

**Why build the dictionary inside the loop?** Because the `ip` value changes for each device. The dictionary is rebuilt with the current device's IP on each iteration.

```python
    hostname = net_connect.find_prompt()[:-1]
```

**What does `find_prompt()[:-1]` do?**
1. `find_prompt()` returns the device prompt: `"csr1#"`
2. `[:-1]` slices off the last character (the `#` or `>`)
3. Result: `"csr1"` — the hostname

**Why extract the hostname this way?** Because you want backup files named after the device (`csr1.cfg`), and the prompt is the easiest way to get the hostname without parsing `show version`.

```python
    output = net_connect.send_command("show run")

    with open(f'backup/{hostname}.cfg', 'w') as file:
        file.write(output)
```

**What does `f'backup/{hostname}.cfg'` create?** A filename like `backup/csr1.cfg`. The f-string inserts the hostname dynamically.

```python
    net_connect.disconnect()
    time.sleep(3)
```

**Why `time.sleep(3)`?** Adds a 3-second delay between devices. This prevents overwhelming the network or devices with rapid consecutive connections. In production, you might adjust this based on your environment.

---

## Chapter 17: Concurrent Connections

### 17.1 Why Concurrency?

If each device connection takes 5 seconds and you have 100 devices, sequential execution takes **500 seconds (8+ minutes)**. With 20 concurrent threads, it takes roughly **25 seconds**. That's a 20x speedup.

**Why does sequential execution take so long?** Because most of the time is spent WAITING — waiting for TCP connections, waiting for SSH handshakes, waiting for device responses. Your CPU is idle during all this waiting.

**How does threading help?** While Thread 1 waits for Device 1 to respond, Thread 2 connects to Device 2, Thread 3 connects to Device 3, etc. The waiting time overlaps instead of adding up.

### 17.2 ThreadPoolExecutor — The Modern Approach

**Twin Bridges Course** (`class4/concurrency/ssh_threads_ascompleted.py`):

```python
from concurrent.futures import ThreadPoolExecutor, as_completed
from datetime import datetime
from netmiko import ConnectHandler
from my_devices import device_list
```

**What is `concurrent.futures`?** Python's standard library for running tasks in parallel. It provides `ThreadPoolExecutor` for I/O-bound tasks (like SSH connections) and `ProcessPoolExecutor` for CPU-bound tasks.

**Why `ThreadPoolExecutor` and not `ProcessPoolExecutor`?** SSH connections are I/O-bound — the bottleneck is network latency, not CPU processing. Threads are lightweight and perfect for this. Processes have more overhead and are better for CPU-intensive tasks.

```python
def ssh_conn(device):
    net_connect = ConnectHandler(**device)
    return net_connect.find_prompt()
```

**Why define a function?** `ThreadPoolExecutor` runs functions in parallel. Each thread calls this function with a different device dictionary.

```python
if __name__ == "__main__":
    start_time = datetime.now()
    max_threads = 4

    pool = ThreadPoolExecutor(max_threads)
```

**What is `max_threads = 4`?** The maximum number of simultaneous connections. More threads = faster, but too many can overwhelm your network or devices. Start with 4-10 and increase carefully.

```python
    future_list = []
    for a_device in device_list:
        future = pool.submit(ssh_conn, a_device)
        future_list.append(future)
```

**What does `pool.submit()` do?** It schedules the function to run in a thread and returns a `Future` object immediately — it does NOT wait for the function to finish. The actual SSH connection happens in the background.

**What is a `Future`?** A placeholder for a result that doesn't exist yet. When the thread finishes, the result becomes available through `future.result()`.

```python
    for future in as_completed(future_list):
        print("Result: " + future.result())
```

**What does `as_completed()` do?** It yields futures as they finish — the fastest device's result comes first, regardless of the order they were submitted. This is efficient because you process results as soon as they're available.

**What if a thread raises an exception?** `future.result()` re-raises the exception in the main thread. You should wrap it in try/except:

```python
for future in as_completed(future_list):
    try:
        print("Result: " + future.result())
    except Exception as e:
        print(f"Error: {e}")
```

---

## Chapter 18: Classes and Objects

### 18.1 What is Object-Oriented Programming and Why Do You Need It?

So far, you've organized code using functions. Functions group behavior. But what about grouping behavior WITH data? A class bundles data (attributes) and behavior (methods) into a single, reusable unit.

**Why do network engineers need classes?** Consider a network device. It has:
- **Data:** hostname, IP address, device type, credentials, connection state
- **Behavior:** connect, disconnect, send commands, backup config, parse output

A class lets you combine all of this into one `NetworkDevice` object.

**Analogy:** A class is like a device template in Cisco DNA Center. The template defines the properties (hostname, IP, model) and capabilities (configure, monitor, backup). Each actual device created from the template is an "instance" of that template.

### 18.2 Anatomy of a Class

**Twin Bridges Course** (`class3/gaia_class/gaia_class.py`):

```python
class GaiaAuthError(Exception):
    """Exception raised when the session ID is missing or expired."""
    pass
```

**What does this do?** It creates a custom exception type. `class` defines a new type. `(Exception)` means it inherits from Python's built-in `Exception` class.

**Why create custom exceptions?** So you can catch specific errors. `except GaiaAuthError` is more meaningful than a generic `except Exception`.

**What does `pass` do?** It's a placeholder that means "this block is intentionally empty." The class inherits everything it needs from `Exception`, so no additional code is required.

```python
class GaiaAPI:
    def __init__(self, host, username, password, api_version="1.8",
                 ssl_verify=False):
        self.host = host
        self.username = username
        self.password = password
        self.base_url = f"https://{host}/gaia_api/v{api_version}/"
        self.headers = {"Content-Type": "application/json"}
        self.ssl_verify = ssl_verify
```

**What is `class GaiaAPI:`?** It defines a new class named `GaiaAPI`. By convention, class names use `PascalCase` (each word capitalized, no underscores).

**What is `__init__`?** The "initializer" method (sometimes called the constructor). It runs automatically when you create a new object: `api_client = GaiaAPI(...)`. Its job is to set up the initial state of the object.

**What is `self`?** A reference to the specific object being created. Every method in a class must have `self` as its first parameter. When you call `api_client.login()`, Python passes `api_client` as `self` automatically.

**What does `self.host = host` do?** It stores the `host` parameter as an **instance attribute** — data that belongs to this specific object. Different objects can have different values:

```python
fw1 = GaiaAPI(host="fw1.example.com", username="admin", password="secret1")
fw2 = GaiaAPI(host="fw2.example.com", username="admin", password="secret2")
# fw1.host is "fw1.example.com"
# fw2.host is "fw2.example.com"
# They are independent — changing one doesn't affect the other
```

**What does `api_version="1.8"` mean?** A default parameter. If the caller doesn't specify an API version, it defaults to "1.8". This is the same as default arguments in functions (Chapter 9).

```python
    def login(self):
        login_payload = {"user": self.username, "password": self.password}
        url = self.base_url + "login"
        response = requests.post(
            url,
            data=json.dumps(login_payload),
            headers=self.headers,
            verify=self.ssl_verify,
        )
        resp_struct = response.json()
        self.headers["X-chkp-sid"] = resp_struct["sid"]
```

**What does `self.headers["X-chkp-sid"] = resp_struct["sid"]` do?** After a successful login, the API returns a session ID (`sid`). This line stores it in the headers dictionary so that subsequent API calls are authenticated.

**Why is this powerful?** Because the session state is managed internally. The caller doesn't need to track session IDs — they just call `login()` once and then use `call()` for every request.

```python
    def call(self, endpoint, payload=None):
        url = self.base_url + endpoint
        if payload is None:
            payload = {}
        if "X-chkp-sid" not in self.headers:
            raise GaiaAuthError(
                "Session ID not set, please call '.login()' method"
            )
        response = requests.post(
            url, data=json.dumps(payload),
            headers=self.headers, verify=self.ssl_verify
        )
        return response
```

**Why check for `"X-chkp-sid"` in headers?** To prevent making API calls without being authenticated. If someone forgets to call `login()` first, this raises a clear error instead of getting a confusing 401 response from the API.

**Why `payload=None` instead of `payload={}`?** This is a Python gotcha. Default mutable arguments (like `{}`) are shared between all calls. If one call modifies the default dict, it affects subsequent calls. Using `None` and creating a new dict inside the function avoids this:

```python
# WRONG — shared mutable default
def call(self, endpoint, payload={}):    # Same dict object every time!
    payload["extra"] = "data"            # Modifies the default for ALL future calls

# RIGHT — safe pattern
def call(self, endpoint, payload=None):
    if payload is None:
        payload = {}                      # Fresh dict every time
```

### 18.3 Using the Class

```python
if __name__ == "__main__":
    api_client = GaiaAPI(host="chkpnt-pod99.lasthop.io",
                         username="admin", password=admin_pass)
    api_client.login()

    res = api_client.call(endpoint="show-version")
    print(res.json())

    api_client.logout()
```

**What is `api_client`?** An **instance** (object) of the `GaiaAPI` class. It has its own `host`, `username`, `password`, `headers`, etc.

**What does `api_client.login()` do?** Calls the `login` method on this specific object. Python translates this to `GaiaAPI.login(api_client)` — the object is passed as `self`.

**What does `api_client.call(endpoint="show-version")` do?** Calls the `call` method, which builds the URL, adds authentication headers, makes the HTTP request, and returns the response.

**Why is this better than functions?** Because all the state (session ID, base URL, headers) is bundled with the object. With functions, you'd have to pass these as parameters to every function call.

---

## Chapter 19: Testing with pytest

### 19.1 Why Test Network Automation Code?

Testing verifies that your code works correctly before you deploy it against production devices.

**Why not just test manually?** Because:
- Manual testing is slow and error-prone
- You can't manually test every edge case
- After changing code, you need to re-test everything — manually doing this every time is impractical
- Tests serve as documentation of expected behavior

### 19.2 Writing Your First Test

**Twin Bridges Course** (`class3/test_pytest_ex/some_funcs.py`) — Functions to test:

```python
def simple_sum(x, y):
    return x + y

def simple_div(x, y):
    return x / y
```

**Twin Bridges Course** (`class3/test_pytest_ex/test_simple.py`) — Tests:

```python
from some_funcs import simple_sum

def test_sums():
    assert simple_sum(1, 7) == 8
    assert simple_sum(0, 0) == 0

def test_negative_sums():
    assert simple_sum(-1, -1) == -2
```

**How does pytest find tests?** By convention:
1. Test files must be named `test_*.py` or `*_test.py`
2. Test functions must be named `test_*`
3. pytest discovers and runs them automatically

**What does `assert` do?** It checks if a condition is `True`. If `True`, nothing happens (test passes). If `False`, the test fails with a detailed error message.

```python
assert simple_sum(1, 7) == 8
```

**Reading this:** "Assert that `simple_sum(1, 7)` equals `8`." If `simple_sum` returns `8`, the assert passes silently. If it returns anything else, pytest reports a failure showing what was expected vs. what was received.

**How to run tests:**

```bash
$ pytest test_simple.py -v
test_simple.py::test_sums PASSED
test_simple.py::test_negative_sums PASSED
```

**What does `-v` do?** Verbose output — shows each test name and its result.

### 19.3 Advanced pytest Features

**Twin Bridges Course** (`class3/test_pytest_ex/test_some_funcs.py`):

```python
@pytest.mark.parametrize(
    "val1, val2, result",
    [(10, 5, 15), (-1, 1, 0), (0, 0, 0), (100, 200, 300)]
)
def test_addition(val1, val2, result):
    assert simple_sum(val1, val2) == result
```

**What is `@pytest.mark.parametrize`?** A decorator that runs the same test function with multiple sets of inputs. Instead of writing four separate test functions, you write one and provide the data.

**How to read this:** "Run `test_addition` four times: once with (10, 5, 15), once with (-1, 1, 0), once with (0, 0, 0), and once with (100, 200, 300). In each run, check that `simple_sum(val1, val2)` equals `result`."

```python
def test_exception():
    with pytest.raises(ZeroDivisionError):
        simple_div(10, 0)
```

**What does `pytest.raises()` do?** It asserts that a specific exception IS raised. The test PASSES if `ZeroDivisionError` occurs. The test FAILS if no exception occurs.

**Why test for exceptions?** Because you want to verify that your code fails correctly. If `simple_div(10, 0)` somehow returned a value instead of raising an error, that would be a bug.

```python
@pytest.mark.skipif(
    sys.version_info.major == 3 and sys.version_info.minor == 13,
    reason="Skip test on PY3.13",
)
def test_skip_example():
    assert simple_sum(-7, 7) == 0
```

**What does `@pytest.mark.skipif` do?** Conditionally skips the test based on a condition. Here, the test is skipped on Python 3.13 (perhaps due to a known incompatibility). The `reason` parameter documents WHY it's skipped.

---

## Chapter 20: Capstone Project — From First Connection to Full Automation

### 20.1 Project Overview

The LABATO-1010 project is a sequence of 12 Python scripts that progressively build a complete network automation toolkit. Each script adds ONE new concept to the previous one, creating a clear learning path.

**Lab topology:** Two Cisco CSR1000V routers at `198.18.1.11` and `198.18.1.12`.

**The progression:**
| Script | New Concept Added | Chapter Reference |
|--------|-------------------|-------------------|
| 1 | First SSH connection + show command | Ch. 14 |
| 2 | First config change | Ch. 15 |
| 3 | Loop over multiple devices | Ch. 6 |
| 4 | Read devices and commands from files | Ch. 7 |
| 5 | Exception handling for production use | Ch. 11 |
| 6 | Environment variables for credentials | Ch. 10 |
| 7 | Multiple show commands from file | Ch. 6 + 7 |
| 8 | Full config backup with timestamps | Ch. 16 |
| 9 | Structured output with Genie parser | Ch. 8 |
| 10 | CSV inventory report with tabulate | Ch. 13 |
| 11 | Nornir framework basics | Ch. 17 |
| 12 | Nornir backup with functions | Ch. 9 |

### 20.2 Script 1 → Script 2: Adding Configuration

**Script 1** uses `send_command()` to READ from the device.
**Script 2** uses `send_config_set()` to WRITE to the device.

The only change between the two scripts is the method called. Everything else — the dictionary, the import, the connection — is identical. This demonstrates that reading and writing to network devices follows the same pattern.

### 20.3 Script 2 → Script 3: Scaling to Multiple Devices

**Script 2** configures ONE device (one dictionary, one connection).
**Script 3** configures TWO devices by putting dictionaries into a list and using a `for` loop.

**This is the most important transition in the entire book.** The jump from "one device" to "many devices" is just:
1. Put dictionaries in a list: `devices = [ios1, ios2]`
2. Wrap the logic in a for loop: `for device in devices:`

Everything inside the loop is identical to the single-device version. The loop just runs it multiple times.

### 20.4 Script 3 → Script 4: Externalizing Data

**Script 3** has hardcoded IP addresses and credentials in the code.
**Script 4** reads IPs from a file and gets credentials from user input.

This is the jump from "lab script" to "something shareable." You can now give this script to a colleague — they just need the `device_list` file and their own credentials. They don't need to edit the Python code.

### 20.5 Script 4 → Script 5: Production Error Handling

**Script 4** crashes if any device is unreachable.
**Script 5** catches every possible SSH error and continues to the next device.

This is the jump from "lab script" to "production tool." Script 5 can run against 100 devices, handle 10 failures gracefully, and still successfully configure the other 90.

### 20.6 Script 5 → Script 6: Automated Execution

**Script 5** always prompts for credentials.
**Script 6** checks environment variables first, only prompting if they're not set.

This enables non-interactive execution: cron jobs, CI/CD pipelines, Ansible integration. The script works the same way in both modes.

### 20.7 Script 8: The Complete Backup Solution

Script 8 is where EVERYTHING comes together. Let's trace every concept:

```python
#!/usr/bin/env python
import os, time                           # Ch. 10 — Modules
from datetime import datetime             # Ch. 10 — datetime module
from getpass import getpass               # Ch. 10 — Secure password input
from netmiko import ConnectHandler        # Ch. 14 — Netmiko

print(datetime.now())                     # Ch. 10 — Timestamp

password = os.getenv("NETMIKO_PASSWORD") if os.getenv("NETMIKO_PASSWORD") else getpass()
# Ch. 5 — Conditional expression
# Ch. 10 — os.getenv() and getpass()

if not os.path.exists('backup/'):         # Ch. 5 — if statement, Ch. 10 — os.path
    os.mkdir('backup')                    # Ch. 10 — os.mkdir

with open('device_list') as f:            # Ch. 7 — File reading
    device_list = f.read().splitlines()   # Ch. 3 — String methods, Ch. 4 — Lists

for devices in device_list:               # Ch. 6 — For loop
    ios_device = {                        # Ch. 4 — Dictionary
        'device_type': 'cisco_ios',
        'ip': devices,
        'username': username,
        'password': password
    }

    net_connect = ConnectHandler(**ios_device)   # Ch. 4 — Dict unpacking, Ch. 14 — Netmiko
    hostname = net_connect.find_prompt()[:-1]    # Ch. 3 — String slicing

    output = net_connect.send_command("show run") # Ch. 14 — send_command

    with open(f'backup/{hostname}.cfg', 'w') as file:  # Ch. 7 — File writing, Ch. 3 — f-string
        file.write(output)

    net_connect.disconnect()              # Ch. 14 — Connection cleanup
    time.sleep(3)                         # Ch. 10 — time module

print(datetime.now())                     # Ch. 10 — End timestamp
```

**Every single line traces back to a chapter you've already learned.** This is the power of building skills incrementally — Script 8 uses concepts from Chapters 3, 4, 5, 6, 7, 10, and 14, and you understand every one of them.

### 20.8 Script 10: The Full Inventory Report

Script 10 adds Genie parsing and CSV export. The new concepts from this script:

```python
output = net_connect.send_command('show version', use_genie=True)
```

**Genie parsing** (Ch. 8) converts raw text to a structured dictionary.

```python
hostname = output["version"]["hostname"]
chassis = output["version"]["chassis"]
```

**Nested dictionary access** (Ch. 4/8) navigates the parsed structure.

```python
print(tabulate(inventory, headers="firstrow", tablefmt="grid"))
```

**tabulate** (Ch. 10) creates a beautiful ASCII table from the inventory list.

```python
with open("inventory.csv", "w", newline="") as f:
    writer = csv.writer(f)
    writer.writerows(inventory)
```

**CSV export** (Ch. 13) saves the inventory to a spreadsheet-compatible file.

### 20.9 Scripts 11-12: Nornir Framework

These final scripts introduce Nornir, which replaces your hand-crafted loops and device management with a professional framework.

**What does Nornir provide that your scripts don't?**
- YAML-based inventory management
- Built-in threading (no manual ThreadPoolExecutor)
- Result collection and error handling per device
- Plugin architecture for extensibility

The YAML inventory files replace the flat `device_list` file, and `nr.run()` replaces your `for` loop.

---

## Chapter 21: Where to Go From Here

### 21.1 What You Can Now Do

After completing this book, you can:

1. Write Python scripts from scratch using proper syntax, data types, and control flow
2. Connect to network devices via SSH and send show/config commands
3. Parse unstructured text output using string methods, regex, TextFSM, and Genie
4. Handle errors gracefully so scripts survive production failures
5. Organize code into reusable functions and classes
6. Work with structured data in JSON, YAML, and CSV formats
7. Scale automation with concurrent connections
8. Test your code with pytest
9. Understand and modify any script from the Twin Bridges, Netmiko, or LABATO courses

### 21.2 Recommended Next Steps

- **NAPALM** — Multi-vendor network abstraction library
- **Ansible** — Agentless automation using YAML playbooks
- **REST APIs** — Cisco DNA Center, Meraki, ACI, NSO
- **YANG/NETCONF/RESTCONF** — Model-driven programmability
- **CI/CD Pipelines** — GitHub Actions, GitLab CI for NetDevOps
- **Terraform** — Infrastructure as Code

### 21.3 Resources

- PyNEng Book: `https://pyneng.readthedocs.io/en/latest/`
- Twin Bridges Free Course: `https://pynet.twb-tech.com/free-python-course.html`
- Cisco DevNet: `https://developer.cisco.com/learning/modules/`
- Netmiko Docs: `https://github.com/ktbyers/netmiko`
- Nornir Docs: `https://nornir.readthedocs.io/en/latest/`

---

*End of Book*
