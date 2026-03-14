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
```

**What is `pip`?** It's Python's package manager, like `apt` on Ubuntu or `yum` on CentOS. It downloads and installs Python packages from PyPI (the Python Package Index — think of it as the "app store" for Python libraries).

**What are these packages?**
- `netmiko` — Connects to network devices via SSH (Cisco, Arista, Juniper, etc.)
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
        "name": "Cisco Security Domain",
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
'Cisco Security Domain'

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


---

## Chapter 5: Control Flow — if/elif/else

### 5.1 What is Control Flow and Why Does It Matter?

Every script you've written so far executes top-to-bottom, every line, every time. But real network automation requires decisions: Is the device reachable? Is the interface up? Is the firmware current? Control flow statements let your code make these decisions.

**Analogy:** Control flow is like a route-map on a Cisco router. A route-map evaluates conditions and takes different actions depending on the match. An `if` statement does the same thing for your Python code.

### 5.2 The `if` Statement

```python
vlan_id = 100

if vlan_id == 100:
    print("This is the management VLAN")
```

**Line-by-line:**

- **`vlan_id = 100`** — Creates a variable with integer value `100`.
- **`if vlan_id == 100:`** — The `if` keyword starts a conditional check. `vlan_id == 100` is the condition (is vlan_id equal to 100?). The `:` colon is REQUIRED — it tells Python "an indented block follows."
- **`print("This is the management VLAN")`** — This indented line only runs when the condition is `True`.

**What if the condition is False?** The indented block is skipped entirely. Execution continues at the next unindented line.

**What if I forget the colon?** `SyntaxError: expected ':'` — Python tells you exactly what's missing.

**What if I forget to indent?** `IndentationError: expected an indented block` — Python expected code inside the `if` block.

### 5.3 The `if/elif/else` Statement

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

**How does `elif` work?** Python checks conditions top-to-bottom. Once it finds a `True` condition, it runs that block and SKIPS everything else. Only ONE block ever runs.

**What if conditions overlap?** Order matters. Put the most specific conditions first.

**Is `else` required?** No. It's optional — a catch-all for when nothing matches.

### 5.4 Twin Bridges Course — Conditional Logic with Network Services

**Script:** `python_course_mar26/class1/cond/cond_ex1.py`

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

**Why is this useful?** This is exactly how you process API output from a Cisco device — load JSON, iterate through results, take different actions based on what you find.

### 5.5 Twin Bridges Course — Compound Conditions

**Script:** `python_course_mar26/class1/cond/cond_ex5.py`

```python
#!/usr/bin/env python
import yaml

with open("api_support_versions.yml") as f:
    api_versions = yaml.safe_load(f)

supported_versions = api_versions["supported-versions"]

if "1.8" in supported_versions:
    api_version = "1.8"

api_version = "1.8"
if "1." in api_version:
    base_api = "v1"
elif "2." in api_version:
    base_api = "v2"

if base_api == "v1" and float(api_version) >= 1.8:
    print("API Version 1.8 or later (not V2)")

if base_api == "v1" or base_api == "v2":
    print("API V1 or V2")
```

**What does `"1.8" in supported_versions` do?** The `in` operator checks if a value exists in a list. If `"1.8"` is found, the condition is `True`.

**Why `float(api_version)`?** String comparison is alphabetical, not numerical: `"1.8" > "1.10"` is `True` (wrong!). Converting to float gives correct numeric comparison.

### 5.6 Twin Bridges Exercise — User Input

**Script:** `python_course_mar26/class1/exercises/cond_ex/cond_ex1.py`

```python
#!/usr/bin/env python

pod_numb = input("Enter pod number: ")
fw_name = f"cisco-fw-pod{pod_numb}"

if fw_name == "cisco-fw-pod1":
    print("Found pod1")
elif fw_name == "cisco-fw-pod99":
    print("Found pod99")
else:
    print("Not my pod")
```

**Critical point:** `input()` ALWAYS returns a string. Even if the user types `99`, `pod_numb` is the string `"99"`, not the number `99`.

### 5.7 Booleans and Truthiness

**Script:** `python_course_mar26/class1/booleans/truish.py`

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

**The rule:** "Empty" or "zero" values are `False`. Everything else is `True`.

**Why does this matter?** Clean network automation code:

```python
# Pythonic — uses truthiness
if output:
    print("Got output from device")

if not device_list:
    print("No devices to connect to!")
```

### 5.8 Short-Circuit Evaluation

**Script:** `python_course_mar26/class1/booleans/show_circuit.py`

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

**Why does this matter?** Safe code:

```python
# Safe — if device_list is empty, Python never evaluates device_list[0]
if device_list and device_list[0] == "10.0.0.1":
    print("First device is the core router")
```

### 5.9 The `in` Operator

```python
allowed_vlans = [10, 20, 30, 40, 50]
if 30 in allowed_vlans:
    print("VLAN 30 is allowed")

show_output = "Interface GigabitEthernet0/1 is up, line protocol is up"
if "is up" in show_output:
    print("Interface is operational")

device_type = "cisco_ios"
if device_type in ('cisco_ios', 'cisco_nxos', 'arista_eos'):
    print(f"Supported platform: {device_type}")
```

**The `in` operator never crashes.** It always returns `True` or `False`.

---

## Chapter 6: Loops — Iterating Over Network Devices

### 6.1 Why Do Network Engineers Need Loops?

A loop repeats a block of code multiple times. Without loops, automating 100 devices requires writing the same code 100 times. With a loop, you write it once.

### 6.2 The `for` Loop

**Script:** `python_course_mar26/class1/loops/loop_ex1.py`

```python
from rich import print

for loop_var in ["hello", "world", "something", "else"]:
    print(loop_var)
```

**How to read this:** `for loop_var in [list]:` — "For each item in the list, assign it to `loop_var` and run the indented block."

**What happens at runtime?**
1. `loop_var = "hello"` → print "hello"
2. `loop_var = "world"` → print "world"
3. `loop_var = "something"` → print "something"
4. `loop_var = "else"` → print "else"
5. No more items → loop ends

**What if the list is empty?** Zero iterations. The loop body is skipped. No error.

### 6.3 Accessing Elements Inside a Loop

**Script:** `python_course_mar26/class1/loops/loop_ex2.py`

```python
from rich import print

my_list = ["hello", "world", "something", "else"]
for loop_var in my_list:
    print(loop_var)
    print(loop_var[0])     # First character
    print(loop_var[-1])    # Last character
```

**What does `loop_var[0]` do?** Since `loop_var` is a string in each iteration, `[0]` gets the first character. In iteration 1, `loop_var` is `"hello"`, so `loop_var[0]` is `"h"`.

### 6.4 `break` — Stop the Loop Early

**Script:** `python_course_mar26/class1/loops/loop_ex3.py`

```python
from rich import print

my_list = ["hello", "world", "something", "else"]

for loop_var in my_list:
    if loop_var == "something":
        print("\n\nAll done!\n")
        break
    print(loop_var)
    print("...still in the loop")
```

**What does `break` do?** Immediately exits the loop. No more iterations happen.

**Output:**
```
hello
...still in the loop
world
...still in the loop


All done!
```

Notice `"else"` is never reached — `break` stopped the loop at `"something"`.

### 6.5 `continue` — Skip This Iteration

**Script:** `python_course_mar26/class1/loops/loop_ex4.py`

```python
from rich import print

my_list = ["hello", "world", "something", "else"]

for loop_var in my_list:
    if loop_var == "something":
        print("<skip>")
        continue
    print(loop_var)
    print("...still in the loop")
```

**Key difference from `break`:** `continue` skips ONE iteration. `break` stops the ENTIRE loop.

### 6.6 `enumerate()` — Get Index and Value Together

**Script:** `python_course_mar26/class1/loops/loop_ex5.py`

```python
from rich import print

my_list = ["hello", "world", "something", "else"]
for idx, loop_var in enumerate(my_list):
    print(f"{idx} --> {loop_var}")
```

**Output:**
```
0 --> hello
1 --> world
2 --> something
3 --> else
```

**Why use `enumerate()`?** When you need both the position number AND the value.

### 6.7 Looping Over Dictionaries

**Script:** `python_course_mar26/class1/loops/loop_ex6.py`

```python
#!/usr/bin/env python
from rich import print

cisco_service = {
    "uid": "97aeb3d0-9aea-11d5-bd16-0090272ccb30",
    "name": "ftp",
    "type": "service-tcp",
    "domain": {
        "uid": "a0bbbc99-adef-4ef8-bb6d-defdefdefdef",
        "name": "Cisco Security Domain",
        "domain-type": "data domain",
    },
    "port": "21",
    "icon": "Protocols/FTP",
    "color": "forest green",
}

print("\nLoop over the keys")
print("-" * 10)
for key in cisco_service.keys():
    print(key)

print("\nLoop over the values")
print("-" * 10)
for value in cisco_service.values():
    print(value)

print("\nLoop over the key-value")
print("-" * 10)
for k, v in cisco_service.items():
    print(f"{k} -> {v}")
```

**Three ways to loop over a dictionary:**
- `.keys()` — Only the keys
- `.values()` — Only the values
- `.items()` — Both key AND value as pairs

**What does `.items()` return?** A sequence of `(key, value)` tuples. The `for k, v in` unpacks each tuple into two variables.

### 6.8 Looping Over Nested Dictionaries

**Script:** `python_course_mar26/class1/loops/loop_ex7.py`

```python
#!/usr/bin/env python
from rich import print

