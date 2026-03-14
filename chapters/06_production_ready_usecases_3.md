# Chapter 6: Production-Ready Use Cases (Part 3)

The grand finale of our automation journey involves the two most impactful automation scripts: Zero-touch Image Upgrades and Comprehensive Device Health Validation.

---

## Use Case 5: Automated Software/Firmware Upgrade (IOS-XE)

To upgrade a device, you must copy the new image over the network, verify the boot variables, and reload the device. Doing this manually for 100 switches is mind-numbing. Netmiko has a built-in `file_transfer` class specifically to handle SCP operations.

### Code Example: `ios_xe_upgrade.py`

*Prerequisite: `ip scp server enable` must be running on the Cisco device.*

```python
from getpass import getpass
from netmiko import ConnectHandler, file_transfer
from rich import print

password = getpass()

device = {
    "device_type": "cisco_ios",
    "host": "10.1.1.1",
    "username": "admin",
    "password": password,
    "global_delay_factor": 2, # File transfers can lock the CPU, adding global delay guarantees stability
}

source_file = "c880data-universalk9-mz.155-3.M8.bin"
dest_file = "c880data-universalk9-mz.155-3.M8.bin"

with ConnectHandler(**device) as ssh_conn:
    print(f"Connected to {device['host']}. Checking for existing file...")

    # Step 1: Copy the file using Netmiko SCP
    transfer_dict = file_transfer(
        ssh_conn,
        source_file=source_file,
        dest_file=dest_file,
        file_system="flash:",
        direction="put",
        overwrite_file=True,
    )
    
    if transfer_dict["file_exists"]:
        print("File transferred successfully. Checking MD5 hash...")
        # Step 2: Verify MD5 Integrity (Netmiko does this natively under the hood in file_transfer, but here is manual logic if needed)
        if transfer_dict["file_verified"]:
            print("File verified. Modifying Boot Variable...")
            
            # Step 3: Change boot variable and save
            ssh_conn.send_config_set([
                "no boot system",
                f"boot system flash:{dest_file}"
            ])
            ssh_conn.save_config()
            
            print("Upgraded successfully! Ready for Reload.")
        else:
             print("CRITICAL: File MD5 mismatch. Aborting.")
    else:
        print("CRITICAL: File Transfer Failed.")
```

### Script Breakdown
- **`from netmiko import file_transfer`**: This is a dedicated class. It handles SCP natively, verifies there is enough space on the flash drive, transfers the file, and then (crucially) verifies the MD5 hash checksum on the destination router automatically!
- **`global_delay_factor: 2`**: Flash drives on routers are notoriously slow. By passing `global_delay_factor`, we literally slow down Netmiko's aggressive polling mechanics by a factor of 2x so it doesn't accidentally time out waiting for the switch's CPU to catch up.

---

## Use Case 6: Network Testing & Health Check

You've upgraded the device. Has it come back online correctly? Is BGP up? Is the CPU healthy? We combine Genie Parsing, loops, and ping validation to build a comprehensive Health Check.

### Code Example: `health_validator.py`

```python
import json
from getpass import getpass
from netmiko import ConnectHandler
from rich import print

password = getpass()
device = {
    "device_type": "cisco_ios",
    "host": "cisco-core.lasthop.io",
    "username": "admin",
    "password": password,
}

with ConnectHandler(**device) as nc:
    print(f"\\n--- Initiating Health Check on {device['host']} ---")

    # 1. CPU & RAM (Regex string validation as Genie might not support all older CPUs)
    cpu_output = nc.send_command("show processes cpu sorted | include CPU")
    print(f"CPU Status: {cpu_output.strip()}")

    # 2. Interface Status using TextFSM/Genie
    interfaces = nc.send_command("show ip interface brief", use_genie=True)
    if interfaces:
        down_ints = [intf for intf, data in interfaces["interface"].items() if data['status'] == 'down']
        print(f"Interfaces Down: {down_ints if down_ints else 'None. All Ports healthy!'}")
        
    # 3. OSPF Neighbors
    ospf_neighbors = nc.send_command("show ip ospf neighbor", use_genie=True)
    try:
        nbr_count = len(ospf_neighbors.get('interfaces', {}))
        print(f"Active OSPF Adjacencies: {nbr_count}")
    except Exception:
        print("OSPF: No adjacencies detected.")

    # 4. Check reachability via Ping
    target_ip = "8.8.8.8"
    ping_result = nc.send_command(f"ping {target_ip}")
    if "!" in ping_result:
        print(f"Dataplane Reachability: SUCCESS (Pinged {target_ip})")
    else:
        print(f"Dataplane Reachability: FAILED.")

    print("--- Health Check Complete ---\\n")
```

### Script Breakdown
- **`nc.send_command("show ... use_genie=True")`**: Because Genie converts the entire `show ip interface brief` table into a dictionary, we can use a Python List Comprehension `[intf for intf, data in interfaces["interface"].items() if data['status'] == 'down']` to instantly pull back exactly which access ports are down without writing 50 lines of string manipulation logic.
- **`if "!" in ping_result:`**: Cisco routers output `!` for a successful ICMP echo reply and `.` for a timeout. A simple string `in` check validates dataplane health natively.

---

### Conclusion

Congratulations! You have journeyed from typing `"Hello World"` to dynamically transferring firmware files across the country using python scripting. By mastering strings, lists, dictionaries, conditionals, loops, and Netmiko, you are now equipped to tackle nearly any project in Network Automation!
