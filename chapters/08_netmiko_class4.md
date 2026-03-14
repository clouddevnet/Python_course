# Part 2: Netmiko Deep Dive
# Chapter 8: Handling Interactive Prompts (Class 4)

Standard network automation assumes sending one command and getting one text block back. But what happens if the router interrupts you?

If you issue `del flash:/somefile.txt`, the router aggressively halts and asks: `Delete filename [somefile.txt]?`. You must programmatically answer `\\n` (Enter), and then it asks a second question: `[confirm]?`, where you must answer `y`.

In Chapter 8, using scripts from `netmiko_course/class4`, we detail how to conquer these interactive multi-step dialogues using sequential Expect Strings and Netmiko's powerful Multiline engines.

---

## Section 8.1: Sequential Expect Strings (`send_command_prompting.py` & `exercise2.py`)

When dealing with a known series of router questions, you can chain multiple `.send_command()` calls together, each specifically hunting for the text of the next question in the dialogue tree.

### Deep Dive Q&A
**Why must `strip_prompt` and `strip_command` be False?**
By default, Netmiko attempts to cleanly remove the command you typed and the trailing router prompt from the final screen output so you only get the pure data. However, in an interactive dialogue, the "prompt" is the actual question the router is asking you! If Netmiko strips it away, your automation logic will break.

**What does `\n` do?**
In Python strings, `\\n` is the carriage return (the Enter key). When the router asks `Destination filename [testx.txt]?`, pressing Enter accepts the default `[testx.txt]`.

### Code Example: Deleting a file

```python
#!/usr/bin/env python
import os
from netmiko import ConnectHandler
from getpass import getpass

password = os.getenv("NETMIKO_PASSWORD") if os.getenv("NETMIKO_PASSWORD") else getpass()

my_device = {"device_type": "cisco_ios", "host": "cisco3.lasthop.io", "username": "pyclass", "password": password}

with ConnectHandler(**my_device) as net_connect:
    filename = "test_file.txt"
    cmd = f"del flash:/{filename}"

    # Step 1: Send 'del' command, expect it to say "Delete filename"
    output = net_connect.send_command(
        cmd, expect_string=r"Delete filename", strip_prompt=False, strip_command=False
    )
    
    # Step 2: Press Enter '\n' to accept the filename, expect it to ask for "confirm"
    output += net_connect.send_command(
        "\\n", expect_string=r"confirm", strip_prompt=False, strip_command=False
    )
    
    # Step 3: Send 'y' to confirm, wait for the standard router '#' prompt to return
    output += net_connect.send_command(
        "y", expect_string=r"#", strip_prompt=False, strip_command=False
    )
    
    print(output)
```

---

## Section 8.2: Bypassing Expects with Timing (`send_command_timing_prompting.py` & `exercise1.py`)

If you don't want to mathematically calculate exact Expect Strings for every single dialogue step, you can use `send_command_timing` to just wait for terminal silence between each answer!

### Deep Dive Q&A
**What is `fast_cli=False`?**
Netmiko tries to optimize connections to go as fast as medically possible. If you are deliberately relying on `send_command_timing` to slowly answer prompts based on terminal silence delays, you must tell Netmiko to chill out by disabling `fast_cli`.

**Why use `if "confirm" in output:`?**
Timing commands don't know what the router is asking, they just know the router stopped talking. By manually checking `if "Do you want to over write" in output`, we can add dynamic logic! If the file doesn't exist, the router won't ask to overwrite it, and our script won't blindly type `y` at the wrong menu.

### Code Example: Copying Files Dynamically

```python
#!/usr/bin/env python
from netmiko import ConnectHandler
# ... setup logic ...
my_device = {"device_type": "cisco_ios", "host": "cisco3.lasthop.io", "username": "pyclass", "password": "abc", "fast_cli": False}

net_connect = ConnectHandler(**my_device)

# Step 1: Send the copy command
output = net_connect.send_command_timing(
    command_string="copy flash:/testx.txt flash:/test-ktb.txt", strip_prompt=False, strip_command=False
)

# Step 2: Check if it's asking for destination filename
if "Destination filename" in output:
    output += net_connect.send_command_timing(command_string="\\n", strip_prompt=False, strip_command=False)

# Step 3: Check if it's asking to overwrite!
if "Do you want to over write" in output:
    output += net_connect.send_command_timing(command_string="y", strip_prompt=False, strip_command=False)

print(output)
net_connect.disconnect()
```

---

## Section 8.3: Massive Interactive Multilines (`exercise3.py` & `exercise4.py`)

The most famous interactive dialogue in networking is the traditional Extended Ping, which asks 7 sequential questions. You do not want to write 7 `if` statements. Netmiko natively supports `send_multiline()`.

### Deep Dive Q&A
**How does `send_multiline()` work?**
You feed it a List of Tuples. Each Tuple contains `("What I want to type", "What prompt I expect back before typing the next thing")`. Netmiko handles mapping the entire chain automatically!

**How does `send_multiline_timing()` work?**
Same concept, but you don't even need Tuples! Just feed it a straight List of strings, and Netmiko will fire the string, wait for silence, fire the next string, wait for silence, down the entire list!

### Code Example: Extended Ping via Explicit Multiline

```python
#!/usr/bin/env python
from netmiko import ConnectHandler

device = {"host": "cisco3.lasthop.io", "username": "pyclass", "password": "abc", "device_type": "cisco_xe"}

# List of Tuples mapping (Command To Send, Expected Router Response)
commands = [
    ("ping", "Protocol"),
    ("\\n", "Target"),
    ("8.8.8.8", "Repeat count"),
    ("100", "Datagram size"),
    ("\\n", "Timeout"),
    ("\\n", "Extended commands"),
    ("\\n", "Sweep range"),
    ("\\n", "#"),
]

with ConnectHandler(**device) as ssh_conn:
    # Netmiko handles the entire 8-step interview flawlessly in one line wrapper
    output = ssh_conn.send_multiline(commands)
    print(output)
```

In Chapter 9 (Class 5), we will finally explore Configuration Changes (`send_config_set`) and how Netmiko can auto-detect what type of router you are logging into!