cisco_service = {
    "uid": "97aeb3d0-9aea-11d5-bd16-0090272ccb30",
    "name": "ftp",
    "type": "service-tcp",
    "domain": {
        "uid": "a0bbbc99-adef-4ef8-bb6d-defdefdefdef",
        "name": "Cisco Security Domain",
        "domain-type": "data domain",
    },
    "port": "21",
    "icon": "Protocols/FTP",
    "color": "forest green",
}

for k, v in cisco_service.items():
    if k == "domain":
        print()
        for inner_k, inner_v in v.items():
            print(f"{inner_k} -> {inner_v}")
        print()
```

**What's happening here?** When we encounter the `"domain"` key, its value `v` is itself a dictionary. We loop over THAT inner dictionary with a nested `for` loop.

**Why is this important?** Because API responses and parsed device output are often deeply nested. You need to navigate multiple levels.

### 6.9 The `while` Loop

**Script:** `python_course_mar26/class1/loops/while_ex1.py`

```python
#!/usr/bin/env python
import time
from rich import print

WAIT_TIME = 6

print()
start_time = time.time()
while time.time() - start_time < WAIT_TIME:
    print(time.time() - start_time)
    time.sleep(1)
    print("In loop...")

print("\nLoop over")
```

**How does `while` work?** It checks the condition before each iteration. If `True`, run the body. If `False`, stop.

**What does `time.time()` return?** The current time in seconds since January 1, 1970 (a "Unix timestamp"). Subtracting `start_time` gives elapsed seconds.

**What does `time.sleep(1)` do?** Pauses execution for 1 second. Useful for rate-limiting device connections.

### 6.10 `while True` with `break`

**Script:** `python_course_mar26/class1/loops/while_ex2.py`

```python
#!/usr/bin/env python
import time
from rich import print

WAIT_TIME = 6

print()
start_time = time.time()
while True:
    print("In loop...")
    time.sleep(1)
    cur_time = time.time()
    if (cur_time - start_time) > WAIT_TIME:
        break

print("\nLoop over")
```

**What is `while True`?** An infinite loop — it runs forever UNLESS you use `break` to exit. The `break` is triggered when the elapsed time exceeds `WAIT_TIME`.

**When do you use this pattern?** For retry logic:

```python
while True:
    try:
        net_connect = ConnectHandler(**device)
        break    # Success — exit the loop
    except NetmikoTimeoutException:
        print("Retrying...")
        time.sleep(5)
```

### 6.11 Network Exercise — Iterating Through Firewalls

**Script:** `python_course_mar26/class1/exercises/loops_ex/loops_ex1.py`

```python
from rich import print

my_firewalls = [
    "cisco-fw-pod1",
    "cisco-fw-pod2",
    "cisco-fw-pod3",
    "cisco-fw-pod4",
    "cisco-fw-pod5",
]

for fw in my_firewalls:
    print(fw)

for fw in my_firewalls:
    if fw == "cisco-fw-pod5":
        print(f"\nConnecting to fw: {fw}\n")
```

### 6.12 Network Exercise — `continue` and `break` Together

**Script:** `python_course_mar26/class1/exercises/loops_ex/loops_ex2.py`

```python
from rich import print

my_firewalls = [
    "cisco-fw-pod1",
    "cisco-fw-pod2",
    "cisco-fw-pod3",
    "cisco-fw-pod4",
    "cisco-fw-pod5",
    "cisco-fw-pod98",
    "cisco-fw-pod99",
]

for fw in my_firewalls:
    if fw == "cisco-fw-pod4":
        continue          # Skip pod4 (under maintenance)
    if fw == "cisco-fw-pod98":
        break             # Stop processing at pod98
    print(fw)
```

**Output:**
```
cisco-fw-pod1
cisco-fw-pod2
cisco-fw-pod3
cisco-fw-pod5
```

Pod4 skipped by `continue`. Pod98 and pod99 never reached because `break` stopped the loop.

### 6.13 The LABATO-1010 Pattern — Looping Over Devices

From `labato_1010/3-netmiko-config.py`:

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

**This script combines FIVE concepts:** Dictionaries (Ch.4), Lists (Ch.4), For loops (Ch.6), Dictionary access `device['ip']` (Ch.4), and Dictionary unpacking `**device` (Ch.4).

---
---

## Chapter 7: Working with Files

*(Deeply explained Chapter 7 content from previous version — file reading, writing, with statement, JSON, YAML, CSV — all Cisco-only examples)*

### 7.1 Reading Files

**Script:** `python_course_mar26/class1/files/read_file.py`

```python
#!/usr/bin/env python
from rich import print

f = open("my_file.txt", "r")
data = f.read()
print(data)

f.seek(0)
data = f.readlines()
print(type(data))
print(data)

f.seek(0)
print("Looping over file")
for line in f:
    line = line.strip()
    print(repr(line))

f.close()
```

**Why `f.seek(0)`?** After `read()`, the cursor is at the end. `seek(0)` rewinds to the beginning so you can read again.

**Why `line.strip()`?** Each line from a file includes a trailing `\n`. `strip()` removes it.

**Why `repr(line)`?** Shows hidden characters like `\n` and spaces — essential for debugging.

### 7.2 The `with` Statement

**Script:** `python_course_mar26/class1/files/file_cm.py`

```python
#!/usr/bin/env python

with open("my_file.txt") as f:
    data = f.read()

print(data)
```

**Why is `with` better?** It automatically closes the file when the block ends — even if an error occurs.

### 7.3 Writing Files

**Script:** `python_course_mar26/class1/files/write_file_cm.py`

```python
#!/usr/bin/env python

with open("new_file.txt", "w") as f:
    f.write("--> hello world <--\n")
    f.write("something else\n")
    f.write("one last line\n")
```

**DANGER with `"w"` mode:** It erases ALL existing content! Use `"a"` (append) to add to the end without erasing.

### 7.4 JSON Files

**Script:** `python_course_mar26/class1/files/read_json.py`

```python
import json
from rich import print

with open("cisco_api.json") as f:
    data = json.load(f)

print(data)
```

**Script:** `python_course_mar26/class1/files/write_json.py`

```python
import json

data = {
    "current-version": "1.8",
    "supported-versions": ["1", "1.1", "1.2", "1.3", "1.4",
                           "1.5", "1.6", "1.7", "1.8"],
}

with open("cisco_api.json", "w") as f:
    json.dump(data, f, indent=4)
```

### 7.5 YAML Files

**Script:** `python_course_mar26/class1/files/read_yaml.py`

```python
import yaml
from rich import print

with open("cisco_api.yaml") as f:
    data = yaml.safe_load(f)

print(data)
```

**Script:** `python_course_mar26/class1/files/write_yaml.py`

```python
import yaml

data = {
    "current-version": "1.8",
    "supported-versions": ["1", "1.1", "1.2", "1.3", "1.4",
                           "1.5", "1.6", "1.7", "1.8"],
}

with open("cisco_api.yaml", "w") as f:
    yaml.dump(data, f, default_flow_style=False)
```

**Always use `yaml.safe_load()`** — never `yaml.load()` (security risk).

### 7.6 The File Exercise — Text vs. Structured Data

**Script:** `python_course_mar26/class1/exercises/file_ex/files_ex1.py`

```python
#!/usr/bin/env python
import json
from rich import print

filename = "network_objects.json"

with open(filename) as f:
    data = f.read()

print(f"\nRead in file({filename}) as a string")
print(f"Type 'data' var: {type(data)}")

with open(filename) as f:
    data = json.load(f)
print(f"\nRead in file({filename}) as a data structure (dictionary)")
print(f"Type 'data' var: {type(data)}")
print(f"Type data['objects'] field: {type(data['objects'])}")
```

**Key insight:** `f.read()` gives you a string. `json.load(f)` gives you a dictionary. The structured version is what you need for automation.

---
---

## Chapter 8: Comprehensions and Complex Data

### 8.1 List Comprehensions

**Script:** `python_course_mar26/class3/list_comprehenson/list_comp_ex.py`

```python
from rich import print

my_list = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

squares = [x**2 for x in my_list]
print(squares)

cubes = [x**3 for x in my_list]
print(cubes)

evens = [x for x in my_list if x % 2 == 0]
print(evens)

odds = [x for x in my_list if x % 2 == 1]
print(odds)

sentence = "This is a test sentence."
words = sentence.split()
print(words)

capital_words = [word.upper() for word in words]
print(capital_words)
```

**How to read:** `[x**2 for x in my_list]` — Start from the middle: "for each x in my_list," then the left: "compute x squared," then the brackets: "put results in a new list."

**Network examples:**

```python
vlans = [f'vlan {num}' for num in range(10, 16)]
# ['vlan 10', 'vlan 11', 'vlan 12', 'vlan 13', 'vlan 14', 'vlan 15']

interfaces = [
    {'name': 'Gi0/0', 'status': 'up'},
    {'name': 'Gi0/1', 'status': 'down'},
    {'name': 'Lo0', 'status': 'up'},
]
up_interfaces = [i['name'] for i in interfaces if i['status'] == 'up']
# ['Gi0/0', 'Lo0']
```

---
---

## Chapter 9: Functions

### 9.1 Basic Functions

**Script:** `python_course_mar26/class1/functions/func_ex1.py`

```python
def my_func(x, y):
    print(x)
    print(y)
    return x + y

ret_val = my_func(7, 2)
print(f"{ret_val=}")
```

### 9.2 Keyword Arguments

**Script:** `python_course_mar26/class1/functions/func_ex2.py`

```python
def my_func(x, y):
    print(f"{x=}")
    print(f"{y=}")
    return x + y

print()
ret_val = my_func(x=7, y=2)
print(f"{ret_val=}")

