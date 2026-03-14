# Chapter 2: Core Data Types (Part 2: Lists & Dictionaries)

Network devices rarely return single pieces of information. A router doesn't have one interface; it has many. An API doesn't return one setting; it returns a payload of features. 

To handle collections of data, Python provides **Lists** and **Dictionaries**.

---

## Section 2.4: Lists

A list is an ordered, mutable (changeable) collection of items. In network automation, lists are used for looping over multiple IP addresses, storing a sequence of configuration commands, or holding lines of text returned from a `show` command.

### 2.4.1 Basic List Operations

#### Deep Dive Q&A
**What defines a List?**
Lists are declared using square brackets `[]`. Items are separated by commas.

**How do we access items inside a list?**
Python lists are "zero-indexed." This means the first item is accessed using `[0]`, the second using `[1]`, etc. You can also access them backwards! `[-1]` always grabs the very last item in the list.

**Why is concatenation useful?**
Network engineers frequently combine lists of commands. For instance, you might have a list of base configurations `["logging buffered", "ntp server 10.1.1.1"]` and want to append interface-specific commands `["interface eth0", "no shut"]`. You can do this easily with `list1 + list2`.

#### Code Example: `list_ex.py`

```python
#!/usr/bin/env python
from rich import print

print("\\nList manipulation:")

# Initialize list
my_list = ["whatever", 22, "hello", 1.0]

print(my_list)
print(type(my_list))
print(f"List length: {len(my_list)}")

print(f"List index 0: {my_list[0]}")
print(f"List index 1: {my_list[1]}")
print(f"List index -1: {my_list[-1]}")

# Update list
print("\\nUpdate list:")
my_list[1] = "something else"
print(my_list)

# Concatenate list
# This creates a new list
print("\\nConcatenate list:")
new_list = my_list + ["another", "string"]
print(new_list)
```

#### Line-by-Line Breakdown
- **`my_list = ["whatever", 22, "hello", 1.0]`**: Lists can hold *mixed* data types. Here we have strings, integers, and floats living together.
- **`len(my_list)`**: The built-in `len()` function returns the total number of items in the collection (4).
- **`my_list[1] = "something else"`**: Lists are mutable. We target the second item (index 1, currently `22`) and overwrite it entirely with a new string.
- **`new_list = my_list + ["another", "string"]`**: The `+` operator, when applied to two lists, merges them into a brand new, longer list.

---

### 2.4.2 List Methods

Python lists come with built-in "methods"—functions specifically attached to the list object itself that allow you to modify it on the fly.

#### Deep Dive Q&A
**What is the difference between `.append()` and `.extend()`?**
If you have a list `[1, 2]`. 
Using `.append([3, 4])` adds the *entire list as a single nested object*: `[1, 2, [3, 4]]`.
Using `.extend([3, 4])` extracts the elements and adds them flatly: `[1, 2, 3, 4]`.

**What is `.pop()`?**
`.pop()` removes an item from a list based on its index and simultaneously *returns* it so you can save it into a variable. 

**What if I don't provide an index to `.pop()`?**
By default, `.pop()` with no arguments removes the very last item in the list `[-1]`.

#### Code Example: `list_methods.py`

```python
#!/usr/bin/env python
from rich import print

my_list = ["whatever", 22, "hello", 1.0]
print(f"Base list: {my_list}\\n")

my_list.append("append string")
print(f"After append: {my_list}\\n")

my_list.extend(["extend_str1", "extend_str2"])
print(f"After extend: {my_list}\\n")

popped_value = my_list.pop()
print(f"Popped value: {popped_value}")
print(f"After pop: {my_list}\\n")

my_list.pop(0)
print(f"After pop(0): {my_list}\\n")

# remove by value
my_list.remove(22)
print(f"After remove(22): {my_list}\\n")

my_list.insert(0, "insert string")
print(f"After insert: {my_list}\\n")
```

#### Line-by-Line Breakdown
- **`my_list.remove(22)`**: Searches the list for the exact value `22` and removes the first instance of it it finds. If `22` doesn't exist, this crashes with a `ValueError`.
- **`my_list.insert(0, "insert string")`**: Forces a new item into the specified index location (`0`). Everything else in the list shoves over one spot to the right.

---

## Section 2.5: Comprehensive List Exercise

### Objective
1. Read a YAML file containing network locations into a List. 
2. Print the first, last, and length of the list.
3. Use `.append()`, index targeting, and concatenation to manipulate the list.
4. Pop the first and last elements securely into variables.

#### Deep Dive Q&A
**Why are we importing `yaml` here?**
Network engineers use YAML constantly (like Ansible playbooks). A YAML list directly translates to a Python list using `yaml.safe_load()`.

**What if `locations.pop(0)` is called on an empty list?**
It will crash with `IndexError: pop from empty list`. Always ensure a list has data before popping!

#### Exercise Solution: `list_ex1.py`

