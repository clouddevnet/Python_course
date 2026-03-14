# Chapter 2: Core Data Types (Part 1: Booleans & Strings)

A deep dive into network automation requires an absolute mastery of basic Data Types. We pull the structural knowledge from the Pyneng theoretical methodology and map it directly onto our specific networking scripts from `python_course_mar26`.

In this first part, we will cover Booleans (True/False logic) and Strings (Text manipulation). 

---

## Section 2.1: Booleans and Truthiness

Booleans represent binary logic: `True` or `False`. While seemingly simple, Python defines something called "Truthiness," where non-boolean data types evaluate to True or False depending on whether they contain data.

### 2.1.1 Truthiness Evaluation

Let's look at how standard data structures behave when cast to a Boolean.

#### Deep Dive Q&A
**What is this doing?**
It evaluates empty strings, the number zero, empty lists, and empty dictionaries to determine their boolean value using the `bool()` function.

**Why is truthiness useful?**
Network engineers constantly pull data (like parsing OSPF neighbors). If a router returns no neighbors, it returns an empty list `[]`. Instead of checking `if len(neighbors) == 0:`, Python allows you to write `if neighbors:`. An empty list evaluates to `False`, so the condition handles it elegantly!

**How does it work?**
Python considers any empty sequence or collection (like `""`, `[]`, `{}`), and the integer `0` or `0.0`, to be `False`. Everything else is `True`.

**What if we test a string with just a space `" "`?**
A string with a space is *not empty*. It contains a character. Therefore, `bool(" ")` evaluates to `True`.

#### Code Example: `truish.py`

```python
#!/usr/bin/env python
from rich import print

# Strings
print("\\nStrings:")
some_str = ""
print(bool(some_str))

# Numbers
print("\\nNumbers:")
some_int = 0
print(bool(some_int))
some_float = 0.0
print(bool(some_float))

# Lists
print("\\nLists:")
some_list = []
print(bool(some_list))

# Dict
print("\\nDict:")
some_dict = {}
print(bool(some_dict))
```

#### Line-by-Line Breakdown
- **`from rich import print`**: Imports the specialized `rich` print function for color-coded console output.
- **`some_str = ""`**: Creates an empty string.
- **`print(bool(some_str))`**: The `bool()` function explicitly forces the variable into a boolean context. Because `some_str` is missing data, this prints `False`.
- **`some_int = 0` and `some_list = []`**: The same logic applies integer zeros and empty brackets.

---

### 2.1.2 Short Circuit Logic

Python optimizes boolean checks (`and` / `or`) using "short-circuit" evaluation.

#### Deep Dive Q&A
**What is Short Circuit Logic?**
It means Python stops evaluating a boolean statement the instant it knows the final answer.

**Why is this helpful in networking?**
Imagine you check `if ping_success() and parse_bgp():`. If `ping_success()` is False, the router is unreachable! The `and` gate requires both to be True. Since the first is False, Python *short-circuits* and never attempts to run `parse_bgp()`, saving you from an SSH timeout error.

**How does `or` handle this?**
With `or`, if the first condition is `True`, the entire statement is guaranteed to be True. Python stops immediately and never executes the second condition.

**What if I want both functions to run regardless?**
You should execute them sequentially before the `if` block, assign their returns to variables, and use those variables in the `if` block.

#### Code Example: `show_circuit.py`

```python
#!/usr/bin/env python
from rich import print

# and: if the first condition is False, we are done.
check_cond = False
if check_cond and my_func():  # noqa
    print("Never printed")

# or: if the first condition is True, we are done.
skip_func = True
if skip_func or my_func():  # noqa
    print("Always printed")
```

#### Line-by-Line Breakdown
- **`check_cond = False`**: Initializes our first boolean.
- **`if check_cond and my_func():`**: The `and` operator sees `False` on the left side. It immediately exits the if-block. `my_func()` is completely ignored.
- **`skip_func = True`**: Initializes a True boolean.
- **`if skip_func or my_func():`**: The `or` operator sees `True`. Since only one side needs to be true, it short-circuits. `print("Always printed")` executes safely.

---

## Section 2.2: Strings

Manipulating text is fundamentally important. Whether decoding an IP address or parsing `show run` on a Cisco router, Strings are king.

### 2.2.1 F-String Formatting

F-strings provide a concise, readable way to embed variables inside text, especially useful for formatting CLI tables.

#### Deep Dive Q&A
**What is an f-string?**
An f-string defines string formatting dynamically by putting an `f` before the quotes and enclosing variables in curly brackets `{}`.

**Why are we splitting IP addresses?**
Because `142.251.141.110` behaves as a single block of text. To categorize it mathematically or align it correctly as 4 "octets", we must fracture the string into pieces using the separator `.`.

**How do you align outputs?**
Inside the f-string curly braces, you add formatting constraints like `:^15` (center, 15 characters wide), `:>15` (right-aligned), or `:<15` (left-aligned).

**What if I try to divide an IPv6 address?**
Since IPv6 addresses use colons (`:`), you must change your split command to `ip_addr.split(":")`.

#### Code Example: `f_strings.py`