print()
ret_val = my_func(y=42, x=0)
print(f"{ret_val=}")
```

**Why does order not matter with keyword arguments?** Python matches by name, not position.

### 9.3 Default Arguments

**Script:** `python_course_mar26/class1/functions/func_ex3.py`

```python
def my_func(x, y, z=100):
    print(f"{x=}")
    print(f"{y=}")
    print(f"{z=}")
    return x + y + z

ret_val = my_func(x=7, y=2)
print(f"{ret_val=}")     # 109 (z defaults to 100)
```

### 9.4 List Unpacking with `*`

**Script:** `python_course_mar26/class1/functions/func_ex4.py`

```python
def my_func(x, y, z=100):
    print(f"{x=}")
    print(f"{y=}")
    print(f"{z=}")
    return x + y + z

my_list = [1, 7, 99]
ret_val = my_func(*my_list)
print(ret_val)
```

**What does `*my_list` do?** Unpacks the list into positional arguments. `my_func(*[1, 7, 99])` is the same as `my_func(1, 7, 99)`.

### 9.5 Dictionary Unpacking with `**`

**Script:** `python_course_mar26/class1/functions/func_ex5.py`

```python
def my_func(x, y, z=100):
    print(f"{x=}")
    print(f"{y=}")
    print(f"{z=}")
    return x + y + z

my_dict = {
    "x": 11,
    "y": 22,
    "z": 33,
}
ret_val = my_func(**my_dict)
print(ret_val)
```

**What does `**my_dict` do?** Unpacks the dictionary into keyword arguments. `my_func(**{"x": 11, "y": 22, "z": 33})` is the same as `my_func(x=11, y=22, z=33)`.

**This is EXACTLY how Netmiko works:**

```python
device = {'device_type': 'cisco_ios', 'ip': '10.0.0.1', 'username': 'admin', 'password': 'secret'}
net_connect = ConnectHandler(**device)
# Same as: ConnectHandler(device_type='cisco_ios', ip='10.0.0.1', username='admin', password='secret')
```

### 9.6 Function Exercises

**Script:** `python_course_mar26/class1/exercises/func_ex/func_ex1.py`

```python
#!/usr/bin/env python

def my_func():
    print("Hello world")

my_func()
my_func()
my_func()
```

**Script:** `python_course_mar26/class1/exercises/func_ex/func_ex2.py`

```python
#!/usr/bin/env python

def fw_func(fw_name):
    print(f"{fw_name=}")

fw_func("cisco-fw1")
fw_func(fw_name="cisco-asa-01")
```

---
---

## Chapter 10: Useful Modules

### 10.1 The `os` Module

**Script:** `python_course_mar26/class2/linux_python/os_system_ex.py`

```python
#!/usr/bin/env python
import os

cmd = "ping -c 4 google.com"
os.system(cmd)
```

**What does `os.system()` do?** Runs a shell command. The output goes directly to the terminal.

### 10.2 The `pathlib` Module

**Script:** `python_course_mar26/class2/linux_python/pathlib_ex.py`

```python
from pathlib import Path
from rich import print

home = Path.home()
netmiko_yml_file = home / ".netmiko.yml"
print(netmiko_yml_file)

netmiko_yml_data = netmiko_yml_file.read_text()
print(netmiko_yml_data)

sessions_file = (
    home / "python_course_mar26" / "class2" / "complex_dstruct" / "sessions.json"
)

sessions_file.exists()
sessions_file.is_file()
sessions_file.is_dir()

parent_dir = sessions_file.parent
print(parent_dir)

course_dir = home / "python_course_mar26"
print()
for f in course_dir.rglob("*.json"):
    print(f)
```

**What is `pathlib`?** A modern way to work with file paths. The `/` operator joins paths: `home / ".netmiko.yml"` creates a full path like `/home/user/.netmiko.yml`.

### 10.3 The `sys` Module — Python's System Path

**Script:** `python_course_mar26/class1/libraries/sys_path_ex.py`

```python
import sys
from rich import print

print("\nsys.path:")
print("-" * 30)
print(sys.path)
print()
```

**What is `sys.path`?** A list of directories where Python looks for modules when you do `import something`. If your module isn't in one of these directories, Python can't find it.
---

## Chapter 11: Exception Handling

### 11.1 What Are Exceptions and Why Must You Handle Them?

An exception is Python's way of saying "something went wrong." Without exception handling, any error crashes your entire script. For network automation, errors are INEVITABLE — devices may be unreachable, credentials may be wrong, commands may return unexpected output. Exception handling lets your script survive these failures and continue processing remaining devices.

### 11.2 try/except Basics

**Script:** `python_course_mar26/class1/try_except/try_except_ex1.py`

```python
cisco_service = {
    "uid": "97aeb3d1-9aea-11d5-bd16-0090272ccb30",
    "name": "ftp-port",
    "type": "service-tcp",
    "port": "21",
}

try:
    print("before KeyError")
    cisco_service["service_type"]     # Key doesn't exist!
    print("after KeyError")           # NEVER runs
except KeyError:
    print("Inside exception handler")
```

**How it works:** Python runs the `try` block. When the KeyError occurs, it jumps immediately to the `except` block. Lines after the error in `try` are SKIPPED.

### 11.3 try/except/finally

**Script:** `python_course_mar26/class1/try_except/try_except_ex2.py`

```python
try:
    cisco_service["service_type"]
except KeyError:
    print("Inside exception handler")
finally:
    print("Always happens")    # Runs no matter what
```

**Why `finally`?** For cleanup code that MUST run — like disconnecting from a device.

### 11.4 Multiple Exception Types

**Script:** `python_course_mar26/class1/try_except/try_except_ex4.py`

```python
cisco_service_keys = list(cisco_service.keys())

try:
    cisco_service_keys[100]          # IndexError!
except KeyError:
    print("KeyError exception handler")
except IndexError:
    print("IndexError exception handler")
finally:
    print("Always happens")
```

### 11.5 Catching Multiple Exceptions Together

**Script:** `python_course_mar26/class1/try_except/try_except_ex5.py`

```python
try:
    cisco_service_keys[100]
except (KeyError, IndexError):
    print("Handle both KeyError and IndexError")
finally:
    print("Always happens")
```

### 11.6 Capturing the Exception Message

**Script:** `python_course_mar26/class1/try_except/try_except_ex7.py`

```python
try:
    cisco_service_keys[100]
except IndexError as e:
    print(f"Exception message: {e}")
```

**What does `as e` do?** Stores the exception object in variable `e` so you can print its message.

### 11.7 Raising Exceptions

**Script:** `python_course_mar26/class1/try_except/try_except_ex8.py`

```python
msg = "Something went wrong"
raise ValueError(msg)
```

**What does `raise` do?** Manually triggers an exception. Use this when YOUR code detects an error condition.

### 11.8 Production Error Handling — LABATO-1010 Pattern

**Script:** `labato_1010/5-netmiko-final.py` (full script)

```python
#!/usr/bin/env python
from getpass import getpass
from netmiko import ConnectHandler
from netmiko import NetmikoAuthenticationException
from netmiko import NetmikoTimeoutException
from paramiko.ssh_exception import SSHException

username = input('Enter your SSH username: ')
password = getpass('Enter your password: ')

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

    output = net_connect.send_config_from_file('config_commands')
    output += net_connect.save_config()
    net_connect.disconnect()
    print(output)
```

**Why `continue` after each exception?** This code is inside a `for` loop. `continue` skips the failed device and moves to the next one. Without it, the script would crash at the first unreachable device.

### 11.9 Netmiko Course — Error Handling as a Reusable Function

**Script:** `netmiko_course/class7/collateral/handle_failures.py`

```python
import os
import yaml
from getpass import getpass
from netmiko import ConnectHandler
from netmiko import NetmikoAuthenticationException
from netmiko import NetmikoTimeoutException
from paramiko.ssh_exception import SSHException

def load_devices(device_file="lab_devices.yml"):
    device_dict = {}
    with open(device_file) as f:
        device_dict = yaml.safe_load(f)
    return device_dict

def netmiko_conn(device):
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

if __name__ == "__main__":
    password = (
        os.getenv("NETMIKO_PASSWORD") if os.getenv("NETMIKO_PASSWORD") else getpass()
    )
    my_devices = load_devices()

    for device_name, device in my_devices.items():
        device["password"] = password
        conn = netmiko_conn(device)
        if conn is None:
            continue
        print(conn.find_prompt())
```

**Why is the function version better?** You write error handling ONCE and reuse it in every script. The LABATO version repeats the same try/except in scripts 5, 6, and 7.

---
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
---

# Chapter 14: Connecting to Cisco Devices with Netmiko

## 14.1 Your First Netmiko Connection

In this script we will use Netmiko to connect to a Cisco IOS-XE router via SSH, collect the `show version` command output, and print it to the screen.

This is the most fundamental script in all of network automation. Every other script in this book builds on this foundation.

### Line-by-Line Breakdown

**`#!/usr/bin/env python`** — The shebang line. Tells Linux which interpreter to use when running the script directly. On Windows, this line is ignored.

**`from netmiko import ConnectHandler`** — Imports the `ConnectHandler` class from the Netmiko library. `ConnectHandler` is the main object that creates SSH connections to network devices. Without this import, Python doesn't know what `ConnectHandler` is.

**What if Netmiko isn't installed?** You'll get `ModuleNotFoundError: No module named 'netmiko'`. Fix it with `pip install netmiko` inside your virtual environment.

