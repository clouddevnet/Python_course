# Chapter 3: Control Flow (Part 3: While Loops)

While `for` loops iterate a specific predetermined number of times (based on the exact length of the list), `while` loops execute continuously *until a specific condition becomes False*. 

In Network Automation, `while` loops are most commonly used for **polling**. If you reboot a router, you want your script to ping it every 10 seconds until it finally responds. You don't know exactly how many pings it will take, so a `while` loop is perfect.

---

## Section 3.9: Basic Time Polling (`while_ex1.py`)

Python's built-in `time` module combined with a `while` loop allows you to build a countdown timer dynamically.

### Deep Dive Q&A
**What is `time.time()` doing?**
It returns the current time in seconds since the Epoch (January 1, 1970). Every time you call it, the number is larger.

**How does the condition mathematically prevent the loop from running forever?**
The variable `WAIT_TIME` is set to 6. `start_time` captures a static snapshot of the clock exactly once before the loop starts. As the loop spins, Python subtracts the `start_time` from the constantly growing `time.time()`. When the difference exceeds 6 seconds, the `<` less-than conditional evaluates to `False`, and the loop shatters.

**What is `time.sleep(1)`?**
This tells the script to pause all execution for exactly 1 second. Without this delay mapping, your script might iterate the `while` loop a million times in 6 seconds, redlining your computer's CPU!

### Code Example: `while_ex1.py`

```python
#!/usr/bin/env python
import ipdb  # noqa
import time
from rich import print

WAIT_TIME = 6

print()
start_time = time.time()
while time.time() - start_time < WAIT_TIME:
    print(time.time() - start_time)
    time.sleep(1)
    print("In loop...")

print("\\nLoop over")
```

---

## Section 3.10: The Infinite Loop Pattern (`while_ex2.py`)

A massive majority of deployed networking scripts do *not* put the mathematical check in the `while` definition. Instead, they use `while True:`, which explicitly guarantees the loop will run forever, and then use `if/break` internally to escape.

### Deep Dive Q&A
**Why use `while True:`?**
It is considered standard architectural patterning in Python (sometimes called the "Loop-and-a-half" pattern). It cleanly separates the *action* you want to perform in the loop from the *condition* required to escape the loop. It often makes the code considerably easier to read.

### Code Example: `while_ex2.py`

```python
#!/usr/bin/env python
import ipdb  # noqa
import time
from rich import print

WAIT_TIME = 6

print()
start_time = time.time()
while True:
    print("In loop...")
    time.sleep(1)
    cur_time = time.time()
    
    # The Escape Hatch
    if (cur_time - start_time) > WAIT_TIME:
        break

print("\\nLoop over")
```

---

## Section 3.11: Truthiness Polling (`while_ex3.py`)

Applying concepts from Chapter 2, we can configure our `while` loops to evaluate the Truthiness of normal variables, rather than numbers.

### Deep Dive Q&A
**Why does `while check_var1:` work?**
Because `check_var1` contains `"some string"`. Non-empty Strings possess a boolean truthiness of `True`. This is functionally identical to saying `while True:`.

**Why does `if not check_var2:` break the loop?**
`check_var2` is an empty string `""`. Empty strings evaluate to `False`. 
The `not` operator instantly flips a boolean. It sees `False`, flips it to `True`, which activates the `if` block, triggering the `break`.

### Code Example: `while_ex3.py`

```python
#!/usr/bin/env python
import ipdb  # noqa
import time
from rich import print

WAIT_TIME = 6

print()
check_var1 = "some string"
check_var2 = ""
while check_var1:
    print("In loop...")
    time.sleep(1)

    if not check_var2:
        break

print("\\nLoop over")
```

---

## 3.12 Comprehensive While Loop Exercise

### Objective
1. Establish a polling loop that runs continuously.
2. Inside the loop, measure current execution time.
3. If elapsed time is less than limits (8 seconds), sleep for 1 second.
4. Once the limit is breached, trigger an `else` block containing a `break` to escape gracefully.

### Exercise Solution:

```python
#!/usr/bin/env python
from rich import print
import time

WAIT_TIME = 8

start_time = time.time()
while True:
    cur_time = time.time()
    if cur_time - start_time < WAIT_TIME:
        print("Sleeping 1s")
        time.sleep(1)
    else:
        print("All done...")
        break
```

In the final portion of Chapter 3, we will investigate Python Exceptions (`try/except`), providing armor for our scripts to prevent them from catastrophically crashing when routers inevitably lose connections halfway through a job.