```python
#!/usr/bin/env python
from rich import print

ip_addr = "142.251.141.110"
fields = ip_addr.split(".")
print(fields)

octet1, octet2, octet3, octet4 = fields

# f-string 15-wide columns (left-aligned by default)
print()
print(f"|{octet1:15}|{octet2:15}|{octet3:15}|{octet4:15}|")

# f-string 15-wide columns (right-aligned)
print()
print(f"|{octet1:>15}|{octet2:>15}|{octet3:>15}|{octet4:>15}|")

# f-string 15-wide columns (centered)
print()
print(f"|{octet1:^15}|{octet2:^15}|{octet3:^15}|{octet4:^15}|")

# Variable display trick
print()
print(f"{octet1=}")

# f-string expressions get evaluated
print()
var1 = 22
var2 = 42
print(f"Variable sum: {var1 + var2}")
```

#### Line-by-Line Breakdown
- **`fields = ip_addr.split(".")`**: The `.split()` method creates a Python List separated by every dot.
- **`octet1, octet2, octet3, octet4 = fields`**: This is called "Tuple Unpacking." We instantly dump the 4 segments of the generated list into 4 named variables.
- **`print(f"|{octet1:^15}|...")`**: Evaluates variables inline formatting tables perfectly centered over 15 terminal column spaces.
- **`{octet1=}`**: Netmiko scripters use this debugging hack frequently. It outputs the exact variable name and its value (e.g., `octet1=142`).

---

### 2.2.2 Unicode Handling

#### Deep Dive Q&A
**What is Unicode?**
Unicode is an IT standard for encoding characters. 

**Why does this matter?**
If you automate against European network devices, switch banners or interface descriptions might contain characters outside standard ASCII (like the German umlaut). 

**How do we parse this?**
In Python, unicode literals are written using `\\u` followed by hexadecimal digits.

**What if the terminal doesn't support the character?**
Terminal fonts missing the specific unicode glyph will usually display an empty box `[]` or a `?`.

#### Code Example: `unicode_chars.py`

```python
#!/usr/bin/env python
from rich import print

print("\\u00e4") # ä
print("\\u00c4") # Ä
```

---

## 2.3 Comprehensive String Exercise

It is time to build muscle memory. Write this script using everything you've just learned.

### Objective
1. Take the base network `198.51.100.0/24`. Strip the mask away.
2. Subdivide the IPv4 address into octets.
3. Print an F-string table with 4 columns dynamically.
4. Attempt the exact same progression with IPv6 `2001:db8:1:1::/64` splitting on the `:` delimiter.

#### Deep Dive Q&A
**Why do you multiply a string `divider = "-" * 15`?**
Instead of manually typing `---------------`, Python easily generates repetitive strings mathematically. This matches the exact 15 column width we declare in our f-string!

**Why does the script use a junk variable `_`?**
When performing `start_ipv6_network, _ = ipv6_network.split("::")`, the user deliberately discards the right side of the split (the `::` ending payload sequence) because it serves no programmatic purpose later.

#### Exercise Solution: `strings_ex1.py`

```python
#!/usr/bin/env python
from rich import print

ip_address = "198.51.100.0/24"
ipv6_address = "2001:db8:1:1::/64"

# Divide the network from the mask
ipv4_network, ipv4_mask = ip_address.split("/")

# Obtain the octets
octet1, octet2, octet3, octet4 = ipv4_network.split(".")

divider = "-" * 15
top_string = "String Exercise1, part-1 (IPv4 .split())"
top_divider = "-" * len(top_string)
print("\\n" + top_string)
print(top_divider)
print(f"IPv4 Network: {ipv4_network}")
print(f"IPv4 Mask: {ipv4_mask}\\n")

print(f"{'octet1':^15} {'octet2':^15} {'octet3':^15} {'octet4':^15}")
print(f"{divider:15} {divider:15} {divider:15} {divider:15}")
print(f"{octet1:^15} {octet2:^15} {octet3:^15} {octet4:^15}")

# Divide the network from the mask (IPv6)
ipv6_network, ipv6_mask = ipv6_address.split("/")

# Obtain the hextets
# _ indicates a junk variable (i.e. just discarded)
start_ipv6_network, _ = ipv6_network.split("::")

# Hard-coded length, in practice would (probably) use a list
hextet1, hextet2, hextet3, hextet4 = start_ipv6_network.split(":")

top_string = "String Exercise1, part-2 (IPv6 .split())"
top_divider = "-" * len(top_string)
print("\\n\\n" + top_string)
print(top_divider)
print(f"IPv6 Network: {ipv6_network}")
print(f"IPv6 Mask: {ipv6_mask}\\n")
print(f"{'hextet1':^15} {'hextet2':^15} {'hextet3':^15} {'hextet4':^15}")
print(f"{divider:15} {divider:15} {divider:15} {divider:15}")
print(f"{hextet1:^15} {hextet2:^15} {hextet3:^15} {hextet4:^15}")
```

#### Line-by-Line Breakdown
- **`ipv4_network, ipv4_mask = ip_address.split("/")`**: Separates the host structure from the subnet bitmask mask exactly once at the CIDR notation.
- **`top_divider = "-" * len(top_string)`**: Dynamically maps the length of the Title and builds a horizontal line identical in size.
- **`start_ipv6_network, _ = ipv6_network.split("::")`**: IPv6 addresses are extremely messy for text parsing. This first split aggressively removes the entire trailing empty space block so that we are left with the primary `2001:db8:1:1` block.
- **`hextet1, hextet2... = start_ipv6_network.split(":")`**: Then it splits normal single colons generating four perfectly intact variables.