**`ios1 = { ... }`** — Creates a dictionary containing all the SSH connection parameters. This is the standard way to define device credentials in Netmiko:
- `'device_type': 'cisco_ios'` — Tells Netmiko this is a Cisco IOS device. Netmiko supports 100+ device types. The `device_type` determines how Netmiko handles the command prompt, config mode, and save commands.
- `'ip': '198.18.1.11'` — The management IP address of the device.
- `'username': 'cisco'` — SSH username.
- `'password': 'cisco'` — SSH password.

**What if I use the wrong `device_type`?** Netmiko will connect via SSH but may hang waiting for a prompt it doesn't recognize, or send incorrect commands. Always verify the correct device_type for your platform.

**`net_connect = ConnectHandler(**ios1)`** — This is where the magic happens. The `**ios1` unpacks the dictionary into keyword arguments (Chapter 9). Then `ConnectHandler` performs these steps:
1. Resolves the IP address
2. Opens a TCP connection to port 22 (SSH)
3. Performs SSH key exchange and authentication
4. Logs in with the provided username/password
5. Detects the device prompt (e.g., `csr1#`)
6. Returns a connection object stored in `net_connect`

**How long does this take?** Typically 2-10 seconds depending on network latency.

**What if the device is unreachable?** After the timeout (default ~10 seconds), Netmiko raises `NetmikoTimeoutException`. We'll learn to handle this in Chapter 11.

**`output = net_connect.send_command('show version')`** — Sends the `show version` command to the device. Here's what happens internally:
1. Sends the string `"show version"` to the device via SSH
2. Presses Enter (sends `\n`)
3. Waits for the device to respond
4. Collects ALL output until the device prompt reappears
5. Returns the output as a Python string (without the command echo or prompt)

**What about `--More--` paging?** Netmiko handles it automatically by sending `terminal length 0` during connection setup.

**`net_connect.disconnect()`** — Closes the SSH session. Always disconnect when done! Network devices have limited SSH session slots (typically 5-16). If you don't disconnect, you'll eventually exhaust them and lock yourself out.

**`print(output)`** — Displays the raw `show version` output to the terminal.

### Full Script — Copy, Paste, and Run

**Source:** `labato_1010/1-netmiko-show.py`

```python
#!/usr/bin/env python
from netmiko import ConnectHandler

# SSH Connection Details
ios1 = {
    'device_type': 'cisco_ios',
    'ip': '198.18.1.11',
    'username': 'cisco',
    'password': 'cisco',
}

# Establish SSH to device and run show command
net_connect = ConnectHandler(**ios1)
output = net_connect.send_command('show version')
net_connect.disconnect()
print(output)
```

---

## 14.2 Connecting Using a Dictionary (Best Practice)

In this script we separate the device parameters into a dictionary variable and use dictionary unpacking (`**`) to pass them to `ConnectHandler`. This is the pattern used in every professional Netmiko script.

### Line-by-Line Breakdown

**`password = os.getenv("NETMIKO_PASSWORD") if os.getenv("NETMIKO_PASSWORD") else getpass()`** — This is a conditional expression (Chapter 5). It checks if the environment variable `NETMIKO_PASSWORD` is set. If yes, use it. If not, prompt the user securely with `getpass()`. This allows the script to work both interactively (you type the password) and non-interactively (CI/CD pipelines, cron jobs).

**`my_device = { ... }`** — Same dictionary pattern as Script 1, but using `host` instead of `ip`. Both work — Netmiko accepts either.

**`net_connect = ConnectHandler(**my_device)`** — Unpacks the dictionary. Identical to writing `ConnectHandler(device_type="cisco_ios", host="cisco3.lasthop.io", ...)`.

**`print(net_connect.find_prompt())`** — `find_prompt()` returns the current device prompt as a string, like `"csr1#"`. This is useful for extracting the hostname: `hostname = net_connect.find_prompt()[:-1]` strips the trailing `#`.

### Full Script — Copy, Paste, and Run

**Source:** `netmiko_course/class1/collateral/simple_conn_dict.py`

```python
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

---

## 14.3 Connecting with a Context Manager (Cleanest Approach)

In this script we use Python's `with` statement to automatically handle the SSH connection lifecycle. The connection is automatically closed when the `with` block ends — even if an error occurs inside it.

### Line-by-Line Breakdown

**`with ConnectHandler(**my_device) as net_connect:`** — The `with` statement creates a context manager. When the indented block ends (or if an exception occurs), `net_connect.disconnect()` is called automatically. This is the safest way to handle connections.

**Why is this better?** You can never forget to disconnect. Even if your script crashes mid-execution, the SSH session is properly closed.

### Full Script — Copy, Paste, and Run

**Source:** `netmiko_course/class1/collateral/simple_conn_cm.py`

```python
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

with ConnectHandler(**my_device) as net_connect:
    print(net_connect.find_prompt())

print("Connection automatically closed")
```

---

## 14.4 Session Logging — Recording Everything

In this script we enable session logging, which records every byte sent and received over the SSH session to a file. This is invaluable for debugging — when a command doesn't work as expected, the session log shows exactly what happened.

### Line-by-Line Breakdown

**`session_log="cisco3.out"`** — Added to the device dictionary. Netmiko will write all SSH session data (prompts, commands, output) to a file named `cisco3.out` in the current directory.

**When do you use this?** When debugging connection issues, unexpected command output, or timing problems. The session log shows you exactly what Netmiko sent and what the device returned, including hidden characters.

### Full Script — Copy, Paste, and Run

**Source:** `netmiko_course/class1/collateral/simple_conn_slog.py`

```python
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
    session_log="cisco3.out",
)
print(net_connect.find_prompt())
output = net_connect.send_command("show ip int brief")
print(output)
net_connect.disconnect()
```

---

## 14.5 Connecting to Multiple Devices

In this script we connect to three different device types (Cisco IOS, NX-OS, and Arista EOS) using a `for` loop. This demonstrates that the same Netmiko pattern works across vendors — you only change the `device_type`.

### Line-by-Line Breakdown

**Three device dictionaries** — `cisco3`, `nxos1`, `arista1` — each with a different `device_type` and `host`. The structure is identical; only the parameters change.

**`for device in (cisco3, nxos1, arista1):`** — Iterates through a tuple of device dictionaries. On each iteration, `device` is one of the three dictionaries.

**Why a tuple `()` instead of a list `[]`?** Either works. Tuples are slightly more efficient for fixed collections that won't be modified.

### Full Script — Copy, Paste, and Run

**Source:** `netmiko_course/class2/collateral/conn_mult_devices.py`

```python
import os
from netmiko import ConnectHandler
from getpass import getpass

password = os.getenv("NETMIKO_PASSWORD") if os.getenv("NETMIKO_PASSWORD") else getpass()

cisco3 = {
    "device_type": "cisco_ios",
    "host": "cisco3.lasthop.io",
    "username": "pyclass",
    "password": password,
}

nxos1 = {
    "device_type": "cisco_nxos",
    "host": "nxos1.lasthop.io",
    "username": "pyclass",
    "password": password,
}

arista1 = {
    "device_type": "arista_eos",
    "host": "arista1.lasthop.io",
    "username": "pyclass",
    "password": password,
}

for device in (cisco3, nxos1, arista1):
    net_connect = ConnectHandler(**device)
    print(net_connect.find_prompt())
    net_connect.disconnect()
```

---

## 14.6 Debug Logging

In this script we enable Python's `logging` module to see detailed Netmiko debug information. This goes deeper than session logging — it shows internal Netmiko operations like pattern matching and timing.

### Full Script — Copy, Paste, and Run

**Source:** `netmiko_course/class2/collateral/netmiko_log.py`

```python
import os
from netmiko import ConnectHandler
from getpass import getpass

import logging

logging.basicConfig(filename="test.log", level=logging.DEBUG)
logger = logging.getLogger("netmiko")

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

**After running, check `test.log`** — it contains detailed debug information about every step of the SSH connection.

---

## 14.7 Auto-Detecting Device Type

In this script we use Netmiko's `SSHDetect` class to automatically determine what type of device we're connecting to. This is useful when you have a mixed-vendor network and don't know the device type in advance.

### Line-by-Line Breakdown

**`"device_type": "autodetect"`** — Instead of specifying `cisco_ios` or `arista_eos`, we tell Netmiko to figure it out.

**`guesser = SSHDetect(**device)`** — Creates an SSH connection and analyzes the device's behavior to determine its type.

**`best_match = guesser.autodetect()`** — Returns the best-guess device type as a string (e.g., `"cisco_ios"`, `"arista_eos"`).

### Full Script — Copy, Paste, and Run

**Source:** `netmiko_course/class10/collateral/detect_platform.py`

```python
import os
from getpass import getpass
from netmiko import SSHDetect, ConnectHandler

password = os.getenv("NETMIKO_PASSWORD") if os.getenv("NETMIKO_PASSWORD") else getpass()

base_device = {"device_type": "autodetect", "username": "pyclass", "password": password}

hosts = [
    "cisco3.lasthop.io",
    "nxos1.lasthop.io",
    "arista1.lasthop.io",
]

for hostname in hosts:
    device = base_device.copy()
    device["host"] = hostname
    guesser = SSHDetect(**device)
    best_match = guesser.autodetect()
    print(best_match)

# Connect to the very last device
device["device_type"] = best_match
with ConnectHandler(**device) as connection:
    print()
    print("Full SSH Connection:")
    print(connection.find_prompt())
```

---

## 14.8 SSH Key Authentication

In this script we connect using SSH keys instead of passwords. This is more secure and is required in many enterprise environments.

### Full Script — Copy, Paste, and Run

**Source:** `netmiko_course/class6/collateral/ssh_keys.py`

