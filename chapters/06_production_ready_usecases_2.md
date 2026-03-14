# Chapter 6: Production-Ready Use Cases (Part 2)

We continue our Capstone project by looking into dynamic change verification. One of the highest sources of network downtime is poorly executed maintenance windows and configuration drift. Automation mitigates these risks perfectly.

---

## Use Case 3: Golden Template Comparison

When you control dozens (or hundreds) of identical edge switches, their base configuration (NTP, Syslog, SNMP, VTY lines) should be totally uniform. This script pulls the configuration of a device and explicitly diffs it against a "Golden" text file to identify undocumented changes. 

### Code Example: `golden_template_diff.py`

```python
import difflib
from getpass import getpass
from netmiko import ConnectHandler
from rich import print

password = getpass()

device = {
    "device_type": "cisco_ios",
    "host": "10.1.1.1",
    "username": "admin",
    "password": password,
}

# The expected 'Golden' configuration
with open("golden_config.txt") as f:
    golden_config = f.read().splitlines()

with ConnectHandler(**device) as net_connect:
    print(f"Connected to {device['host']}")
    
    # Send show run and split lines to create a list of strings
    running_config = net_connect.send_command("show run").splitlines()

# Use built-in difflib to compare 
diff = difflib.unified_diff(
    golden_config, 
    running_config, 
    fromfile='golden_config', 
    tofile='running_config',
    lineterm=''
)

# Output only the lines that differ
delta_found = False
for line in diff:
    delta_found = True
    if line.startswith("+") and not line.startswith("+++"):
        print(f"[green]{line}[/green]") # Addition to running
    elif line.startswith("-") and not line.startswith("---"):
        print(f"[red]{line}[/red]")     # Missing from running

if not delta_found:
    print("Configuration matches Golden Template 100%.")
```

### Script Breakdown
- **`difflib.unified_diff`**: A powerful built-in Python library for comparing sequences. Passing it two lists (the golden text and the live output) generates a diff exactly like you would see in `git`. 
- **`print(f"[green]{line}[/green]")`**: Taking advantage of the `rich` library we learned in Chapter 2, we dynamically color-code the console output. Lines missing from the switch show as Red, unexpected additions show up as Green!

---

## Use Case 4: Pre and Post Change Window Comparison

During a change window (like an upgrade or failover event), engineers run a series of `show` commands beforehand, make the change, and run them again afterward to verify they didn't break anything. We can automate this exact flow.

Instead of parsing raw text with Regex, the most scalable method is to coerce the router into returning **structured JSON** using the TextFSM / Genie parsers built directly into Netmiko!

### Code Example: `pre_post_check.py`

This script uses the `use_genie` flag to natively parse the `show ip route` table into a structured Dictionary. 

*Prerequisite: In your python environment, must run `pip install pyats genie` first.*

```python
import json
from getpass import getpass
from netmiko import ConnectHandler
from rich import print

password = getpass("Enter password: ")

device = {
    "device_type": "cisco_ios",
    "host": "cisco3.lasthop.io",
    "username": "pyclass",
    "password": password,
}

with ConnectHandler(**device) as net_connect:
    print(f"Logged into {net_connect.host} for PRE-CHECK")
    
    # PRE-CHECK: The output is NOT text! It natively returns a parsed Python Dictionary!
    pre_routing = net_connect.send_command("show ip route", use_genie=True)
    
    # Ensure there's a default route present natively checking keys.
    default_pre = pre_routing.get("vrf", {}).get("default", {}).get("address_family", {}).get("ipv4", {}).get("routes", {}).get("0.0.0.0/0")
    
    if not default_pre:
        print("CRITICAL: No default route in pre-check. Aborting maintenance.")
        exit()
        
    print("Pre-check validated.")
    
    input("Make your changes now! Press Enter to execute Post-Check...")
    
    # POST-CHECK
    post_routing = net_connect.send_command("show ip route", use_genie=True)
    default_post = post_routing.get("vrf", {}).get("default", {}).get("address_family", {}).get("ipv4", {}).get("routes", {}).get("0.0.0.0/0")

    if pre_routing == post_routing:
       print("SUCCESS: Routing table matches exactly.")
    else:
       print("WARNING: Routing table drift detected!")
```

### Script Breakdown
- **`use_genie=True`**: This flag activates Cisco's pyATS/Genie library engine inside Netmiko. It catches the unstructured text output from `show ip route` and translates it directly into nested Python Dictionaries automatically.
- **`.get()`**: Instead of hard-accessing a dictionary key (which throws a `KeyError` if it doesn't exist, as we saw in Chapter 3), using `.get(key, default_value)` safely attempts to extract the key. If it's missing, it returns an empty dictionary `{}` which safely chains. 

In the final section of our Capstone, we will push automated configurations to a device, update system imaging, and integrate comprehensive health validations.
