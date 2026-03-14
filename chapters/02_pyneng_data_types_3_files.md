# Chapter 2: Core Data Types (Part 3: Files, JSON, & YAML)

Lists and Dictionaries are incredible for manipulating data in memory, but once your script finishes executing, everything in RAM evaporates. To persist data for future use (like saving a routing table backup or reading an IP inventory), you must interact with the host File System.

In this final section of Chapter 2, we will cover reading and writing raw text files natively in Python, and how to import/export structured data formats like JSON and YAML.

---

## Section 2.8: Native Text Files

Python has a built-in `open()` function that creates a file object, allowing you to read its contents or write new strings into it.

### 2.8.1 Reading and Writing Files (The Manual Way)

#### Deep Dive Q&A
**Why do we pass `"r"` or `"w"` to the `open()` function?**
These are mode flags. `"r"` stands for Read mode (the default). If you try to write to a file opened in `"r"` mode, it crashes securely preventing accidental data loss. `"w"` stands for Write mode. **WARNING:** Opening a file in `"w"` mode instantly deletes all existing contents of the file! To append natively, use `"a"`.

**What is the difference between `.read()` and `.readlines()`?**
The `.read()` method returns the entire file as one massive monolithic String block. The `.readlines()` method parses the file and returns a Python List, where each line of the text file is its own string element in the list.

**Why must we run `f.close()`?**
Opening a file locks it at the operating system level. If your script crashes before `.close()` is called, that file might remain locked, meaning no other process can access it until you reboot.

#### Code Example: `read_file.py`

```python
#!/usr/bin/env python
from rich import print

# Open file
f = open("my_file.txt", "r")

# Read entire file contents
data = f.read()
print(data)

# Go back to start of the file
f.seek(0)

# Read the entire file, but as a list of lines
data = f.readlines()
print(type(data))
print(data)

# Go back to start of the file
f.seek(0)

# Loop over the file (haven't covered loops yet)
print("Looping over file")
for line in f:
    # Eliminate double enter
    line = line.strip()
    print(repr(line))

# Cloes file
f.close()
```

#### Code Example: `write_file.py`

```python
#!/usr/bin/env python

f = open("new_file.txt", "w")
f.write("--> hello world <--\\n")
f.write("something else\\n")
f.write("one last line\\n")
f.close()
```

---

### 2.8.2 Context Managers (The Pythonic Way)

To avoid the dangerous file-locking issue when `.close()` fails to trigger, Python introduced the `with` statement, known as a Context Manager.

#### Deep Dive Q&A
**What does the `with` statement actually do?**
When you indent a block of code under a `with` statement, Python guarantees that the moment the code un-indents (either by completing normally or by crashing), it will automatically and securely close the file object. 

**Should I always use this?**
Yes. You should almost never write `f = open()`. Always use `with open() as f:`.

#### Code Example: `file_cm.py` & `write_file_cm.py`

```python
#!/usr/bin/env python

# Context manager automatically closes the file (when done)
with open("my_file.txt") as f:
    data = f.read()

print(data)

# Writing via Context Manager
with open("new_file.txt", "w") as f:
    f.write("--> hello world <--\\n")
    f.write("something else\\n")
    f.write("one last line\\n")
```

---

## Section 2.9: Structured Data (JSON & YAML)

Reading raw text forces engineers into complex Regular Expression mapping. A smarter approach is to use structured serialization formats. JSON is universally used by REST APIs. YAML is universally used by automation engines like Ansible. 

#### Deep Dive Q&A
**Why use `.load()` instead of `.read()`?**
If you open a JSON file and run `.read()`, Python treats it as a single block of text. You cannot run Dictionary `.get()` queries against a block of text. The `json.load()` function intelligently parses the text and natively converts it into a Python Dictionary or List!

**How do we save Dictionaries back to files?**
The inverse of `.load()` is `.dump()`. We use `json.dump(data, f)` to export the dictionary back into text format onto the hard drive.

#### Code Example: JSON & YAML Operations

```python
import json
import yaml
from rich import print

# --- Reading JSON ---
with open("gaia_api.json") as f:
    # Converts JSON text into Python Dictionary
    json_data = json.load(f)
print(json_data)

# --- Writing JSON ---
my_data = {"key1": "val1", "key2": "val2", "key3": "val3"}
# Open in Write mode!
with open("my_file.json", "w") as f:
    json.dump(my_data, f, indent=4)  # indent=4 makes it pretty-printed!

# --- Reading YAML ---
with open("gaia_api.yaml") as f:
    # safe_load is required for YAML security
    yaml_data = yaml.safe_load(f)
print(yaml_data)

# --- Writing YAML ---
my_list = ["some", "list", "of", "strings"]
with open("my_file.yml", "w") as f:
    yaml.dump(my_list, f, default_flow_style=False)
```

---

## Section 2.10: Comprehensive File Exercise

### Objective
1. Open up a file containing a list of network objects named `network_objects.json`.
2. First, read the file purely as raw text using `.read()`. Inspect its type.
3. Second, read the file using `json.load()`. Inspect its type and the type of its nested dictionary `"objects"`.

#### Deep Dive Q&A
**Why is it important to check the `type()`?**
To prove the structural difference! When we print the raw text, it *looks* like a dictionary on the screen, but running `type(data)` proves it is just a `<class 'str'>`. Only after running `json.load()` does it officially become `<class 'dict'>`.

#### Exercise Solution: `files_ex1.py`

```python
#!/usr/bin/env python
import json
from rich import print

filename = "network_objects.json"

# Read in file as text
with open(filename) as f:
    data = f.read()

# rich.print is misleading here as it would make it look like a data structure
print(f"\\nRead in file({filename}) as a string")
print(f"Type 'data' var: {type(data)}")

# Read in file as JSON
with open(filename) as f:
    data = json.load(f)
print(f"\\nRead in file({filename}) as a data structure (dictionary)")
print(f"Type 'data' var: {type(data)}")
print(f"Type data['objects'] field: {type(data['objects'])}")
print()
```

#### Line-by-Line Breakdown
- **`data = f.read()`**: Takes the whole JSON file and treats it as standard text.
- **`type(data)`**: Dynamically returns string datatype. 
- **`data = json.load(f)`**: Forces Python's `json` library engine to parse the text and structure it securely into memory.
- **`type(data['objects'])`**: Because it translates into a Dictionary, we can natively query the nested `'objects'` key perfectly!

By mastering data typing, you now have the capabilities to construct, slice, parse, format, and save network state reliably. Next in Chapter 3, we dive into logic pathways with Conditionals and Loop Iterators.