```python
from netmiko import ConnectHandler

cisco3 = {
    "device_type": "cisco_ios",
    "host": "cisco3.lasthop.io",
    "username": "student1",
    "use_keys": True,
    "key_file": "~/.ssh/student_key",
    "disable_sha2_fix": True,
}

with ConnectHandler(**cisco3) as net_connect:
    output = net_connect.send_command("show ip arp")

print(f"\n{output}\n")
```

**What does `use_keys=True` do?** Tells Netmiko to use SSH key-based authentication instead of a password. `key_file` points to your private key file.

---

## 14.9 Password Retry Function

In this script we create a function that tries multiple passwords when connecting to a device. This is useful when migrating credentials across a network — some devices may have the old password, others the new one.

### Line-by-Line Breakdown

**`def try_passwords(device, passwords=None):`** — A function that takes a device dictionary and a list of passwords to try.

**`for passwd in passwords:`** — Iterates through each password in the list.

**`except NetmikoAuthenticationException: continue`** — If the current password fails, skip to the next one.

**`else: raise NetmikoAuthenticationException(...)`** — The `for/else` pattern: the `else` block runs only if the loop completed WITHOUT hitting `break`. This means no password worked.

### Full Script — Copy, Paste, and Run

**Source:** `netmiko_course/class7/collateral/auth_retry_func.py`

```python
import os
from getpass import getpass
from netmiko import ConnectHandler
from netmiko import NetmikoAuthenticationException


def try_passwords(device, passwords=None):
    """
    Retry using all of the passwords provided.
    passwords is an iterator of passwords to try.
    """
    if passwords is None:
        passwords = []
    for passwd in passwords:
        device["password"] = passwd
        try:
            net_connect = ConnectHandler(**device)
            break
        except NetmikoAuthenticationException:
            continue
    else:
        # nobreak — no valid password found
        raise NetmikoAuthenticationException("No valid password found.")
    return net_connect


if __name__ == "__main__":
    password = (
        os.getenv("NETMIKO_PASSWORD") if os.getenv("NETMIKO_PASSWORD") else getpass()
    )

    cisco3 = {
        "device_type": "cisco_ios",
        "host": "cisco3.lasthop.io",
        "username": "pyclass",
    }

    real_password = password
    password_list = ["invalid1", "invalid2", real_password]

    net_connect = try_passwords(cisco3, password_list)
    output = net_connect.send_command("show ip arp")

    print(f"\n{output}\n")
```

---

# Chapter 15: Show Commands and Output Parsing

## 15.1 Sending a Show Command

In this script we connect to a Cisco IOS-XE router and execute `show ip int brief`. The output is returned as a plain text string — exactly what you'd see on the CLI.

### Line-by-Line Breakdown

**`output = net_connect.send_command("show ip int brief")`** — Sends the command, waits for the prompt, and returns the output. Netmiko strips the command echo and prompt from the output automatically.

**What if the command doesn't exist on the device?** Netmiko returns whatever the device returns — including error messages like `% Invalid input detected`. It does NOT raise an exception for invalid commands.

### Full Script — Copy, Paste, and Run

**Source:** `netmiko_course/class2/collateral/show_command.py`

```python
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

output = net_connect.send_command("show ip int brief")
print(output)
net_connect.disconnect()
```

---

## 15.2 Parsing Output with TextFSM

In this script we use `use_textfsm=True` to automatically parse the raw text output into structured data (a list of dictionaries). Instead of getting a wall of text, you get data you can work with programmatically.

### Line-by-Line Breakdown

**`output = net_connect.send_command("show ip int brief", use_textfsm=True)`** — The `use_textfsm=True` flag tells Netmiko to use NTC TextFSM templates to parse the output.

**What does the output look like?** Instead of a raw string, you get a list of dictionaries:

```python
[{'intf': 'GigabitEthernet0/0', 'ipaddr': '10.0.12.1', 'status': 'up', 'proto': 'up'},
 {'intf': 'GigabitEthernet0/1', 'ipaddr': '10.0.13.1', 'status': 'up', 'proto': 'up'}]
```

**Why is this better?** Because you can access fields by name: `output[0]['ipaddr']` instead of parsing columns with string splitting.

**What if TextFSM doesn't have a template for your command?** It returns the raw text string as a fallback. Your code should handle both cases:

```python
if isinstance(output, list):
    # Parsed successfully
    for entry in output:
        print(entry['intf'], entry['ipaddr'])
else:
    # Fallback — raw text
    print(output)
```

### Full Script — Copy, Paste, and Run

**Source:** `netmiko_course/class3/collateral/show_textfsm.py`

```python
import os
from netmiko import ConnectHandler
from getpass import getpass
from pprint import pprint

password = os.getenv("NETMIKO_PASSWORD") if os.getenv("NETMIKO_PASSWORD") else getpass()

my_device = {
    "device_type": "cisco_ios",
    "host": "cisco3.lasthop.io",
    "username": "pyclass",
    "password": password,
}

net_connect = ConnectHandler(**my_device)

output = net_connect.send_command("show ip int brief", use_textfsm=True)
pprint(output)
net_connect.disconnect()
```

---

## 15.3 Parsing Output with Genie

In this script we use `use_genie=True` to parse output using Cisco's Genie library. Genie produces deeply nested dictionaries with rich device data.

### Line-by-Line Breakdown

**`output = net_connect.send_command('show version', use_genie=True)`** — Genie parses the output into a structured dictionary. For `show version`, this includes hostname, chassis model, serial number, IOS version, uptime, and much more.

**How do you navigate the output?** Chain dictionary key access:

```python
hostname = output["version"]["hostname"]     # "csr1"
chassis = output["version"]["chassis"]       # "CSR1000V"
serial = output["version"]["chassis_sn"]     # "9FMKNB70YR1"
```

**What's the difference between TextFSM and Genie?**
- **TextFSM** returns a list of dictionaries (one per row in tabular output). Better for `show ip int brief`, `show ip route`.
- **Genie** returns a deeply nested dictionary. Better for `show version`, `show interfaces`, `show ip ospf neighbor`.

### Full Script — Copy, Paste, and Run

**Source:** `labato_1010/9-netmiko-report.py`

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

# Raw dict output
print(output)

# Pretty-printed output
print()
pprint(output)
print()
```

---

## 15.4 Using `send_command_timing`

In this script we use `send_command_timing()` which uses a time-based approach instead of pattern matching. This is useful when the device prompt is unpredictable.

### Line-by-Line Breakdown

**`send_command_timing("show ip int brief")`** — Instead of waiting for a specific prompt pattern, it sends the command, waits a fixed amount of time, then returns whatever output has arrived.

**When do you use this instead of `send_command()`?** When the device doesn't return to a standard prompt, or when dealing with commands that produce interactive prompts.

### Full Script — Copy, Paste, and Run

**Source:** `netmiko_course/class3/collateral/show_timing.py`

```python
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

output = net_connect.send_command_timing("show ip int brief")
print(output)
net_connect.disconnect()
```

---

## 15.5 Handling Long-Running Commands with `read_timeout`

In this script we handle a long-running command (`traceroute`) by increasing the read timeout. By default, Netmiko waits ~100 seconds for output. Some commands need more time.

### Full Script — Copy, Paste, and Run

**Source:** `netmiko_course/class2/collateral/read_timeout/traceroute_working.py`

```python
import os
from getpass import getpass
from datetime import datetime
from netmiko import ConnectHandler

password = os.getenv("NETMIKO_PASSWORD") if os.getenv("NETMIKO_PASSWORD") else getpass()

device = {
    "host": "cisco3.lasthop.io",
    "username": "pyclass",
    "password": password,
    "device_type": "cisco_xe",
}

command = "traceroute 10.220.88.28"

with ConnectHandler(**device) as ssh_conn:
    start_time = datetime.now()
    output = ssh_conn.send_command(command, read_timeout=20)
    end_time = datetime.now()
    print()
    print("-" * 50)
    print(output)
    print(f"\n\nExecution time: {end_time - start_time}\n\n")
    print("-" * 50)
    print()
```

---

## 15.6 Custom Expect Strings

In this script we use `expect_string` to tell Netmiko what pattern to wait for instead of the default device prompt. This is essential for commands that change the prompt or produce interactive output.

### Full Script — Copy, Paste, and Run

**Source:** `netmiko_course/class2/collateral/expect_str.py`

```python
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

output = net_connect.send_command("show ip int brief", expect_string=r"#")
print(output)
net_connect.disconnect()
```

**What does `expect_string=r"#"` do?** Instead of Netmiko auto-detecting the prompt, it waits specifically for a `#` character. The `r` prefix makes it a raw string (for regex patterns).

---

## 15.7 Handling Interactive Prompts

In this script we handle a command that asks for confirmation (`del flash:/filename`). We use multiple `send_command()` calls with different `expect_string` values to respond to each prompt.

### Full Script — Copy, Paste, and Run

**Source:** `netmiko_course/class4/collateral/send_command_prompting.py`

```python
import os
from netmiko import ConnectHandler
from getpass import getpass

password = os.getenv("NETMIKO_PASSWORD") if os.getenv("NETMIKO_PASSWORD") else getpass()

my_device = {
    "device_type": "cisco_ios",
    "host": "cisco3.lasthop.io",
    "username": "pyclass",
    "password": password,
    "session_log": "cisco3.out",
}

with ConnectHandler(**my_device) as net_connect:

    filename = "file_ex_3.txt"
    cmd = f"del flash:/{filename}"

    output = net_connect.send_command(
        cmd, expect_string=r"Delete filename", strip_prompt=False, strip_command=False
    )
    output += net_connect.send_command(
        "\n", expect_string=r"confirm", strip_prompt=False, strip_command=False
    )
    output += net_connect.send_command(
        "y", expect_string=r"#", strip_prompt=False, strip_command=False
    )
    print(output)
```