```python
#!/usr/bin/env python
import yaml
from rich import print

filename = "locations.yml"

# Read in file as YAML
with open(filename) as f:
    locations = yaml.safe_load(f)

print()

# Print the list
print(locations)

# Print first element of list
print(f"First element: {locations[0]}")

# Print last element of list
print(f"Last element: {locations[-1]}")

# Print length of the list
print(f"List length: {len(locations)}")

# Add element to the list
locations.append("Leipzig")

# Change the fourth element of the list to be 'Stuttgart'
locations[3] = "Stuttgart"

# Print the current list
print(locations)

# Use list concatentation to add the following list ["Dortmund", "Essen"]
# Could also do: locations += ["Dortmund", "Essen"]
locations = locations + ["Dortmund", "Essen"]

# Print the current list
print(locations)

# Pop the first element of the list into a variable
city1 = locations.pop(0)

# Pop the last element of the list into a variable
city_n = locations.pop()

# Print 'city1', 'city_n', and current 'locations' list
print(f"{city1=}")
print(f"{city_n=}")
print(f"{locations=}")
```

#### Line-by-Line Breakdown
- **`yaml.safe_load(f)`**: Specifically digests the YAML structured language into native Python structures.
- **`locations[3] = "Stuttgart"`**: Replaces the 4th object dynamically.
- **`locations = locations + [...]`**: This overwrites the original variable with the newly concatenated version.

---

## Section 2.6: Dictionaries

If Lists are just ordered sequences, **Dictionaries** are structured mappings. They store data in `key: value` pairs. Over 90% of REST API interactions involve receiving JSON data and mapping it directly into a Python Dictionary.

### 2.6.1 Basic Dictionary Operations

#### Deep Dive Q&A
**What defines a Dictionary?**
Dictionaries use curly braces `{}`. Data is bound together using colons `key: value`. 

**How do we access data in a Dictionary?**
Instead of using numerical indexes like `my_list[0]`, you use the explicit key name, like `my_dict["ip_addr"]`. This is immensely powerful because you don't need to know *where* the IP address is in the payload, you just ask for it by name.

**What if I try to access a key that isn't there?**
Executing `my_dict["fake_key"]` crashes the script with a `KeyError`. We will cover how to avoid this securely using the `.get()` method or `try/except` blocks in Chapter 3.

#### Code Example: `dict_ex.py`

```python
#!/usr/bin/env python
from rich import print

# Common way dictionary is formatted
my_dict = {
    "ip_addr": "10.1.1.1",
    "platform": "cisco_ios",
    "vendor": "cisco",
    "model": "1921",
}

print(my_dict)
print(my_dict["ip_addr"])
print(my_dict["platform"])

# Add a new key
my_dict["serial_number"] = "A1234567"

print()
print(my_dict)
print()
```

#### Line-by-Line Breakdown
- **`"ip_addr": "10.1.1.1"`**: establishing a key `"ip_addr"` that houses the string `"10.1.1.1"`.
- **`print(my_dict["platform"])`**: Explicitly retrieves the value associated with `"platform"` (which outputs `"cisco_ios"`).
- **`my_dict["serial_number"] = "A1234567"`**: Unlike a list `.append()`, to add a new item to a dictionary, you simply act as if the key already exists and define it. Python catches it and dynamically inserts the new key-value string.

---

## 2.7 Comprehensive Dictionary Exercise

### Objective
1. Load a complex network object from a JSON file.
2. Extract specific routing keys (name, subnet4, mask-length4).
3. Extract nested keys (dictionaries inside of dictionaries).
4. Perform add, update, and `.pop()` deletion methods.

#### Deep Dive Q&A
**Why are we importing `json` here?**
Similar to YAML, a JSON payload generated by a firewall or router inherently translates into a Python Dictionary. 

**What is a "Nested Dictionary"?**
It's a dictionary whose *value* is another dictionary. To access it, you chain the brackets back to back: `network_obj["domain"]["uid"]`.

**How do we delete keys safely?**
The `.pop("color")` method works on dictionaries too. It finds the key `"color"`, removes it from the dictionary entirely, and acts as a safeguard.

#### Exercise Solution: `dict_ex1.py`

```python
#!/usr/bin/env python
import json
from rich import print

with open("net_object_net128.json") as f:
    network_obj = json.load(f)

# Print the dictionary
print(network_obj)

# Retrieve the 'name', 'subnet4' and 'mask-length4' fields (store into variables)
name = network_obj["name"]
network = network_obj["subnet4"]
netmask = network_obj["mask-length4"]

# Print these three variables out.
print(f"Network Object: {name} ({network}/{netmask})")

# Retrieve the network_obj['domain']['uid'] field (nested dictionary) and save to a variable.
domain_uid = network_obj["domain"]["uid"]
print(f"Domain UID: {domain_uid}")

# Add a new key 'location' to the dictionary (set the value to "Munich").
network_obj["location"] = "Munich"

# Change the 'location' key to "Cologne"
network_obj["location"] = "Cologne"

# Delete the 'color' key
network_obj.pop("color")

# Print your dictionary
print(network_obj)
```

#### Line-by-Line Breakdown
- **`json.load(f)`**: Paired with `open()`, this parses raw JSON strings directly into the `network_obj` dictionary.
- **`network = network_obj["subnet4"]`**: Targeted key extraction for automation variables.
- **`network_obj["location"] = "Munich"`**: Creates the key. The line below it **overwrites** it with "Cologne". Dictionaries cannot have duplicate keys!
- **`network_obj.pop("color")`**: Destructively removes the entire key and value mapping for "color" out of memory.

In the final section of Chapter 2, we will focus exclusively on File I/O (Input/Output)—the programmatic art of writing these lists and dictionaries back out into persistent storage.
