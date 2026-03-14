# Chapter 2: Core Data Types - Lists and Dictionaries

In the previous section, we covered parsing and slicing Strings. When you parse output, you usually need somewhere to store it. In Python, the two most common and powerful data structures for storing parsed network data are **Lists** and **Dictionaries**.

## Section 2.3: Python Lists

A list is an ordered, mutable collection of elements. Think of it like a spreadsheet column. In networking, lists typically hold IP addresses, interfaces, or VLAN ids.

### Code Example: `list_ex.py` and `list_methods.py`

From `python_course_mar26/class1/lists`, let's see how to manipulate these arrays.

```python
my_list = ["zzz", "world", "foo", 22, None]

# Indexing (0-based)
print(my_list[0])  # "zzz"
print(my_list[2])  # "foo"
print(my_list[-1]) # None
```

In networking, `.pop()`, `.append()`, and `extend()` are some of your best tools when iterating through VLANs or routing tables:

```python
# list_methods.py excerpt
my_list = ["zzz", "world", "foo", 22, None]
my_list.append(42)  # Adds 42 to the end of the list

some_list = [0, "hello"]
my_list.extend(some_list) # Merges some_list into my_list

pop_val = my_list.pop(0) # Removes and returns "zzz"

my_list.remove("foo") # Deletes "foo" by value
```

### Exercise: YAML to Lists (`list_ex1.py`)

YAML files are incredibly common in Network Automation (like Ansible playbooks). Using the `yaml` module, you can read them seamlessly into python lists. You need a `locations.yml` file to run this script.

```python
import yaml
from rich import print

filename = "locations.yml"

# Read in file as YAML
with open(filename) as f:
    locations = yaml.safe_load(f)

# Print first element of list
print(f"First element: {locations[0]}")

# Print length of the list
print(f"List length: {len(locations)}")

# Add element to the list
locations.append("Leipzig")

# Change the fourth element of the list to be 'Stuttgart'
locations[3] = "Stuttgart"

# Print the current list
print(locations)

# Pop the first element of the list into a variable
city1 = locations.pop(0)
print(f"{city1=}")
```

---

## Section 2.4: Python Dictionaries

A dictionary is an unordered, mutable collection of key-value pairs. Think of it like a JSON API response from a Cisco Meraki or Nexus switch. You access elements by their `key` rather than an index number.

### Code Example: `dict_ex.py`

This example mimics a Check Point firewall service object.

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

Notice `domain` is a nested dictionary. You can navigate it precisely:

```python
# Retrieving nested keys
print(ftp_service["domain"]["name"]) # Check Point Data
```

### Exercise: JSON to Dictionaries (`dict_ex1.py`)

When calling network APIs, responses come formatted as JSON text streams. `json.load()` converts JSON text into a Python Dictionary natively.

*Prerequisite: ensure you have `net_object_net128.json` downloaded locally before executing this.*

```python
import json
from rich import print

with open("net_object_net128.json") as f:
    network_obj = json.load(f)

# Retrieve the 'name', 'subnet4' and 'mask-length4' fields (store into variables)
name = network_obj["name"]
network = network_obj["subnet4"]
netmask = network_obj["mask-length4"]

print(f"Network Object: {name} ({network}/{netmask})")

# Add a new key 'location' to the dictionary
network_obj["location"] = "Munich"

# Delete the 'color' key
network_obj.pop("color")

print(network_obj)
```

In the next chapter, we will bridge Data Types and execution by covering Control Flow conditional statements (`if/else`) and looping methodologies over datasets.