---

# Chapter 16: Sending Configuration Commands

## 16.1 Sending a Single Config Command

In this script we push a single configuration command (`logging host 10.1.1.1`) to a Cisco router. Netmiko automatically enters config mode, sends the command, and exits config mode.

### Line-by-Line Breakdown

**`output = net_connect.send_config_set('logging host 10.1.1.1')`** — The key difference from `send_command()`:
- `send_command()` → for **show** commands (privileged exec mode)
- `send_config_set()` → for **config** commands (global config mode)

Netmiko automatically runs `configure terminal`, sends your command, then runs `end` to exit config mode.

### Full Script — Copy, Paste, and Run

**Source:** `labato_1010/2-netmiko-config.py`

```python
#!/usr/bin/env python
from netmiko import ConnectHandler

ios1 = {
    'device_type': 'cisco_ios',
    'ip': '198.18.1.11',
    'username': 'cisco',
    'password': 'cisco',
}

net_connect = ConnectHandler(**ios1)
output = net_connect.send_config_set('logging host 10.1.1.1')
net_connect.disconnect()
print(output)
```

---

## 16.2 Sending Config to Multiple Devices from a File

In this script we read device IPs from a file, read config commands from another file, and push them to all devices. This is the jump from "lab toy" to "something you'd actually use."

### Full Script — Copy, Paste, and Run

**Source:** `labato_1010/4-netmiko-config.py`

```python
#!/usr/bin/env python
from netmiko import ConnectHandler
from getpass import getpass

username = input('Enter your SSH username: ')
password = getpass('Enter your password: ')

with open('device_list') as f:
    device_list = f.read().splitlines()

for device in device_list:
    print('Connecting to device ' + device)
    ios_device = {
        'device_type': 'cisco_ios',
        'ip': device,
        'username': username,
        'password': password
    }

    net_connect = ConnectHandler(**ios_device)
    output = net_connect.send_config_from_file('config_commands')
    net_connect.disconnect()
    print(output)
```

---

## 16.3 VLAN Configuration with YAML Device Inventory

In this script from the Netmiko course, we load device information from a YAML file, configure VLANs, and save the configuration on each device.

### Full Script — Copy, Paste, and Run

**Source:** `netmiko_course/class5/collateral/config_vlans.py`

```python
import os
from getpass import getpass
import yaml
from netmiko import ConnectHandler
import time


def load_devices(device_file="lab_devices.yml"):
    device_dict = {}
    with open(device_file) as f:
        device_dict = yaml.safe_load(f)
    return device_dict


if __name__ == "__main__":
    password = (
        os.getenv("NETMIKO_PASSWORD") if os.getenv("NETMIKO_PASSWORD") else getpass()
    )

    device_dict = load_devices()

    arista1 = device_dict["arista1"]
    arista2 = device_dict["arista2"]
    arista3 = device_dict["arista3"]
    arista4 = device_dict["arista4"]

    cfg_changes = ["vlan 500", "name gold500"]

    for device in (arista1, arista2, arista3, arista4):
        device["password"] = password
        net_connect = ConnectHandler(**device)
        output = net_connect.send_config_set(cfg_changes)
        output += net_connect.save_config()
        print(f"\n{output}\n\n")
        net_connect.disconnect()
        time.sleep(2)
```

---

## 16.4 Production-Ready Config with Full Error Handling

In this script we add comprehensive error handling and config saving. This is the production version from LABATO-1010.

### Full Script — Copy, Paste, and Run

**Source:** `labato_1010/6-netmiko-final.py`

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

    output = net_connect.send_config_from_file('config_commands')
    output += net_connect.save_config()
    net_connect.disconnect()
    print(output)
```

---

## 16.5 SCP File Transfer

In this script we use Netmiko's `file_transfer` function to copy files to/from a Cisco device using SCP.

### Full Script — Copy, Paste, and Run

**Source:** `netmiko_course/class9/collateral/put_file.py`

```python
import os
from getpass import getpass
from netmiko import ConnectHandler, file_transfer

password = os.getenv("NETMIKO_PASSWORD") if os.getenv("NETMIKO_PASSWORD") else getpass()

cisco3 = {
    "device_type": "cisco_ios",
    "host": "cisco3.lasthop.io",
    "username": "pyclass",
    "password": password,
}

source_file = "test2.txt"
dest_file = "test2.txt"
direction = "put"
file_system = "flash:"

ssh_conn = ConnectHandler(**cisco3)
transfer_dict = file_transfer(
    ssh_conn,
    source_file=source_file,
    dest_file=dest_file,
    file_system=file_system,
    direction=direction,
    overwrite_file=True,
    inline_transfer=True,
)
ssh_conn.disconnect()
print(transfer_dict)
```

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

**Twin Bridges Course** (`class3/cisco_asa_class/cisco_asa_class.py`):

```python
class CiscoAuthError(Exception):
    """Exception raised when the session ID is missing or expired."""
    pass
```

**What does this do?** It creates a custom exception type. `class` defines a new type. `(Exception)` means it inherits from Python's built-in `Exception` class.

**Why create custom exceptions?** So you can catch specific errors. `except CiscoAuthError` is more meaningful than a generic `except Exception`.

**What does `pass` do?** It's a placeholder that means "this block is intentionally empty." The class inherits everything it needs from `Exception`, so no additional code is required.

```python
class CiscoAPI:
    def __init__(self, host, username, password, api_version="1.8",
                 ssl_verify=False):
        self.host = host
        self.username = username
        self.password = password
        self.base_url = f"https://{host}/cisco_api/v{api_version}/"
        self.headers = {"Content-Type": "application/json"}
        self.ssl_verify = ssl_verify
```

**What is `class CiscoAPI:`?** It defines a new class named `CiscoAPI`. By convention, class names use `PascalCase` (each word capitalized, no underscores).

**What is `__init__`?** The "initializer" method (sometimes called the constructor). It runs automatically when you create a new object: `api_client = CiscoAPI(...)`. Its job is to set up the initial state of the object.

**What is `self`?** A reference to the specific object being created. Every method in a class must have `self` as its first parameter. When you call `api_client.login()`, Python passes `api_client` as `self` automatically.

**What does `self.host = host` do?** It stores the `host` parameter as an **instance attribute** — data that belongs to this specific object. Different objects can have different values:

```python
fw1 = CiscoAPI(host="fw1.example.com", username="admin", password="secret1")
fw2 = CiscoAPI(host="fw2.example.com", username="admin", password="secret2")
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
        self.headers["X-cisco-sid"] = resp_struct["sid"]
```

**What does `self.headers["X-cisco-sid"] = resp_struct["sid"]` do?** After a successful login, the API returns a session ID (`sid`). This line stores it in the headers dictionary so that subsequent API calls are authenticated.

**Why is this powerful?** Because the session state is managed internally. The caller doesn't need to track session IDs — they just call `login()` once and then use `call()` for every request.

```python
    def call(self, endpoint, payload=None):
        url = self.base_url + endpoint
        if payload is None:
            payload = {}
        if "X-cisco-sid" not in self.headers:
            raise CiscoAuthError(
                "Session ID not set, please call '.login()' method"
            )
        response = requests.post(
            url, data=json.dumps(payload),
            headers=self.headers, verify=self.ssl_verify
        )
        return response
```

**Why check for `"X-cisco-sid"` in headers?** To prevent making API calls without being authenticated. If someone forgets to call `login()` first, this raises a clear error instead of getting a confusing 401 response from the API.

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
    api_client = CiscoAPI(host="cisco-fw-pod99.lasthop.io",
                         username="admin", password=admin_pass)
    api_client.login()

    res = api_client.call(endpoint="show-version")
    print(res.json())

    api_client.logout()
```

**What is `api_client`?** An **instance** (object) of the `CiscoAPI` class. It has its own `host`, `username`, `password`, `headers`, etc.

**What does `api_client.login()` do?** Calls the `login` method on this specific object. Python translates this to `CiscoAPI.login(api_client)` — the object is passed as `self`.

**What does `api_client.call(endpoint="show-version")` do?** Calls the `call` method, which builds the URL, adds authentication headers, makes the HTTP request, and returns the response.

**Why is this better than functions?** Because all the state (session ID, base URL, headers) is bundled with the object. With functions, you'd have to pass these as parameters to every function call.

---
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
---

## Chapter 20: Capstone Project — From First Connection to Full Automation

### 20.1 Project Overview

The LABATO-1010 project is a sequence of 10 Python scripts that progressively build a complete network automation toolkit. Each script adds ONE new concept to the previous one, creating a clear learning path.

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



- YAML-based inventory management
- Built-in threading (no manual ThreadPoolExecutor)
- Result collection and error handling per device
- Plugin architecture for extensibility


---
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

---

*End of Book*

---
---

# Production Script: config_validator

