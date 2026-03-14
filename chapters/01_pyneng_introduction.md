# Chapter 1: Introduction to Python for Network Automation

Welcome to Part 1: Comprehensive Python Introduction of "Learn Python and Network Automation - The Complete Practical Guide". 

Drawing heavily from the theoretical foundations of the *Python for Network Engineers (pyneng)* methodology, we couple those concepts with the practical, executable code examples from the Twin Bridges `python_course_mar26`.

Network automation requires moving away from the Command Line Interface (CLI) and treating infrastructure as code. To do this, we must build muscle memory: open up your terminal, create files matching our lessons, type out the code, and execute it. 

## Writing Your First Script

In network automation, you often create scripts consisting of multiple Python commands to run collectively. Let's look at the foundational script from `class1/python_script/my_script.py`.

### Deep Dive Q&A

**What is a Python script?**
A Python script is a simple text file containing a sequence of Python commands. Instead of typing commands one by one interactively, the script runs them all from top to bottom.

**Why use a script instead of the interactive shell?**
While the interactive shell (REPL) is great for testing quick one-liners (like verifying how a regex pattern matches an interface name), scripts are saved permanently. You write a script to back up 500 routers once, and you can run it every night forever. 

**How do we execute it?**
You invoke the Python interpreter from your operating system's terminal, passing the script name as an argument: `python my_script.py`.

**What if the script doesn't run or says "Command not found"?**
This usually means Python is not installed, or your operating system's PATH variable doesn't know where the `python` executable lives. On Linux/Mac, you might need to type `python3` instead of `python`.

---

### Code Example: `my_script.py`

This is the exact script from `python_course_mar26/class1/python_script/my_script.py`.

```python
#!/usr/bin/env python
print("Hello world")
```

### Line-by-Line Breakdown

- **`#!/usr/bin/env python`**: This line is referred to as a "shebang" line. In UNIX/Linux based environments (which most Network Automation platforms like Ansible/Ubuntu run on), it dictates which interpreter is responsible for executing the script. Using `/usr/bin/env python` dynamically searches the current user's environment for an active Python executable. This is exceptionally helpful if you use a Python Virtual Environment.
- **`print("Hello world")`**: Here we are using a built-in Python function named `print()`. It acts as the standard output stream for your code, taking the argument passed to it (the string `"Hello world"`) and displaying it on your command line terminal.

### Executing the Script

Make the script executable and run it using the `python` interpreter on your terminal:

```bash
$ python my_script.py
Hello world
```

With this foundational ability to execute saved code, we can move rapidly to networking concepts. In the next chapter, we will dive into Data Types—specifically covering how to slice, parse, and format IP addresses using Strings, Lists, and Dictionaries.
