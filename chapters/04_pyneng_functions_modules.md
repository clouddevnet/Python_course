# Chapter 4: Functions, Modules, and Libraries

As your network automation footprint grows, your scripts will become unmanageably large if you copy and paste the same 50 lines of code every time you want to connect to a new router. **Functions** allow you to wrap repetitive logic into a single reusable block. **Libraries** (Modules) allow you to import external code written by other engineers to supercharge your programs.

This chapter concludes Part 1 of our practical guide, bridging foundational Python theory heavily into the functional logic needed for Part 2's Netmiko deep dive.

---

## Section 4.1: Defining Functions (`func_ex1.py`)

A function is declared using the `def` keyword. Think of a function as a custom machine: you feed raw materials (arguments) into it, it processes them, and it spits out a finished product (`return`).

### Deep Dive Q&A
**What happens if a function doesn't have a `return` statement?**
By default, if you don't explicitly `return` data back to the main script, the function completes its task and implicitly returns `None`.

**What is the difference between defining and calling?**
Just defining a function `def my_func():` does absolutely nothing on its own. It just registers the machine in memory. You physically have to push the start button by "calling" it: `my_func()`.

### Code Example: Function Definitions and Basic Exercises

```python
#!/usr/bin/env python
from rich import print

# Definition
def my_func(x, y):
    print(x)
    print(y)
    return x + y

# Calling the function and saving its returned product
ret_val = my_func(7, 2)
print(f"{ret_val=}")

# Exercise: Simple Print
def fw_func():
    print("Hello world")

fw_func()
```

---

## Section 4.2: Arguments (Positional vs Keyword)

When feeding variables into a function, Python needs to know which variable maps to which slot.

### Deep Dive Q&A
**What is a Positional Argument?**
If you call `fw_func("chkpnt", "1.1.1.1")`, Python blindly strictly assigns `"chkpnt"` to the very first variable in the function definition, and `"1.1.1.1"` to the second. Position matters entirely.

**What is a Keyword Argument?**
If you call `fw_func(ipaddr="1.1.1.1", name="chkpnt")`, you explicitly name the slots. Order completely stops mattering! Python correctly maps them based on explicitly declared variable names.

**Can I mix them?**
Yes, but Positional arguments *must* come first. You cannot provide a keyword argument, and then suddenly provide a naked positional argument.

### Code Example: `func_ex3.py` (Exercise)

```python
#!/usr/bin/env python
from rich import print

def fw_func(name, ipaddr, os_version="R82"):
    print(f"{name=}")
    print(f"{ipaddr=}")
    print(f"{os_version=}")
    return f"{name}-{ipaddr}-{os_version}"

# Positional arguments
print("\\nFunction call with positional arguments")
ret_val = fw_func("chkpnt-pod99", "3.77.44.109", "R81.20")

# Named (Keyword) arguments
print("\\nFunction call with named arguments")
ret_val = fw_func(
    os_version="R82",
    ipaddr="3.77.44.100",
    name="chkpnt-pod1",
)

# Both named and positional
print("\\nFunction call with both positional and named arguments")
ret_val = fw_func(
    "chkpnt-pod2",
    os_version="R82.10",
    ipaddr="3.77.44.9",
)
```

#### Line-by-Line Breakdown
- **`def fw_func(..., os_version="R82"):`**: This declares a **Default Parameter**. If the human calling the function forgets to provide an `os_version`, the function won't crash! It will gracefully assume the value is `"R82"` and proceed.

---

## Section 4.3: Unpacking Arguments (`*args` and `**kwargs`)

Sometimes your network data is already grouped inside a List or a Dictionary, and it's exhausting to manually extract every single item to pass into a function. Python allows "unpacking".

### Deep Dive Q&A
**What does the asterisk `*` do?**
If you pass `*my_list` into a function call, Python violently explodes the list apart, taking each element and blasting them into the function sequentially as Positional Arguments.

**What do double asterisks `**` do?**
The double asterisk targets Dictionaries. If you pass `**my_dict`, Python unpacks the dictionary mapping the explicitly named dictionary Keys directly to the function's Keyword Arguments!

### Code Example: Unpacking Lists and Dicts (`func_ex4.py` & `func_ex5.py`)

```python
#!/usr/bin/env python

def my_func(x, y, z=100):
    return x + y + z

# Unpacking a List (Positional map: x=1, y=7, z=99)
my_list = [1, 7, 99]
ret_val = my_func(*my_list)
print(ret_val)

# Unpacking a Dictionary (Keyword map)
my_dict = {
    "x": 11,
    "y": 22,
    "z": 33,
}
ret_val = my_func(**my_dict)
print(ret_val)
```

---

## Section 4.4: Library Modules and `sys.path` 

You aren't restricted to the code you write yourself. Python allows you to `import` external libraries containing thousands of functions written by others.

### Deep Dive Q&A
**What is the difference between `import re` and `from re import search`?**
Using `import re` gives you access to the entire Regular Expression library, but you have to specifically call it by explicitly saying `re.search()`.
Using `from re import search` tells Python to extract *only* the `search` function and load it natively into memory, allowing you to just type `search()` directly.

**How does Python know where to find these external libraries?**
Python looks through a highly specific list of directories defined in the operating system environment. You can physically view this list by printing `sys.path`.

**What if I want to see exactly where a module is installed on my hard drive?**
You can print the module's hidden `__file__` attribute! This is an incredible debugging tool when deploying Network Automation containers.

### Code Example: Libraries

```python
import sys
import re
from rich import print

# View exactly what directories Python searches for modules
print("\\nsys.path:")
print("-" * 30)
print(sys.path)

# View exactly where the Regex module is strictly loaded from
print(re.__file__)
```

### Part 1 Conclusion
You have now heavily mastered Strings, Data Structures, Control Flow, and Functions. You are ready to automate infrastructure. 

In **Part 2 of this Guide** (Chapters 5 through 16), we pivot away from theoretical exercises and begin our massive, 12-Class deep dive into Netmiko—connecting, commanding, and manipulating real network devices.
