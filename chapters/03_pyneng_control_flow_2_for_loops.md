# Chapter 3: Control Flow (Part 2: For Loops)

When you ask an API for an inventory of its routers, it doesn't give you one. It gives you fifties, hundreds, or thousands configured into a massive List. We use `for` loops to iterate through that list automatically, dealing with each router one by one.

---

## Section 3.5: Iterating over Lists (`loop_ex1.py` & `loop_ex2.py`)

A `for` loop grabs the first item in a List, assigns it to a temporary variable, runs the indented code block, and then loops back up to grab the next item automatically.

### Deep Dive Q&A
**What is `loop_var`?**
When scanning `for loop_var in my_list:`, `loop_var` dynamically holds the value of whatever iteration the loop is currently on. You can name this anything you want! `for router in my_list:` or `for ip in my_list:` works exactly the same.

**Why does `loop_ex2.py` print brackets like `[0]` and `[-1]` inside the loop?**
Because `loop_var` temporarily holds a String on every iteration, and Strings can be sliced exactly like Lists! `[0]` pulls the first letter of the word, `[-1]` pulls the final letter.

### Code Example

```python
#!/usr/bin/env python
from rich import print

my_list = ["hello", "world", "something", "else"]

print("\\n--- Basic Loop ---")
for loop_var in my_list:
    print(loop_var)

print("\\n--- Indexed Loops ---")
for loop_var in my_list:
    print(loop_var)
    # Print the first letter
    print(loop_var[0])
    # Print the last letter
    print(loop_var[-1])
```

---

## Section 3.6: Controlling the Loop (`break` and `continue`)

We don't always want a loop to finish. If we are searching a list of 5,000 MAC addresses to find our stolen laptop, once we find it at index 4, there is no reason to check the remaining 4,996 elements.

### Deep Dive Q&A
**What does `break` do?**
The `break` keyword (`loop_ex3.py`) instantly shatters the loop. The loop terminates completely and your script moves onto whatever code exists underneath the iteration block.

**What does `continue` do?**
The `continue` keyword (`loop_ex4.py`) abandons *only the current line item iteration*. It forcibly kicks Python back to the top of the `for` loop to grab the *next* item. It skips the current cycle, but keeps the loop alive.

### Code Example (`loop_ex3.py` & `loop_ex4.py`)

```python
#!/usr/bin/env python
from rich import print

my_list = ["hello", "world", "something", "else"]

print("\\n--- Testing Break ---")
for loop_var in my_list:
    if loop_var == "something":
        print("\\n\\nAll done!\\n")
        break
    print(loop_var)
    print("...still in the loop")

print("\\n--- Testing Continue ---")
for loop_var in my_list:
    if loop_var == "something":
        print("<skip>")
        continue
    print(loop_var)
    print("...still in the loop")
```

#### Line-by-Line Breakdown
- **`if loop_var == "something": continue`**: When the loop reaches "something", it hits `continue`. The print statement directly under it (`...still in the loop`) is bypassed completely.

---

## Section 3.7: Enumeration and Dictionaries

Sometimes we need to know the mathematical index of where we are in a list. Other times, we aren't looping over lists at all—we are looping over Dictionaries!

### Deep Dive Q&A
**What is `enumerate()`?**
By wrapping a List in `enumerate(my_list)` in `loop_ex5.py`, Python pumps out *two* variables per cycle. The first is an aggressive numerical counter (0, 1, 2, 3...), and the second is the actual item from the list.

**How do you loop over a Dictionary (`loop_ex6.py`)?**
Dictionaries contain Keys and Values. 
- `for k in my_dict.keys():` gives you simply the key names.
- `for v in my_dict.values():` gives you the raw data.
- **Critical:** `for key, value in dict.items():` gives you both cleanly!

### Code Example (`loop_ex5.py` and `loop_ex6.py`)

```python
#!/usr/bin/env python
from rich import print

print("\\n--- Enumerate ---")
my_list = ["hello", "world", "something", "else"]
for idx, loop_var in enumerate(my_list):
    print(f"{idx} --> {loop_var}")

print("\\n--- Looping over Dictionary ---")
ftp_service = {
    "uid": "97aeb3d0-9aea-11d5-bd16-0090272ccb30",
    "name": "ftp",
    "port": "21",
}

for k, v in ftp_service.items():
    print(f"{k} -> {v}")
```

#### Line-by-Line Breakdown
- **`for idx, loop_var in enumerate(my_list):`**: Captures index `0` and value `"hello"`.
- **`for k, v in ftp_service.items():`**: Extracts precisely both sides of the dictionary's colon mapping.

---

## 3.8 Comprehensive For Loop Exercises

### Objective
1. Standard Iteration: Loop over a list of firewalls, printing them.
2. Flow Control: Iterate over `pod1-gaia` through `pod99-gaia`. If you hit `pod4`, skip it (`continue`). If you hit `pod98`, kill the loop (`break`).
3. Enumeration: Print out the specific sequence indexes of every firewall.

### Exercise Solutions (`loops_ex1.py` - `loops_ex3.py`)

```python
#!/usr/bin/env python
from rich import print

my_firewalls = [
    "pod1-gaia", "pod2-gaia", "pod3-gaia", 
    "pod4-gaia", "pod5-gaia", "pod98-gaia", "pod99-gaia"
]

print("\\n--- Exercise 1: Standard Search ---")
for fw in my_firewalls:
    if fw == "pod5-gaia":
        print(f"Connecting to fw: {fw}")

print("\\n--- Exercise 2: Continue and Break ---")
for fw in my_firewalls:
    if fw == "pod4-gaia":
        continue
    if fw == "pod98-gaia":
        break
    print(f"Processing {fw}")

print("\\n--- Exercise 3: Enumerate ---")
for idx, fw in enumerate(my_firewalls):
    print(f"{idx} -> {fw}")
```

Conditionals and For Loops drive 95% of automation logic. In Part 3 of this chapter, we will finish our loop coverage with `While` loops and dive deeply into Python's `try/except` Crash Management engine.
