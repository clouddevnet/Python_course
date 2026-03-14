# Chapter 3: Control Flow (Part 4: Exception Handling)

Network automation interacts with unpredictable external systems. Devices reboot, credentials expire, passwords change, and cables get unplugged. 

When a script asks a router for data and the router doesn't respond, the script will mathematically crash. To build resilient automation, we wrap dangerous code blocks in **Exception Handlers** (`try/except/finally`) to gracefully manage these failures.

---

## Section 3.13: Basic Exception Catching (`try_except_ex1.py`)

When you attempt to do something illegal in Python (like pulling a Dictionary key that does not exist), Python throws an Exception (a `KeyError`).

### Deep Dive Q&A
**What is a `try` block?**
The `try:` statement tells Python: "Attempt to execute the following indented code. If it crashes, do *not* terminate the script. Instead, immediately jump down to the `except` block."

**Why do we specify `except KeyError:`?**
It is considered dangerous to write a naked `except:` because it catches *every single possible failure*, including ones you didn't plan for (like running out of memory). By explicitly catching `KeyError`, you ensure your script only handles the specific dictionary-missing-key mistake.

### Code Example: `try_except_ex1.py`

```python
#!/usr/bin/env python
from rich import print

fw_service = {
    "name": "ftp-port",
    "port": "21",
}

# Gracefully handle with try/except
try:
    print("Trying to access fake key before KeyError...")
    fw_service["service_type"]
    print("This line will NEVER print, because the line above crashed.")
except KeyError:
    print("Inside exception handler: KeyError successfully caught!")
```

---

## Section 3.14: The `finally` Clause (`try_except_ex2.py`)

Sometimes, whether your script succeeds *or* fails, a specific action **must** occur.

### Deep Dive Q&A
**What is `finally` used for in Networking?**
Imagine you log into a Cisco router via SSH (`try`), execute a command, and the command fails because the syntax was wrong (`except`). Whether it succeeds or fails, you *must* cleanly close the SSH connection! If you don't, you might lock out other engineers. You achieve this by putting `ssh_conn.disconnect()` inside the `finally:` block.

### Code Example: `try_except_ex2.py`

```python
#!/usr/bin/env python
from rich import print

fw_service = {"name": "ftp"}

try:
    print("before KeyError")
    fw_service["service_type"]
except KeyError:
    print("Inside exception handler")
finally:
    print("\\nAlways happens - Closing active connections here!")
```

---

## Section 3.15: Catching Multiple Exceptions (`try_except_ex5.py`)

A single block of code might fail for multiple reasons. Python allows you to group error handling together.

### Deep Dive Q&A
**What is `IndexError`?**
While `KeyError` happens when you ask a Dictionary for a bad Key, an `IndexError` happens when you ask a List for a slot that doesn't exist (like asking for `my_list[100]` when it only has 5 items).

**How do you catch multiple?**
You can wrap the explicitly named Exceptions inside parentheses: `except (KeyError, IndexError):`.

### Code Example: `try_except_ex5.py`

```python
#!/usr/bin/env python

fw_service = {"name": "ftp-port"}
fw_service_keys = list(fw_service.keys())

try:
    print("before Error")
    # Try to access a Dictionary Key that doesn't exist AND
    # Try to access a List element that doesn't exist
    fw_service_keys[100]
    
except (KeyError, IndexError):
    print("Handled both KeyError and IndexError cleanly")
finally:
    print("Always happens")
```

---

## Section 3.16: Manually Raising Errors (`try_except_ex8.py`)

You don't just have to catch errors—you can aggressively throw them to stop execution when humans provide bad data.

### Deep Dive Q&A
**Why would I manually purposely crash my script?**
If reading a user's input, and they type `pod99` instead of an actual IP address, you shouldn't attempt to ping `pod99`. It's better to immediately halt the script intentionally using `raise ValueError("Invalid IP Syntax")`.

### Code Example: `try_except_ex8.py`

```python
#!/usr/bin/env python

fw_service = {"name": "ftp-port"}

msg = "CRITICAL: Something went fundamentally wrong during validation"
raise ValueError(msg)
```

With Chapter 3 complete, we fully understand how to control the execution flow of data routing through our logic. In Chapter 4, we will learn how to build our *own* commands by creating reusable Functions and importing Modules.