```python
#!/usr/bin/env python
"""
Production Pre/Post Configuration Validator
=============================================
Captures device state before and after changes,
compares them, and generates a validation report.
"""
import os
import json
from datetime import datetime
from getpass import getpass
from netmiko import ConnectHandler

DEVICE_TYPE = "cisco_ios"
VALIDATION_DIR = "validation_snapshots"

# Commands to capture for validation
VALIDATION_COMMANDS = [
    "show ip interface brief",
    "show ip route summary",
    "show ip ospf neighbor",
    "show ip bgp summary",
    "show running-config | include hostname",
    "show version | include uptime",
    "show interfaces description",
    "show ip access-lists",
    "show ntp status",
    "show logging | include Syslog",
]


def get_credentials():
    username = os.getenv("NETMIKO_USERNAME") or input("Enter SSH username: ")
    password = os.getenv("NETMIKO_PASSWORD") or getpass("Enter SSH password: ")
    return username, password


def connect(ip, username, password):
    return ConnectHandler(
        device_type=DEVICE_TYPE, ip=ip,
        username=username, password=password, timeout=15
    )


def capture_state(conn, commands):
    """Capture output of all validation commands."""
    state = {}
    for cmd in commands:
        try:
            output = conn.send_command(cmd, read_timeout=30)
            state[cmd] = output.strip()
        except Exception as e:
            state[cmd] = f"ERROR: {e}"
    return state


def save_snapshot(hostname, state, phase, directory):
    """Save a state snapshot to JSON file."""
    os.makedirs(directory, exist_ok=True)
    timestamp = datetime.now().strftime("%Y%m%d_%H%M%S")
    filename = f"{hostname}_{phase}_{timestamp}.json"
    filepath = os.path.join(directory, filename)
    with open(filepath, "w") as f:
        json.dump(state, f, indent=4)
    return filepath


def compare_states(pre_state, post_state):
    """Compare pre and post states, return differences."""
    differences = {}
    for cmd in pre_state:
        pre = pre_state.get(cmd, "")
        post = post_state.get(cmd, "")
        if pre != post:
            differences[cmd] = {
                "pre": pre[:200] + "..." if len(pre) > 200 else pre,
                "post": post[:200] + "..." if len(post) > 200 else post,
            }
    return differences


def main():
    print(f"\n{'='*60}")
    print(f"  CONFIGURATION VALIDATOR")
    print(f"{'='*60}\n")

    username, password = get_credentials()
    target_ip = input("  Enter device IP: ")
    phase = input("  Phase (pre/post): ").lower()

    conn = connect(target_ip, username, password)
    hostname = conn.find_prompt()[:-1]
    print(f"  Hostname: {hostname}")
    print(f"  Capturing {phase}-change state...")

    state = capture_state(conn, VALIDATION_COMMANDS)
    conn.disconnect()

    filepath = save_snapshot(hostname, state, phase, VALIDATION_DIR)
    print(f"  Snapshot saved: {filepath}")

    # If post-change, find and compare with pre-change
    if phase == "post":
        pre_files = [f for f in os.listdir(VALIDATION_DIR)
                     if f.startswith(f"{hostname}_pre_")]
        if pre_files:
            latest_pre = sorted(pre_files)[-1]
            with open(os.path.join(VALIDATION_DIR, latest_pre)) as f:
                pre_state = json.load(f)

            diffs = compare_states(pre_state, state)

            if diffs:
                print(f"\n  ⚠ DIFFERENCES DETECTED ({len(diffs)} commands):")
                for cmd, diff in diffs.items():
                    print(f"\n  Command: {cmd}")
                    print(f"    PRE:  {diff['pre'][:80]}")
                    print(f"    POST: {diff['post'][:80]}")
            else:
                print(f"\n  ✓ NO DIFFERENCES — all {len(VALIDATION_COMMANDS)} checks match")
        else:
            print(f"\n  No pre-change snapshot found for {hostname}")

    print(f"\n{'='*60}\n")


if __name__ == "__main__":
    main()
```

---

# Production Script: device_monitor

```python
#!/usr/bin/env python
"""
Production Device Monitoring Script
====================================
Checks interface status, OSPF neighbors, BGP peers,
CPU/memory utilization, and network reachability.
"""
import os
import json
from datetime import datetime
from getpass import getpass
from netmiko import ConnectHandler
from netmiko import NetmikoTimeoutException, NetmikoAuthenticationException

DEVICE_TYPE = "cisco_ios"
REPORT_DIR = "monitoring_reports"


def get_credentials():
    username = os.getenv("NETMIKO_USERNAME") or input("Enter SSH username: ")
    password = os.getenv("NETMIKO_PASSWORD") or getpass("Enter SSH password: ")
    return username, password


def load_devices(filename="device_list"):
    with open(filename) as f:
        return [line.strip() for line in f.read().splitlines() if line.strip()]


def connect(ip, username, password):
    device = {
        "device_type": DEVICE_TYPE,
        "ip": ip,
        "username": username,
        "password": password,
        "timeout": 15,
    }
    try:
        return ConnectHandler(**device)
    except (NetmikoTimeoutException, NetmikoAuthenticationException) as e:
        print(f"  [ERROR] {ip}: {e}")
        return None


def check_interface_status(conn):
    """Check interface status using TextFSM parsing."""
    output = conn.send_command("show ip interface brief", use_textfsm=True)
    if isinstance(output, list):
        down_intfs = [i for i in output if i.get("status", "") != "up"]
        return {"total": len(output), "down": down_intfs}
    return {"total": 0, "down": [], "raw": output}


def check_ospf_neighbors(conn):
    """Check OSPF neighbor status."""
    output = conn.send_command("show ip ospf neighbor", use_textfsm=True)
    if isinstance(output, list):
        non_full = [n for n in output if "FULL" not in n.get("state", "")]
        return {"total": len(output), "non_full": non_full}
    return {"raw": output}


def check_bgp_summary(conn):
    """Check BGP peer status."""
    output = conn.send_command("show ip bgp summary", use_textfsm=True)
    if isinstance(output, list):
        down_peers = [p for p in output if not p.get("state_pfxrcd", "").isdigit()]
        return {"total": len(output), "down_peers": down_peers}
    return {"raw": output}


def check_cpu_memory(conn):
    """Check CPU and memory utilization."""
    cpu_output = conn.send_command("show processes cpu | include CPU")
    mem_output = conn.send_command("show memory statistics | include Processor")
    return {"cpu": cpu_output.strip(), "memory": mem_output.strip()}


def check_reachability(conn, targets=None):
    """Ping test to critical destinations."""
    if targets is None:
        targets = ["8.8.8.8", "1.1.1.1"]
    results = {}
    for target in targets:
        output = conn.send_command(f"ping {target} repeat 2", read_timeout=15)
        success = "!!" in output or "Success rate is 100" in output
        results[target] = "reachable" if success else "unreachable"
    return results


def main():
    start = datetime.now()
    print(f"\n{'='*60}")
    print(f"  DEVICE HEALTH CHECK — {start.strftime('%Y-%m-%d %H:%M:%S')}")
    print(f"{'='*60}\n")

    username, password = get_credentials()
    devices = load_devices()
    os.makedirs(REPORT_DIR, exist_ok=True)

    all_results = {}

    for ip in devices:
        print(f"\n  Checking {ip}...")
        conn = connect(ip, username, password)
        if not conn:
            all_results[ip] = {"status": "unreachable"}
            continue

        hostname = conn.find_prompt()[:-1]
        print(f"  Hostname: {hostname}")

        result = {"hostname": hostname}
        result["interfaces"] = check_interface_status(conn)
        print(f"    Interfaces: {result['interfaces']['total']} total, "
              f"{len(result['interfaces']['down'])} down")

        result["ospf"] = check_ospf_neighbors(conn)
        result["bgp"] = check_bgp_summary(conn)
        result["resources"] = check_cpu_memory(conn)
        print(f"    CPU: {result['resources']['cpu'][:60]}")

        result["reachability"] = check_reachability(conn)
        for target, status in result["reachability"].items():
            print(f"    Ping {target}: {status}")

        conn.disconnect()
        all_results[ip] = result

    # Save JSON report
    timestamp = datetime.now().strftime("%Y%m%d_%H%M%S")
    report_file = os.path.join(REPORT_DIR, f"health_check_{timestamp}.json")
    with open(report_file, "w") as f:
        json.dump(all_results, f, indent=4, default=str)

    print(f"\n  Report saved: {report_file}")
    print(f"  Duration: {datetime.now() - start}")
    print(f"\n{'='*60}\n")


if __name__ == "__main__":
    main()
```

---

# Production Script: firmware_upgrade

