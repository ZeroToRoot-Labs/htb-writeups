
# Hack The Box – Meow Walkthrough

Difficulty: Very Easy  
Platform: Hack The Box  

This write-up explains how the Meow machine was solved step-by-step.

---

# Step 0 – Connect to Hack The Box VPN

Before accessing any machine, we must connect to the Hack The Box VPN.

Download the VPN configuration file from the Hack The Box portal.

Then connect using OpenVPN.

Command:

sudo openvpn yourvpnfile.ovpn

After connecting, you will have access to the Hack The Box lab network.

---

# Step 1 – Identify the Target Machine

After spawning the machine, we receive an IP address.

Example:

10.129.xx.xx

This will be the target for scanning.

---

# Step 2 – Enumeration

The first step in penetration testing is enumeration.

We scan the target using Nmap.

Command:

nmap -sC -sV TARGET_IP

Explanation:

-sC → runs default scripts  
-sV → detects service versions  

This scan identifies open ports and services.

---

# Step 3 – Scan Results

The scan reveals the following open port:

23/tcp → Telnet

Telnet allows remote command-line login.

---

# Step 4 – Exploitation

Since Telnet is open, we attempt to connect.

Command:

telnet TARGET_IP

When prompted for login, we try:

root

This grants access to the machine.

---

# Step 5 – Capture the Flag

Once logged in, we list files.

Command:

ls

Then read the flag.

Command:

cat flag.txt

The flag confirms the machine has been successfully compromised.

---

# Lessons Learned

• Enumeration is the most important step  
• Exposed Telnet services are insecure  
• Weak authentication can lead to full system compromise

---

# Meow Completion Badge

https://labs.hackthebox.com/achievement/machine/3230071/394
<img width="1167" height="748" alt="image" src="https://github.com/user-attachments/assets/647f4c84-5e47-40fe-b6ba-f1498f5f7cc4" />

---
# Platform

Hack The Box

---

# Disclaimer

All actions performed in this walkthrough were done on the Hack The Box training platform for educational purposes.
