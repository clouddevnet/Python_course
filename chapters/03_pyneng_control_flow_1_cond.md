# Chapter 3: Control Flow (Part 1: Conditionals)

Now that we know how to store information using Lists and Dictionaries, we must be able to control how our code processes it. In Network Automation, this takes the form of Conditional logic (`if/elif/else`) to handle different network operating systems, Looping (`for/while`) to iterate over devices, and Error Handling (`try/except`) to deal with unavailable devices.

In Part 1 of Chapter 3, we dive deeply into Conditionals, iterating over a progression of scripts ranging from basic string matching to parsing API versions natively.

---

## Section 3.1: Basic Conditionals (`cond_ex1.py`)

Conditionals evaluate boolean logic (True/False) to make decisions in your code. The foundational script loads JSON TCP service data and makes logic loops based on string values.

### Deep Dive Q&A
**Why do we use `elif` instead of multiple `if` statements?**
If you use multiple `if` statements consecutively, *every single one is evaluated* regardless of whether the previous one matched. Using `elif` links the logic into a chain. The moment an `if` or `elif` condition is True, the rest of the chain is skipped completely, saving processor cycles!

**How does `else` function here?**
The `else` block is a catch-all funnel. If a service is neither FTP nor DNS, it falls cleanly into the `else` block to simply print its name.

**What if I forget the colon `:` at the end of the `if` statement?**
Python will immediately crash with a `SyntaxError: expected ':'`. Control flow blocks *must* contain a colon to define where the indented block begins.

### Code Example: `cond_ex1.py`

```python
#!/usr/bin/env python
import ipdb  # noqa
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

#### Line-by-Line Breakdown
- **`import ipdb`**: A robust debugging tool library, though standard Python users typically rely on `pdb`.
- **`if service_name == "ftp":`**: The script uses the `==` operator to strictly compare the current string variable against the text.

---

## Section 3.2: Calling Functions inside Conditionals (`cond_ex2.py` / `cond_ex3.py`)

Sometimes you want an `if` statement to trigger a secondary action, like checking the health of a node *only* after confirming it's active.

*Note: `cond_ex2.py` and `cond_ex3.py` demonstrate the identical implementation pattern iterating on the first script.*

### Deep Dive Q&A
**Why are function returns used in conditionals?**
If `check_service(service)` returned `True` (assuming the FTP service was healthy), the nested `if check:` evaluates that boolean directly to print success. 

**What if `check_service` returns nothing?**
If a function `pass`es without a `return` statement, Python implicitly returns `None`. Setting `check = None`, followed by `if check:`, evaluates to `False` due to our previous lesson on Truthiness. 

### Code Example

```python
#!/usr/bin/env python
import ipdb  # noqa
import json
from rich import print

def check_service(service):
    """Just placeholder function."""
    pass

with open("tcp_services.json") as f:
    services = json.load(f)

service_list = services["objects"]
print(len(service_list))

for service in service_list:
    service_name = service["name"]
    if service_name == "ftp":
        print("Found FTP Service")
        check = check_service(service)
        if check:
            print("FTP service check passed")
    elif service_name == "domain-tcp":
        print("Found DNS (TCP)")
        check_service(service)
    else:
        print("Service not found")
        print("Nothing else to do")
```

---

## Section 3.3: API Version Checking (`cond_ex4.py` & `cond_ex5.py`)

Network API endpoints frequently update. Automation frameworks often use `in` string checks and float evaluations to figure out which payload structures to send.

### Deep Dive Q&A
**What does `in` keyword do here?**
`if "1.8" in supported_versions:` checks if the string `"1.8"` exists anywhere inside the YAML list array.

**Why checking `"1."` inside `api_version`?**
When performing `if "1." in api_version`, the script is blindly searching for the substring `"1."` inside the string `"1.8"`. Since it finds it, it knows this is a version 1 architecture API.

**How do we handle mathematical conditions (`cond_ex5`)?**
The line `float(api_version) >= 1.8` takes the string `"1.8"`, forces it into a decimal Number (a `float`), and mathematically checks if it is structurally greater than or equal to `1.8`. 

### Code Example: `cond_ex5.py`

*(This script builds perfectly on the concepts from `cond_ex4.py`)*

```python
#!/usr/bin/env python
import ipdb  # noqa
import yaml
from rich import print

with open("api_support_versions.yml") as f:
    api_versions = yaml.safe_load(f)

supported_versions = api_versions["supported-versions"]

# ['1', '1.1', '1.2', '1.3', '1.4', '1.5', '1.6', '1.7', '1.8']
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

#### Line-by-Line Breakdown
- **`base_api == "v1" and float(...)`**: Combines a strict String equivalency match with a parsed Float mathematical comparison inside a singular `and` short-circuiting gate!

---

## Section 3.4: Comprehensive Conditional Exercise

### Objective
1. Utilize the `input()` function to ask the user to type in their Pod Number.
2. Build a firewall name using f-strings (e.g. `chkpnt-pod<number>`).
3. Write an `if / elif / else` block checking if it is `pod1`, `pod99`, or neither.

#### Deep Dive Q&A
**What is `input()` doing?**
It pauses script execution entirely and waits dynamically for the human to type something into the terminal and strike the Enter key.

**What if the user types a literal space like ` `?**
The script will map `fw_name = "chkpnt-pod "`, which will fail both the `if` and `elif` checks, successfully catching it in the safe `else` block!

#### Exercise Solution: `cond_ex1.py`

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

#### Line-by-Line Breakdown
- **`input("Enter pod number: ")`**: Natively prompts the terminal for human input.
- **`fw_name = f"chkpnt-pod{pod_numb}"`**: Takes the human input variable and elegantly formats it using F-Strings into the expected Check Point firewall hostname framework.
- **`elif fw_name == "chkpnt-pod99":`**: Validates secondary explicit matching logic.