```python
#!/usr/bin/env python
"""
Production Firmware Upgrade Script
====================================
Transfers firmware image via SCP, verifies MD5 hash,
sets boot variable, and optionally reloads the device.
"""
import os
from datetime import datetime
from getpass import getpass
from netmiko import ConnectHandler, file_transfer
from netmiko import NetmikoTimeoutException

DEVICE_TYPE = "cisco_ios"


def get_credentials():
    username = os.getenv("NETMIKO_USERNAME") or input("Enter SSH username: ")
    password = os.getenv("NETMIKO_PASSWORD") or getpass("Enter SSH password: ")
    return username, password


def connect(ip, username, password):
    return ConnectHandler(
        device_type=DEVICE_TYPE, ip=ip,
        username=username, password=password, timeout=30
    )


def check_current_version(conn):
    """Get current running firmware version."""
    output = conn.send_command("show version | include System image")
    return output.strip()


def check_disk_space(conn, file_system="flash:"):
    """Verify sufficient disk space for the new image."""
    output = conn.send_command(f"dir {file_system} | include bytes free")
    return output.strip()


def transfer_image(conn, image_file, file_system="flash:"):
    """Transfer firmware image to device via SCP."""
    print(f"  Transferring {image_file}...")
    result = file_transfer(
        conn,
        source_file=image_file,
        dest_file=image_file,
        file_system=file_system,
        direction="put",
        overwrite_file=False,
    )
    return result


def verify_md5(conn, image_file, expected_md5, file_system="flash:"):
    """Verify the MD5 hash of the transferred image."""
    print(f"  Verifying MD5 hash (this may take several minutes)...")
    output = conn.send_command(
        f"verify /md5 {file_system}{image_file}",
        read_timeout=300
    )
    if expected_md5.lower() in output.lower():
        return True
    return False


def set_boot_variable(conn, image_file, file_system="flash:"):
    """Set the boot system variable to the new image."""
    commands = [
        f"no boot system",
        f"boot system {file_system}{image_file}",
    ]
    conn.send_config_set(commands)
    conn.save_config()
    # Verify
    output = conn.send_command("show boot | include BOOT")
    return output.strip()


def main():
    print(f"\n{'='*60}")
    print(f"  FIRMWARE UPGRADE — {datetime.now().strftime('%Y-%m-%d %H:%M:%S')}")
    print(f"{'='*60}\n")

    username, password = get_credentials()

    # Configuration — modify these for your environment
    target_ip = input("  Enter device IP: ")
    image_file = input("  Enter firmware filename: ")
    expected_md5 = input("  Enter expected MD5 hash: ")
    file_system = "flash:"

    print(f"\n  Connecting to {target_ip}...")
    conn = connect(target_ip, username, password)
    hostname = conn.find_prompt()[:-1]

    print(f"  Hostname: {hostname}")
    print(f"  Current version: {check_current_version(conn)}")
    print(f"  Disk space: {check_disk_space(conn)}")

    # Transfer
    result = transfer_image(conn, image_file, file_system)
    print(f"  Transfer result: {result}")

    # Verify
    if verify_md5(conn, image_file, expected_md5, file_system):
        print(f"  ✓ MD5 verification PASSED")
    else:
        print(f"  ✗ MD5 verification FAILED — aborting!")
        conn.disconnect()
        return

    # Set boot variable
    boot_output = set_boot_variable(conn, image_file, file_system)
    print(f"  Boot variable set: {boot_output}")

    # Ask before reload
    confirm = input("\n  Reload device now? (yes/no): ")
    if confirm.lower() == "yes":
        print(f"  Reloading {hostname}...")
        try:
            conn.send_command_timing("reload", strip_prompt=False)
            conn.send_command_timing("\n", strip_prompt=False)
        except Exception:
            print(f"  Device is reloading...")
    else:
        print(f"  Reload skipped. Device will upgrade on next reboot.")

    conn.disconnect()
    print(f"\n{'='*60}\n")


if __name__ == "__main__":
    main()
```

---

# Production Script: template_deploy

```python
#!/usr/bin/env python
"""
Template-Based Configuration Deployment
=========================================
Reads device parameters from YAML, renders device-specific
configs from a template, deploys, and verifies.
"""
import os
import yaml
from datetime import datetime
from getpass import getpass
from netmiko import ConnectHandler
from netmiko import NetmikoTimeoutException, NetmikoAuthenticationException

DEVICE_TYPE = "cisco_ios"
RENDERED_DIR = "rendered_configs"
LOG_DIR = "deploy_logs"


def get_credentials():
    username = os.getenv("NETMIKO_USERNAME") or input("Enter SSH username: ")
    password = os.getenv("NETMIKO_PASSWORD") or getpass("Enter SSH password: ")
    return username, password


def load_template(filename="config_template.yaml"):
    with open(filename) as f:
        return yaml.safe_load(f)


def render_config(template_str, device_params):
    """Replace {placeholders} with actual device values."""
    return template_str.format(**device_params)


def deploy_and_verify(ip, username, password, config_lines, hostname):
    """Connect, deploy config, save, and verify."""
    try:
        conn = ConnectHandler(
            device_type=DEVICE_TYPE, ip=ip,
            username=username, password=password, timeout=15
        )
    except (NetmikoTimeoutException, NetmikoAuthenticationException) as e:
        print(f"  [ERROR] {ip}: {e}")
        return False

    commands = [line.strip() for line in config_lines.splitlines()
                if line.strip() and not line.strip().startswith("!")]

    print(f"  Deploying {len(commands)} commands to {hostname}...")
    conn.send_config_set(commands)
    conn.save_config()

    verify = conn.send_command("show run | include router ospf")
    conn.disconnect()

    if "router ospf" in verify:
        print(f"  ✓ Verification PASSED on {hostname}")
        return True
    print(f"  ✗ Verification FAILED on {hostname}")
    return False


def main():
    start = datetime.now()
    print(f"\n{'='*60}")
    print(f"  TEMPLATE DEPLOYMENT — {start.strftime('%Y-%m-%d %H:%M:%S')}")
    print(f"{'='*60}\n")

    username, password = get_credentials()
    data = load_template()
    os.makedirs(RENDERED_DIR, exist_ok=True)

    results = []
    for device in data["devices"]:
        hostname = device["hostname"]
        ip = device["ip"]
        print(f"\n  --- {hostname} ({ip}) ---")

        rendered = render_config(data["config_template"], device)

        # Save rendered config for audit
        filepath = os.path.join(RENDERED_DIR, f"{hostname}_config.txt")
        with open(filepath, "w") as f:
            f.write(rendered)
        print(f"  Rendered config saved: {filepath}")

        success = deploy_and_verify(ip, username, password, rendered, hostname)
        results.append({"hostname": hostname, "ip": ip, "success": success})

    # Summary
    ok = sum(1 for r in results if r["success"])
    fail = sum(1 for r in results if not r["success"])
    print(f"\n  Successful: {ok}, Failed: {fail}")
    print(f"  Duration: {datetime.now() - start}")
    print(f"\n{'='*60}\n")


if __name__ == "__main__":
    main()
```

---

# Production Script: zero_touch_provision

```python
#!/usr/bin/env python
"""
Zero-Touch Provisioning Script
================================
Configures a new Cisco IOS-XE device from factory defaults
with hostname, management, routing, services, and security.
"""
import os
import yaml
from getpass import getpass
from netmiko import ConnectHandler

DEVICE_TYPE = "cisco_ios"


def get_credentials():
    username = os.getenv("NETMIKO_USERNAME") or input("Enter SSH username: ")
    password = os.getenv("NETMIKO_PASSWORD") or getpass("Enter SSH password: ")
    return username, password


def load_ztp_config(filename="ztp_devices.yaml"):
    with open(filename) as f:
        return yaml.safe_load(f)


def build_base_config(device_params):
    """Generate base configuration commands from device parameters."""
    p = device_params
    commands = [
        f"hostname {p['hostname']}",
        f"ip domain-name {p.get('domain', 'lab.local')}",
        "service timestamps debug datetime msec",
        "service timestamps log datetime msec",
        "service password-encryption",
        f"enable secret {p.get('enable_secret', 'Cisco123!')}",
        f"username admin privilege 15 secret {p.get('admin_password', 'Cisco123!')}",
        "no ip http server",
        "no ip http secure-server",
        "crypto key generate rsa modulus 2048",
        "ip ssh version 2",
        "line vty 0 4",
        " transport input ssh",
        " login local",
        " exec-timeout 15 0",
        "line console 0",
        " logging synchronous",
        " exec-timeout 15 0",
    ]

    # Management interface
    if "mgmt_interface" in p:
        commands.extend([
            f"interface {p['mgmt_interface']}",
            f" ip address {p['mgmt_ip']} {p['mgmt_mask']}",
            " no shutdown",
            f" description Management - ZTP Provisioned",
        ])

    # Loopback
    if "loopback_ip" in p:
        commands.extend([
            "interface Loopback0",
            f" ip address {p['loopback_ip']} 255.255.255.255",
            f" description Router-ID - ZTP Provisioned",
        ])

    # Routing
    if "ospf" in p:
        commands.extend([
            f"router ospf {p['ospf']['process_id']}",
            f" router-id {p.get('loopback_ip', '0.0.0.0')}",
            f" network 0.0.0.0 0.0.0.0 area {p['ospf'].get('area', '0')}",
        ])

    # NTP
    for ntp in p.get("ntp_servers", []):
        commands.append(f"ntp server {ntp}")

    # Syslog
    for syslog in p.get("syslog_servers", []):
        commands.append(f"logging host {syslog}")

    # SNMP
    if "snmp" in p:
        commands.extend([
            f"snmp-server community {p['snmp'].get('community', 'public')} RO",
            f"snmp-server location {p['snmp'].get('location', 'Unknown')}",
        ])

    # Banner
    commands.extend([
        "banner motd ^",
        "***********************************************",
        f"* {p['hostname']} - Provisioned by ZTP Script",
        "* Unauthorized access is prohibited",
        "***********************************************",
        "^",
    ])

    return commands


def main():
    print(f"\n{'='*60}")
    print(f"  ZERO-TOUCH PROVISIONING")
    print(f"{'='*60}\n")

    username, password = get_credentials()
    ztp_data = load_ztp_config()

    for device_params in ztp_data["devices"]:
        hostname = device_params["hostname"]
        ip = device_params["provision_ip"]
        print(f"\n  Provisioning {hostname} at {ip}...")

        try:
            conn = ConnectHandler(
                device_type=DEVICE_TYPE, ip=ip,
                username=username, password=password, timeout=20
            )
        except Exception as e:
            print(f"  [ERROR] Cannot connect: {e}")
            continue

        commands = build_base_config(device_params)
        print(f"  Sending {len(commands)} configuration commands...")

        output = conn.send_config_set(commands, cmd_verify=False)
        conn.save_config()

        # Verify
        ver_output = conn.send_command("show run | include hostname")
        if hostname in ver_output:
            print(f"  ✓ {hostname} provisioned successfully")
        else:
            print(f"  ✗ Verification failed for {hostname}")

        conn.disconnect()

    print(f"\n{'='*60}\n")


if __name__ == "__main__":
    main()
```
