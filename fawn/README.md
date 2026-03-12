# Hack The Box – Fawn Walkthrough | ZeroToRoot Labs

Difficulty: Very Easy  
Platform: Hack The Box  
YouTube Tutorial: https://youtu.be/ng4uYETrzuw

This machine demonstrates how anonymous FTP access can expose sensitive files.

---

# Step 0 – Connect to Hack The Box VPN

Before interacting with the machine we must connect to the Hack The Box VPN.

Download the VPN configuration file from the Hack The Box portal. If you already have .ovpn file downloaded, navigate to the folders its downloaded and run below.

Connect using OpenVPN.

Command:

sudo openvpn yourvpnfile.ovpn

Once connected we can access machines in the lab network.

---

# Step 1 – Spawn the Machine

Start the Fawn machine in Hack The Box and obtain the target IP address.

Example:

10.129.xx.xx

---

# Step 2 – Enumeration

The first step is to scan the target using Nmap.

Command:

nmap -sC -sV TARGET_IP

Explanation:

-sC → runs default scripts  
-sV → detects service versions  

---

# Step 3 – Scan Results

The scan reveals:

21/tcp → FTP

FTP stands for File Transfer Protocol and is used for transferring files between systems.

---

# Step 4 – Exploitation

We attempt to connect to the FTP service.

Command:

ftp TARGET_IP

When prompted for login credentials we try:

Username:

anonymous

Password:

anonymous

This works because the FTP server allows anonymous access.

---

# Step 5 – List Files

Once logged in we list files on the server.

Command:

ls

We discover a file containing the flag.

---

# Step 6 – Download the Flag

Use the get command to download the file.

Command:

get flag.txt

---

# Step 7 – Read the Flag

Display the flag using:

cat flag.txt

This confirms successful exploitation of the machine.

---

# Lessons Learned

- FTP is not a shell:
You cannot use cat inside ftp>.
You must get files and then use Linux tools (cat, grep, etc.) locally.

- Anonymous FTP is dangerous:
Anyone can log in and read files.
In real environments, this can expose sensitive data.

- Control vs data connection:
Errors like “No control connection” are related to FTP’s dual-connection design.
passive off can fix issues.

- Workflow pattern:

Enumerate → Identify FTP → Check anonymous → List files → Download → Analyse.


---

# Platform

Hack The Box
https://labs.hackthebox.com/achievement/machine/3230071/393
<img width="1157" height="748" alt="image" src="https://github.com/user-attachments/assets/52034a85-b228-4a1c-854c-796e8c8d30b9" />

---

# Disclaimer

This walkthrough is for educational purposes only and was performed on the Hack The Box training platform.
