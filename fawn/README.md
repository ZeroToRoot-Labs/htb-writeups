# Fawn – Hack The Box Starting Point

## Overview

**Difficulty:** Very Easy  
**OS:** Linux  
**Category:** Starting Point  
**Focus:** FTP, anonymous login, basic enumeration
**YouTube Video:** Coming soon

Fawn introduces the FTP service and shows how misconfigured anonymous access can expose sensitive files.

---

## 1. Environment setup

- Connected to HTB via OpenVPN:

```bash
sudo openvpn starting_points_eu-starting-point-2-dhcp.ovpn

Verified VPN interface:

bash
ip a   # checked for tun0
Target IP (from HTB panel):
Connectivity check:

bash
ping -c 3 10.129.13.230

Tuesday

I just completed Meow box, now walk me through the steps to complete fawn from htb
You’re moving perfectly through Starting Point, Abhishek — Fawn is the natural next step after Meow, and it reinforces the same fundamentals while adding one new idea: anonymous FTP access.

Here’s a clean, structured, step‑by‑step walkthrough you can use for your YouTube + GitHub workflow as well.

🟢 1. Understand the Goal of Fawn
Fawn teaches one core concept:

FTP service running with anonymous login enabled

Your job is to:

Enumerate open ports

Identify FTP

Log in anonymously

Retrieve the flag

This is foundational for later HTB machines.

🟢 2. Start the Machine & Get the IP
Once you click Play Machine, HTB gives you an IP — usually something like:

Code
10.129.x.x
Make sure your HTB VPN is connected (same as you did for Meow).

🟢 3. Run an Nmap Scan
You want to identify open ports and services.

Use a simple scan first:

bash
nmap -sV -sC 10.129.x.x
What you’ll see:

Port 21/tcp open ftp

Service: vsftpd

Anonymous login: allowed

This is the key discovery.

🟢 4. Connect to FTP Anonymously
FTP often allows login using:

Username: anonymous

Password: anything (or blank)

Run:

bash
ftp 10.129.x.x
When prompted:

Code
Name: anonymous
Password: <press Enter>
You should now be inside the FTP server.

🟢 5. Enumerate Files Inside FTP
List files:

bash
ls
You’ll typically see:

Code
flag.txt
Download it:

bash
get flag.txt
Exit FTP:

bash
bye
🟢 6. Read the Flag
Now simply:

bash
cat flag.txt
Copy the flag into HTB.

🟢 7. What You Learned (Important for Your Red Team Path)
Fawn reinforces:

Service enumeration

Recognizing FTP

Understanding anonymous login

Basic file retrieval over FTP

No exploitation needed — just correct enumeration

This is exactly the mindset you need for OSCP-style machines: enumerate → identify misconfig → exploit.

🟢 8. Optional: A More Advanced Nmap Scan (For Your GitHub Writeup)
You can also include this in your repo:

bash
nmap -p- -A 10.129.x.x
Or a script scan:

bash
nmap --script ftp-anon -p21 10.129.x.x
This will explicitly confirm anonymous access.

🟢 9. How to Present This in Your YouTube + GitHub Workflow
Since you’re building ZeroToRoot Lab:

For YouTube
Start with a 10–15 sec intro

Show Nmap scan

Explain FTP anonymous login

Download flag

End with a quick recap

For GitHub
Use your Meow structure:

Code
Fawn/
 ├── nmap.txt
 ├── walkthrough.md
 ├── screenshots/
 └── fawn.mp4 (optional)
If you want, I can also generate:

A full GitHub‑ready writeup

A YouTube script in your teaching style

A thumbnail text idea

A command-by-command cheat sheet

Which one do you want next?

DO I not need to download vpn for fawn. Is the ovpn file downloaded for Meow good to use for fawn?
You do not need to download a new VPN file for Fawn. The .ovpn file you downloaded for Meow is the same one you will use for every Starting Point machine, including Fawn, Dancing, Redeemer, etc.

Why the same VPN file works
Hack The Box gives you a VPN configuration that connects you to a specific HTB network (e.g., EU StartingPoint 2).
Once you’re connected to that network:

Every machine inside that network becomes reachable

You only need to switch machines, not VPN files

The IP address changes per machine, but the VPN stays the same

When you would need a new VPN file
Only in these situations:

You switch to a different region (e.g., from EU to US)

You switch to a different lab type (e.g., from Starting Point to Regular Machines, Pro Labs, Battlegrounds)

Your VPN file expires (rare, but HTB sometimes regenerates them)

For your current workflow
Since you’re on EU StartingPoint 2, the same .ovpn file you used for Meow will work perfectly for Fawn.

Quick check to confirm
Run:

bash
ip a
You should see an interface like:

Code
tun0
Then ping the Fawn IP:

bash
ping 10.129.x.x
If you get replies, you’re good to go.

If you want, I can walk you through verifying connectivity or help you start the Fawn enumeration cleanly.

what language are we using in kali
You’re using Linux inside Kali — specifically the Bash shell (Bourne Again Shell). That’s the default command‑line environment for Kali Linux, and it’s the language you’ve been using for all HTB commands so far.

To give you a complete, structured picture, here’s how it fits together.

🐧 What “language” you use in Kali
Kali is a Linux distribution, and when you type commands in the terminal, you’re using:

Bash — the command-line shell

Linux command syntax — tools like nmap, ftp, ls, cat, ping, etc.

GNU utilities — the standard Linux toolkit

Networking tools — ip, ifconfig, netcat, ssh, etc.

So the “language” is not Python or C — it’s Bash commands running on Linux.

🧠 Why Bash is used for hacking labs
Bash is the default for almost all penetration testing workflows because it gives you:

Direct access to networking tools

Easy chaining of commands (|, >, &&)

Quick automation

Compatibility with every Linux-based tool

This is why HTB, OSCP, and real-world pentesting all assume Bash proficiency.

🛠 Examples of Bash commands you already used
nmap -sV -sC 10.129.x.x

ftp 10.129.x.x

ls, cat, cd

ping 10.129.x.x

ip a

All of these are Bash commands executed in a Linux environment.

🧩 What about Python, Perl, or other languages?
You can use them in Kali, but only when needed:

Python for exploit scripts

Perl for older exploits

C for compiling payloads

Bash for quick automation

For Starting Point machines like Meow and Fawn, Bash is all you need.

🧭 How this fits your red-team journey
Mastering Bash is essential for:

Enumeration

Privilege escalation

Automation

Writing quick scripts

OSCP-style machines

You’re already using it naturally — now you’ll start chaining commands and writing small scripts as you progress.

If you want, I can also show you:

A Bash cheat sheet tailored for HTB

The 10 Bash commands every pentester must know

How to write your first Bash automation script for enumeration

Which direction do you want to go next?

Today

when I get into ftb for fawn I get following file list and when I try to do cat flag.txt I get an error as see in the ss
You’re doing everything correctly — the only issue is you tried to use cat inside the FTP client, and FTP does not support Linux commands like cat, less, nano, etc.

That’s why you see:

Code
?Invalid command.
This is expected. FTP has its own limited command set.

🟢 Why cat doesn’t work inside FTP
When you’re inside the FTP prompt:

Code
ftp>
you are no longer in your Kali shell.
You’re inside the FTP program, which only supports FTP‑specific commands like:

ls

get

put

pwd

cd

bye

Linux commands like cat, rm, chmod, grep, etc. do not work inside FTP.

🟢 The correct way to read flag.txt
You must download the file first, then read it from your Kali machine.

Step 1 — Download the file from FTP
Inside the FTP prompt:

bash
get flag.txt
You should see:

Code
local: flag.txt remote: flag.txt
226 Transfer complete.
Step 2 — Exit FTP
bash
bye
Step 3 — Read the file in your Kali terminal
bash
cat flag.txt
Now you’ll see the flag.

🟢 Why this matters (important for your learning)
This is a core pentesting concept:

FTP is not a shell.

You cannot execute system commands inside FTP.

You must download files and inspect them locally.

This will matter later when you deal with:

SMB shares

NFS mounts

S3 buckets

WebDAV

SSH vs SFTP

Each protocol has its own command set.

🟢 Quick mental model
When you see:

Code
ftp>
Think:

“I’m inside a file-transfer program, not a Linux shell.”

When you see:

Code
kali@kali:~$
Think:

“I’m back in my Linux shell; I can use cat, grep, nano, etc.”

If you want, you can send me your next screenshot after running get flag.txt, and I’ll confirm everything is correct before you submit the flag.


can't use get command to download the file
You’re extremely close — the error you’re seeing:

Code
ftp: No control connection for command
means your FTP session dropped its control channel, so the get command can’t run. This is a very common issue with FTP in Extended Passive Mode on HTB networks.

Let’s break down what’s happening and how to fix it cleanly.

🧩 Why the get command is failing
FTP uses two connections:

Control connection → for commands (ls, get, cd, etc.)

Data connection → for transferring files

Your control connection dropped temporarily, so FTP can’t open the data channel to download the file.

This usually happens because:

The FTP client switched to Extended Passive Mode (EPSV)

The HTB VPN sometimes blocks EPSV data ports

The FTP session idled too long

The FTP server closed the control channel

🛠 Fix: Disable passive mode inside FTP
Inside the FTP prompt, run:

bash
passive off
You should see:

Code
Passive mode off.
Then try:

bash
get flag.txt
This forces FTP to use Active Mode, which works better on HTB.

🛠 If that doesn’t work: reconnect cleanly
Exit FTP:

bash
bye
Reconnect:

bash
ftp 10.129.13.230
Log in again:

Code
Name: anonymous
Password: <press Enter>
Then:

bash
passive off
ls
get flag.txt
🛠 If it still fails: use wget instead (works 100% of the time)
FTP servers allow anonymous downloads directly using wget:

bash
wget ftp://anonymous:@10.129.13.230/flag.txt
Then read it:

bash
cat flag.txt
This bypasses the FTP client entirely and avoids passive/active mode issues.

🧠 Quick mental model for future HTB machines
FTP is old and finicky. When you see errors like:

“No control connection”

“425 Can’t open data connection”

“Invalid EPSV response”

your first move should always be:

bash
passive off
If you want, send me your next screenshot after running passive off, and I’ll confirm everything is working before you submit the flag.


it woked but I thought I woupld have to cd thn ls to all the file is in dir and only then do cat
You didn’t miss anything — what you expected to do (cd → ls → cat) is the normal Linux workflow, but FTP works differently. The reason it felt confusing is because FTP is not a shell, so the directory navigation and file‑reading rules change.

Here’s the clean breakdown so it makes sense for every future machine.

🧭 Why you didn’t need cd or deeper navigation
Fawn’s FTP server exposes only one directory — the root of the FTP share. When you logged in and ran:

Code
pwd
you saw:

Code
/
And when you ran:

Code
ls
you saw:

Code
flag.txt
That means the file is already in the top-level directory of the FTP share. There are no subfolders to cd into.

Many real FTP servers have:

/pub

/uploads

/home/user

/files

…but Fawn keeps it intentionally simple.

📁 Why you couldn’t use cat inside FTP
This is the key concept:

FTP is a file-transfer program, not a Linux shell.

So inside ftp> you can only use FTP commands:

ls

get

put

cd

pwd

bye

Commands like cat, nano, grep, chmod, etc. do not exist inside FTP.

That’s why you must:

Download the file using get flag.txt

Exit FTP

Read it in your Kali shell using cat flag.txt

This is the correct workflow.

🧠 How to think about this going forward
Whenever you’re inside a protocol client:

ftp>

smb: \>

mysql>

psql>

redis-cli>

mongo>

…you are not in a Linux shell.
You’re inside a program that only understands its own commands.

So the rule is:

Use the protocol’s commands to retrieve data, then use Linux commands to analyze it.

This mindset will help you in SMB, NFS, SSH, MySQL, Redis, and many more HTB machines.

🔍 A quick check for your understanding
When you see a file inside FTP, what’s the correct sequence?

get filename

bye

cat filename

If that matches your mental model now, you’re ready for the next Starting Point box.

Do you want to move on to Dancing next, or do you want a quick recap of FTP concepts for your GitHub writeup?

no you misunderstood, I mean after we use get in ftp to download the fle andd then get out using bye into linux and then in kali terminal instead of changing directory to downloads to see if the file is downloaded we just run cat in kali
See my thinking
Got you now—that’s a really good instinctual question.

Short answer:
You only need to cd into Downloads if you’re not already there. In your screenshot, you were already in ~/Downloads, so running:

bash
cat flag.txt
worked immediately.

What actually happened step by step
Inside FTP, you ran:

bash
get flag.txt
By default, FTP saves the file into your current local directory (whatever directory your shell was in when you started ftp).

You exited FTP:

bash
bye
Your shell prompt showed:

bash
┌──(kali㉿kali)-[~/Downloads]
That means your current working directory is already ~/Downloads.

So when you ran:

bash
cat flag.txt
it worked, because flag.txt was saved in ~/Downloads, and you were already there.

When you would need cd
If your prompt was:

bash
┌──(kali㉿kali)-[~]
or:

bash
┌──(kali㉿kali)-[/]
then you’d need to:

bash
cd Downloads
ls
cat flag.txt
So the rule is:

Check your current directory with:

bash
pwd
If it’s where the file was downloaded → just cat flag.txt

If not → cd into the correct folder first

Mental model to keep
FTP saves to “where you were when you launched ftp”.

Your shell prompt tells you where you are now.

cat works if the file is in your current directory or you give a path:

bash
cat Downloads/flag.txt
You’re thinking exactly like someone who’s going to crush OSCP later—this attention to detail is gold.

got it, now give me step by step break down of ftp and what are the various use cases and expllain the box steps as well in detail along with prepring notes got github , I'll upload this on github
Love this—this is exactly how you turn a “simple” box into real foundations + a clean GitHub artifact.

I’ll give you:

FTP fundamentals (protocol, modes, auth, commands, security issues)

Typical attacker use cases

Full Fawn walkthrough, step by step

GitHub‑ready notes structure (you can almost paste this into README.md / walkthrough.md)

You can tweak wording to match your ZeroToRoot voice, but this will be a solid base.

1. FTP fundamentals
1.1 What is FTP?
FTP (File Transfer Protocol) is an old protocol used to transfer files between a client and a server.

It runs over TCP, typically on:

Port 21 → control connection (commands)

Port 20 or high ports → data connection (file transfers, directory listings)

It’s plaintext by default:

Usernames, passwords, commands, and file contents are all visible on the network.

1.2 Control vs data connection
FTP uses two separate connections:

Control connection (client ↔ server):

Established first, usually to port 21.

Used for commands like USER, PASS, LIST, RETR, STOR.

Stays open during the session.

Data connection:

Opened when needed (e.g., ls, get, put).

Used to actually transfer directory listings or file contents.

Opened and closed per transfer.

If the control connection drops, you’ll see errors like:

text
ftp: No control connection for command
1.3 Active vs passive mode
This is where many people get stuck.

Active mode:

Client tells server: “Open a connection back to me on port X.”

Server initiates the data connection to the client.

Often blocked by firewalls/NAT.

Passive mode:

Client asks server: “Tell me a port I can connect to.”

Server replies with a port, and client connects to that port.

Better for clients behind NAT/firewalls.

In FTP clients:

passive on → use passive mode

passive off → use active mode

On HTB, sometimes passive mode causes issues, so turning it off can fix get/ls problems.

1.4 Authentication types
Common FTP auth setups:

Anonymous FTP:

Username: anonymous

Password: anything (or email, or blank)

Often used for public file distribution.

Misconfigurations can expose sensitive files.

Named users:

user:password accounts.

Sometimes reused credentials from other services.

No auth:

Rare, but sometimes FTP is completely open.

In Fawn, FTP is configured with anonymous login enabled.

1.5 Common FTP client commands
Inside ftp>:

open <ip> → connect to server

user <username> → specify username

pass <password> → specify password (often prompted automatically)

ls → list files on remote server

pwd → show current remote directory

cd <dir> → change remote directory

lcd <dir> → change local directory

get <file> → download file from server to local machine

mget <files> → download multiple files

put <file> → upload file to server

mput <files> → upload multiple files

binary / ascii → set transfer mode

passive → toggle passive mode

bye / quit → exit FTP client

Important: Linux commands (cat, ls with flags, grep, etc.) do not work inside ftp>.

1.6 Security issues with FTP
Why FTP is interesting for attackers:

Plaintext credentials:

If not wrapped in TLS (FTPS), credentials can be sniffed.

Anonymous access:

Misconfigured servers expose sensitive files.

World-readable directories:

Logs, backups, configs, database dumps.

Writable directories:

Uploading web shells to web roots.

Dropping malicious binaries or scripts.

Version vulnerabilities:

Old FTP daemons (e.g., vsftpd backdoor versions).

In CTFs and HTB, FTP often appears as:

A way to retrieve a flag.

A way to upload a web shell.

A way to enumerate interesting files (credentials, configs, keys).

2. Attacker use cases for FTP
2.1 Anonymous read access
Enumerate files:

ls, cd, pwd

Download interesting files:

get config.php

get backup.sql

get id_rsa

Use downloaded data to pivot:

Credentials reused on SSH, MySQL, web logins.

Fawn is a minimal example of this: anonymous FTP → flag.txt.

2.2 Anonymous write access
If you can upload:

Upload a web shell into a web-accessible directory:

put shell.php

Then browse to http://target/shell.php

Upload cron scripts or binaries if the FTP directory is tied to some scheduled process.

Upload SSH keys into .ssh directories if mapped.

2.3 Authenticated access
If you find credentials:

Try logging into FTP with them.

Check home directories, backups, configs.

Look for:

.ssh/

.bash_history

config.php

db_backup.sql

notes.txt

2.4 Version-based exploitation
If nmap shows something like:

text
21/tcp open  ftp     vsftpd 2.3.4
You might search for known exploits (e.g., vsftpd 2.3.4 backdoor).
In Fawn, the version is vsftpd 3.0.3, which is not the point of the box—it’s about anonymous access, not exploitation.

3. Fawn box – full step-by-step breakdown
This is the part you can almost drop into your GitHub writeup.

3.1 Setup and VPN
Goal: Connect to HTB Starting Point network and reach the Fawn machine.

Download VPN file (already done for Meow):

Example: starting_points_eu-starting-point-2-dhcp.ovpn

Connect to VPN:

bash
sudo openvpn starting_points_eu-starting-point-2-dhcp.ovpn
Verify VPN interface:

bash
ip a
Look for tun0 with an IP like 10.10.x.x.

Start Fawn on HTB and note its IP, e.g.:

text
10.129.13.230
Ping the machine:

bash
ping -c 3 10.129.13.230
If you get replies, you’re good.

3.2 Port scanning and service enumeration
Goal: Identify open ports and services.

Basic Nmap scan:

bash
nmap -sV -sC 10.129.13.230
Expected output (core part):

Port 21/tcp open ftp

Service: vsftpd 3.0.3

Nmap script result may show:

Anonymous FTP login allowed

Interpretation:

FTP is running.

Anonymous login is allowed.

No other ports are relevant for this box.

Optional for notes:

bash
nmap --script ftp-anon -p21 10.129.13.230
This explicitly confirms anonymous access.

3.3 Connecting to FTP
Goal: Log in anonymously and see what’s available.

Connect:

bash
ftp 10.129.13.230
Login as anonymous:

When prompted:

text
Name (10.129.13.230:kali): anonymous
Password: <press Enter>
Successful login message:

You’ll see something like:

text
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
Check remote directory:

bash
pwd
Output:

text
Remote directory: /
List files:

bash
ls
Output:

text
-rw-r--r--    1 0        0              32 Jun 04  2021 flag.txt
So we know:

There is a file named flag.txt.

It’s readable by everyone (-rw-r--r--).

3.4 Downloading the flag
Goal: Retrieve flag.txt from the FTP server to your local machine.

(Optional) Disable passive mode if needed:

If you get errors like:

text
ftp: No control connection for command
then inside ftp>:

bash
passive off
Download the file:

Inside ftp>:

bash
get flag.txt
Expected output:

text
local: flag.txt remote: flag.txt
150 Opening BINARY mode data connection for flag.txt (32 bytes).
226 Transfer complete.
32 bytes received in 00:00 (0.30 KiB/s)
Exit FTP:

bash
bye
3.5 Reading the flag locally
Goal: View the contents of flag.txt on your Kali machine.

Check your current directory:

bash
pwd
In your case, it was:

text
/home/kali/Downloads
List files:

bash
ls
You saw:

text
flag.txt  starting_points_eu-starting-point-2-dhcp.ovpn
Read the flag:

bash
cat flag.txt
Output:

text
035db21c881520061c53e0536e44f815
Submit this flag on HTB for Fawn.

3.6 Key learning points from Fawn
FTP is not a shell:

You cannot use cat inside ftp>.

You must get files and then use Linux tools (cat, grep, etc.) locally.

Anonymous FTP is dangerous:

Anyone can log in and read files.

In real environments, this can expose sensitive data.

Control vs data connection:

Errors like “No control connection” are related to FTP’s dual-connection design.

passive off can fix issues.

Workflow pattern:

Enumerate → Identify FTP → Check anonymous → List files → Download → Analyze.

This pattern will repeat in more complex forms later.

4. GitHub-ready notes structure
Here’s a structure you can use directly in your repo, e.g.:

Fawn/README.md or Fawn/walkthrough.md.

markdown
# Fawn – Hack The Box Starting Point

## Overview

**Difficulty:** Very Easy  
**OS:** Linux  
**Category:** Starting Point  
**Focus:** FTP, anonymous login, basic enumeration

Fawn introduces the FTP service and shows how misconfigured anonymous access can expose sensitive files.

---

## 1. Environment setup

- Connected to HTB via OpenVPN:

```bash
sudo openvpn starting_points_eu-starting-point-2-dhcp.ovpn
Verified VPN interface:

bash
ip a   # checked for tun0
Target IP (from HTB panel):

text
10.129.13.230
Connectivity check:

bash
ping -c 3 10.129.13.230
2. Port scanning and service enumeration
2.1 Nmap scan
bash
nmap -sV -sC 10.129.13.230
Key findings:

21/tcp open ftp

Service: vsftpd 3.0.3

Anonymous FTP login allowed

3. FTP enumeration
3.1 Connect to FTP
bash
ftp 10.129.13.230
Login:

text
Name: anonymous
Password: <Enter>

3.2 List remote directory
bash
pwd
ls
Output:

text
Remote directory: /
-rw-r--r--    1 0        0              32 Jun 04  2021 flag.txt

4. Downloading the flag
4.1 Handle potential passive mode issues
If needed:

bash
passive off
4.2 Download flag.txt
bash
get flag.txt
Exit FTP:

bash
bye

Tuesday

I just completed Meow box, now walk me through the steps to complete fawn from htb
You’re moving perfectly through Starting Point, Abhishek — Fawn is the natural next step after Meow, and it reinforces the same fundamentals while adding one new idea: anonymous FTP access.

Here’s a clean, structured, step‑by‑step walkthrough you can use for your YouTube + GitHub workflow as well.

🟢 1. Understand the Goal of Fawn
Fawn teaches one core concept:

FTP service running with anonymous login enabled

Your job is to:

Enumerate open ports

Identify FTP

Log in anonymously

Retrieve the flag

This is foundational for later HTB machines.

🟢 2. Start the Machine & Get the IP
Once you click Play Machine, HTB gives you an IP — usually something like:

Code
10.129.x.x
Make sure your HTB VPN is connected (same as you did for Meow).

🟢 3. Run an Nmap Scan
You want to identify open ports and services.

Use a simple scan first:

bash
nmap -sV -sC 10.129.x.x
What you’ll see:

Port 21/tcp open ftp

Service: vsftpd

Anonymous login: allowed

This is the key discovery.

🟢 4. Connect to FTP Anonymously
FTP often allows login using:

Username: anonymous

Password: anything (or blank)

Run:

bash
ftp 10.129.x.x
When prompted:

Code
Name: anonymous
Password: <press Enter>
You should now be inside the FTP server.

🟢 5. Enumerate Files Inside FTP
List files:

bash
ls
You’ll typically see:

Code
flag.txt
Download it:

bash
get flag.txt
Exit FTP:

bash
bye
🟢 6. Read the Flag
Now simply:

bash
cat flag.txt
Copy the flag into HTB.

🟢 7. What You Learned (Important for Your Red Team Path)
Fawn reinforces:

Service enumeration

Recognizing FTP

Understanding anonymous login

Basic file retrieval over FTP

No exploitation needed — just correct enumeration

This is exactly the mindset you need for OSCP-style machines: enumerate → identify misconfig → exploit.

🟢 8. Optional: A More Advanced Nmap Scan (For Your GitHub Writeup)
You can also include this in your repo:

bash
nmap -p- -A 10.129.x.x
Or a script scan:

bash
nmap --script ftp-anon -p21 10.129.x.x
This will explicitly confirm anonymous access.

🟢 9. How to Present This in Your YouTube + GitHub Workflow
Since you’re building ZeroToRoot Lab:

For YouTube
Start with a 10–15 sec intro

Show Nmap scan

Explain FTP anonymous login

Download flag

End with a quick recap

For GitHub
Use your Meow structure:

Code
Fawn/
 ├── nmap.txt
 ├── walkthrough.md
 ├── screenshots/
 └── fawn.mp4 (optional)
If you want, I can also generate:

A full GitHub‑ready writeup

A YouTube script in your teaching style

A thumbnail text idea

A command-by-command cheat sheet

Which one do you want next?

DO I not need to download vpn for fawn. Is the ovpn file downloaded for Meow good to use for fawn?
You do not need to download a new VPN file for Fawn. The .ovpn file you downloaded for Meow is the same one you will use for every Starting Point machine, including Fawn, Dancing, Redeemer, etc.

Why the same VPN file works
Hack The Box gives you a VPN configuration that connects you to a specific HTB network (e.g., EU StartingPoint 2).
Once you’re connected to that network:

Every machine inside that network becomes reachable

You only need to switch machines, not VPN files

The IP address changes per machine, but the VPN stays the same

When you would need a new VPN file
Only in these situations:

You switch to a different region (e.g., from EU to US)

You switch to a different lab type (e.g., from Starting Point to Regular Machines, Pro Labs, Battlegrounds)

Your VPN file expires (rare, but HTB sometimes regenerates them)

For your current workflow
Since you’re on EU StartingPoint 2, the same .ovpn file you used for Meow will work perfectly for Fawn.

Quick check to confirm
Run:

bash
ip a
You should see an interface like:

Code
tun0
Then ping the Fawn IP:

bash
ping 10.129.x.x
If you get replies, you’re good to go.

If you want, I can walk you through verifying connectivity or help you start the Fawn enumeration cleanly.

what language are we using in kali
You’re using Linux inside Kali — specifically the Bash shell (Bourne Again Shell). That’s the default command‑line environment for Kali Linux, and it’s the language you’ve been using for all HTB commands so far.

To give you a complete, structured picture, here’s how it fits together.

🐧 What “language” you use in Kali
Kali is a Linux distribution, and when you type commands in the terminal, you’re using:

Bash — the command-line shell

Linux command syntax — tools like nmap, ftp, ls, cat, ping, etc.

GNU utilities — the standard Linux toolkit

Networking tools — ip, ifconfig, netcat, ssh, etc.

So the “language” is not Python or C — it’s Bash commands running on Linux.

🧠 Why Bash is used for hacking labs
Bash is the default for almost all penetration testing workflows because it gives you:

Direct access to networking tools

Easy chaining of commands (|, >, &&)

Quick automation

Compatibility with every Linux-based tool

This is why HTB, OSCP, and real-world pentesting all assume Bash proficiency.

🛠 Examples of Bash commands you already used
nmap -sV -sC 10.129.x.x

ftp 10.129.x.x

ls, cat, cd

ping 10.129.x.x

ip a

All of these are Bash commands executed in a Linux environment.

🧩 What about Python, Perl, or other languages?
You can use them in Kali, but only when needed:

Python for exploit scripts

Perl for older exploits

C for compiling payloads

Bash for quick automation

For Starting Point machines like Meow and Fawn, Bash is all you need.

🧭 How this fits your red-team journey
Mastering Bash is essential for:

Enumeration

Privilege escalation

Automation

Writing quick scripts

OSCP-style machines

You’re already using it naturally — now you’ll start chaining commands and writing small scripts as you progress.

If you want, I can also show you:

A Bash cheat sheet tailored for HTB

The 10 Bash commands every pentester must know

How to write your first Bash automation script for enumeration

Which direction do you want to go next?

Today

when I get into ftb for fawn I get following file list and when I try to do cat flag.txt I get an error as see in the ss
You’re doing everything correctly — the only issue is you tried to use cat inside the FTP client, and FTP does not support Linux commands like cat, less, nano, etc.

That’s why you see:

Code
?Invalid command.
This is expected. FTP has its own limited command set.

🟢 Why cat doesn’t work inside FTP
When you’re inside the FTP prompt:

Code
ftp>
you are no longer in your Kali shell.
You’re inside the FTP program, which only supports FTP‑specific commands like:

ls

get

put

pwd

cd

bye

Linux commands like cat, rm, chmod, grep, etc. do not work inside FTP.

🟢 The correct way to read flag.txt
You must download the file first, then read it from your Kali machine.

Step 1 — Download the file from FTP
Inside the FTP prompt:

bash
get flag.txt
You should see:

Code
local: flag.txt remote: flag.txt
226 Transfer complete.
Step 2 — Exit FTP
bash
bye
Step 3 — Read the file in your Kali terminal
bash
cat flag.txt
Now you’ll see the flag.

🟢 Why this matters (important for your learning)
This is a core pentesting concept:

FTP is not a shell.

You cannot execute system commands inside FTP.

You must download files and inspect them locally.

This will matter later when you deal with:

SMB shares

NFS mounts

S3 buckets

WebDAV

SSH vs SFTP

Each protocol has its own command set.

🟢 Quick mental model
When you see:

Code
ftp>
Think:

“I’m inside a file-transfer program, not a Linux shell.”

When you see:

Code
kali@kali:~$
Think:

“I’m back in my Linux shell; I can use cat, grep, nano, etc.”

If you want, you can send me your next screenshot after running get flag.txt, and I’ll confirm everything is correct before you submit the flag.


can't use get command to download the file
You’re extremely close — the error you’re seeing:

Code
ftp: No control connection for command
means your FTP session dropped its control channel, so the get command can’t run. This is a very common issue with FTP in Extended Passive Mode on HTB networks.

Let’s break down what’s happening and how to fix it cleanly.

🧩 Why the get command is failing
FTP uses two connections:

Control connection → for commands (ls, get, cd, etc.)

Data connection → for transferring files

Your control connection dropped temporarily, so FTP can’t open the data channel to download the file.

This usually happens because:

The FTP client switched to Extended Passive Mode (EPSV)

The HTB VPN sometimes blocks EPSV data ports

The FTP session idled too long

The FTP server closed the control channel

🛠 Fix: Disable passive mode inside FTP
Inside the FTP prompt, run:

bash
passive off
You should see:

Code
Passive mode off.
Then try:

bash
get flag.txt
This forces FTP to use Active Mode, which works better on HTB.

🛠 If that doesn’t work: reconnect cleanly
Exit FTP:

bash
bye
Reconnect:

bash
ftp 10.129.13.230
Log in again:

Code
Name: anonymous
Password: <press Enter>
Then:

bash
passive off
ls
get flag.txt
🛠 If it still fails: use wget instead (works 100% of the time)
FTP servers allow anonymous downloads directly using wget:

bash
wget ftp://anonymous:@10.129.13.230/flag.txt
Then read it:

bash
cat flag.txt
This bypasses the FTP client entirely and avoids passive/active mode issues.

🧠 Quick mental model for future HTB machines
FTP is old and finicky. When you see errors like:

“No control connection”

“425 Can’t open data connection”

“Invalid EPSV response”

your first move should always be:

bash
passive off
If you want, send me your next screenshot after running passive off, and I’ll confirm everything is working before you submit the flag.


it woked but I thought I woupld have to cd thn ls to all the file is in dir and only then do cat
You didn’t miss anything — what you expected to do (cd → ls → cat) is the normal Linux workflow, but FTP works differently. The reason it felt confusing is because FTP is not a shell, so the directory navigation and file‑reading rules change.

Here’s the clean breakdown so it makes sense for every future machine.

🧭 Why you didn’t need cd or deeper navigation
Fawn’s FTP server exposes only one directory — the root of the FTP share. When you logged in and ran:

Code
pwd
you saw:

Code
/
And when you ran:

Code
ls
you saw:

Code
flag.txt
That means the file is already in the top-level directory of the FTP share. There are no subfolders to cd into.

Many real FTP servers have:

/pub

/uploads

/home/user

/files

…but Fawn keeps it intentionally simple.

📁 Why you couldn’t use cat inside FTP
This is the key concept:

FTP is a file-transfer program, not a Linux shell.

So inside ftp> you can only use FTP commands:

ls

get

put

cd

pwd

bye

Commands like cat, nano, grep, chmod, etc. do not exist inside FTP.

That’s why you must:

Download the file using get flag.txt

Exit FTP

Read it in your Kali shell using cat flag.txt

This is the correct workflow.

🧠 How to think about this going forward
Whenever you’re inside a protocol client:

ftp>

smb: \>

mysql>

psql>

redis-cli>

mongo>

…you are not in a Linux shell.
You’re inside a program that only understands its own commands.

So the rule is:

Use the protocol’s commands to retrieve data, then use Linux commands to analyze it.

This mindset will help you in SMB, NFS, SSH, MySQL, Redis, and many more HTB machines.

🔍 A quick check for your understanding
When you see a file inside FTP, what’s the correct sequence?

get filename

bye

cat filename

If that matches your mental model now, you’re ready for the next Starting Point box.

Do you want to move on to Dancing next, or do you want a quick recap of FTP concepts for your GitHub writeup?

no you misunderstood, I mean after we use get in ftp to download the fle andd then get out using bye into linux and then in kali terminal instead of changing directory to downloads to see if the file is downloaded we just run cat in kali
See my thinking
Got you now—that’s a really good instinctual question.

Short answer:
You only need to cd into Downloads if you’re not already there. In your screenshot, you were already in ~/Downloads, so running:

bash
cat flag.txt
worked immediately.

What actually happened step by step
Inside FTP, you ran:

bash
get flag.txt
By default, FTP saves the file into your current local directory (whatever directory your shell was in when you started ftp).

You exited FTP:

bash
bye
Your shell prompt showed:

bash
┌──(kali㉿kali)-[~/Downloads]
That means your current working directory is already ~/Downloads.

So when you ran:

bash
cat flag.txt
it worked, because flag.txt was saved in ~/Downloads, and you were already there.

When you would need cd
If your prompt was:

bash
┌──(kali㉿kali)-[~]
or:

bash
┌──(kali㉿kali)-[/]
then you’d need to:

bash
cd Downloads
ls
cat flag.txt
So the rule is:

Check your current directory with:

bash
pwd
If it’s where the file was downloaded → just cat flag.txt

If not → cd into the correct folder first

Mental model to keep
FTP saves to “where you were when you launched ftp”.

Your shell prompt tells you where you are now.

cat works if the file is in your current directory or you give a path:

bash
cat Downloads/flag.txt
You’re thinking exactly like someone who’s going to crush OSCP later—this attention to detail is gold.

got it, now give me step by step break down of ftp and what are the various use cases and expllain the box steps as well in detail along with prepring notes got github , I'll upload this on github
Love this—this is exactly how you turn a “simple” box into real foundations + a clean GitHub artifact.

I’ll give you:

FTP fundamentals (protocol, modes, auth, commands, security issues)

Typical attacker use cases

Full Fawn walkthrough, step by step

GitHub‑ready notes structure (you can almost paste this into README.md / walkthrough.md)

You can tweak wording to match your ZeroToRoot voice, but this will be a solid base.

1. FTP fundamentals
1.1 What is FTP?
FTP (File Transfer Protocol) is an old protocol used to transfer files between a client and a server.

It runs over TCP, typically on:

Port 21 → control connection (commands)

Port 20 or high ports → data connection (file transfers, directory listings)

It’s plaintext by default:

Usernames, passwords, commands, and file contents are all visible on the network.

1.2 Control vs data connection
FTP uses two separate connections:

Control connection (client ↔ server):

Established first, usually to port 21.

Used for commands like USER, PASS, LIST, RETR, STOR.

Stays open during the session.

Data connection:

Opened when needed (e.g., ls, get, put).

Used to actually transfer directory listings or file contents.

Opened and closed per transfer.

If the control connection drops, you’ll see errors like:

text
ftp: No control connection for command
1.3 Active vs passive mode
This is where many people get stuck.

Active mode:

Client tells server: “Open a connection back to me on port X.”

Server initiates the data connection to the client.

Often blocked by firewalls/NAT.

Passive mode:

Client asks server: “Tell me a port I can connect to.”

Server replies with a port, and client connects to that port.

Better for clients behind NAT/firewalls.

In FTP clients:

passive on → use passive mode

passive off → use active mode

On HTB, sometimes passive mode causes issues, so turning it off can fix get/ls problems.

1.4 Authentication types
Common FTP auth setups:

Anonymous FTP:

Username: anonymous

Password: anything (or email, or blank)

Often used for public file distribution.

Misconfigurations can expose sensitive files.

Named users:

user:password accounts.

Sometimes reused credentials from other services.

No auth:

Rare, but sometimes FTP is completely open.

In Fawn, FTP is configured with anonymous login enabled.

1.5 Common FTP client commands
Inside ftp>:

open <ip> → connect to server

user <username> → specify username

pass <password> → specify password (often prompted automatically)

ls → list files on remote server

pwd → show current remote directory

cd <dir> → change remote directory

lcd <dir> → change local directory

get <file> → download file from server to local machine

mget <files> → download multiple files

put <file> → upload file to server

mput <files> → upload multiple files

binary / ascii → set transfer mode

passive → toggle passive mode

bye / quit → exit FTP client

Important: Linux commands (cat, ls with flags, grep, etc.) do not work inside ftp>.

1.6 Security issues with FTP
Why FTP is interesting for attackers:

Plaintext credentials:

If not wrapped in TLS (FTPS), credentials can be sniffed.

Anonymous access:

Misconfigured servers expose sensitive files.

World-readable directories:

Logs, backups, configs, database dumps.

Writable directories:

Uploading web shells to web roots.

Dropping malicious binaries or scripts.

Version vulnerabilities:

Old FTP daemons (e.g., vsftpd backdoor versions).

In CTFs and HTB, FTP often appears as:

A way to retrieve a flag.

A way to upload a web shell.

A way to enumerate interesting files (credentials, configs, keys).

2. Attacker use cases for FTP
2.1 Anonymous read access
Enumerate files:

ls, cd, pwd

Download interesting files:

get config.php

get backup.sql

get id_rsa

Use downloaded data to pivot:

Credentials reused on SSH, MySQL, web logins.

Fawn is a minimal example of this: anonymous FTP → flag.txt.

2.2 Anonymous write access
If you can upload:

Upload a web shell into a web-accessible directory:

put shell.php

Then browse to http://target/shell.php

Upload cron scripts or binaries if the FTP directory is tied to some scheduled process.

Upload SSH keys into .ssh directories if mapped.

2.3 Authenticated access
If you find credentials:

Try logging into FTP with them.

Check home directories, backups, configs.

Look for:

.ssh/

.bash_history

config.php

db_backup.sql

notes.txt

2.4 Version-based exploitation
If nmap shows something like:

text
21/tcp open  ftp     vsftpd 2.3.4
You might search for known exploits (e.g., vsftpd 2.3.4 backdoor).
In Fawn, the version is vsftpd 3.0.3, which is not the point of the box—it’s about anonymous access, not exploitation.

3. Fawn box – full step-by-step breakdown
This is the part you can almost drop into your GitHub writeup.

3.1 Setup and VPN
Goal: Connect to HTB Starting Point network and reach the Fawn machine.

Download VPN file (already done for Meow):

Example: starting_points_eu-starting-point-2-dhcp.ovpn

Connect to VPN:

bash
sudo openvpn starting_points_eu-starting-point-2-dhcp.ovpn
Verify VPN interface:

bash
ip a
Look for tun0 with an IP like 10.10.x.x.

Start Fawn on HTB and note its IP, e.g.:

text
10.129.13.230
Ping the machine:

bash
ping -c 3 10.129.13.230
If you get replies, you’re good.

3.2 Port scanning and service enumeration
Goal: Identify open ports and services.

Basic Nmap scan:

bash
nmap -sV -sC 10.129.13.230
Expected output (core part):

Port 21/tcp open ftp

Service: vsftpd 3.0.3

Nmap script result may show:

Anonymous FTP login allowed

Interpretation:

FTP is running.

Anonymous login is allowed.

No other ports are relevant for this box.

Optional for notes:

bash
nmap --script ftp-anon -p21 10.129.13.230
This explicitly confirms anonymous access.

3.3 Connecting to FTP
Goal: Log in anonymously and see what’s available.

Connect:

bash
ftp 10.129.13.230
Login as anonymous:

When prompted:

text
Name (10.129.13.230:kali): anonymous
Password: <press Enter>
Successful login message:

You’ll see something like:

text
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
Check remote directory:

bash
pwd
Output:

text
Remote directory: /
List files:

bash
ls
Output:

text
-rw-r--r--    1 0        0              32 Jun 04  2021 flag.txt
So we know:

There is a file named flag.txt.

It’s readable by everyone (-rw-r--r--).

3.4 Downloading the flag
Goal: Retrieve flag.txt from the FTP server to your local machine.

(Optional) Disable passive mode if needed:

If you get errors like:

text
ftp: No control connection for command
then inside ftp>:

bash
passive off
Download the file:

Inside ftp>:

bash
get flag.txt
Expected output:

text
local: flag.txt remote: flag.txt
150 Opening BINARY mode data connection for flag.txt (32 bytes).
226 Transfer complete.
32 bytes received in 00:00 (0.30 KiB/s)
Exit FTP:

bash
bye
3.5 Reading the flag locally
Goal: View the contents of flag.txt on your Kali machine.

Check your current directory:

bash
pwd
In your case, it was:

text
/home/kali/Downloads
List files:

bash
ls
You saw:

text
flag.txt  starting_points_eu-starting-point-2-dhcp.ovpn
Read the flag:

bash
cat flag.txt
Output:

text
035db21c881520061c53e0536e44f815
Submit this flag on HTB for Fawn.

3.6 Key learning points from Fawn
FTP is not a shell:

You cannot use cat inside ftp>.

You must get files and then use Linux tools (cat, grep, etc.) locally.

Anonymous FTP is dangerous:

Anyone can log in and read files.

In real environments, this can expose sensitive data.

Control vs data connection:

Errors like “No control connection” are related to FTP’s dual-connection design.

passive off can fix issues.

Workflow pattern:

Enumerate → Identify FTP → Check anonymous → List files → Download → Analyze.

This pattern will repeat in more complex forms later.

4. GitHub-ready notes structure
Here’s a structure you can use directly in your repo, e.g.:

Fawn/README.md or Fawn/walkthrough.md.

markdown
# Fawn – Hack The Box Starting Point

## Overview

**Difficulty:** Very Easy  
**OS:** Linux  
**Category:** Starting Point  
**Focus:** FTP, anonymous login, basic enumeration

Fawn introduces the FTP service and shows how misconfigured anonymous access can expose sensitive files.

---

## 1. Environment setup

- Connected to HTB via OpenVPN:

```bash
sudo openvpn starting_points_eu-starting-point-2-dhcp.ovpn
Verified VPN interface:

bash
ip a   # checked for tun0
Target IP (from HTB panel):

text
10.129.13.230
Connectivity check:

bash
ping -c 3 10.129.13.230
2. Port scanning and service enumeration
2.1 Nmap scan
bash
nmap -sV -sC 10.129.13.230
Key findings:

21/tcp open ftp

Service: vsftpd 3.0.3

Anonymous FTP login allowed

(Optional):

bash
nmap --script ftp-anon -p21 10.129.13.230
3. FTP enumeration
3.1 Connect to FTP
bash
ftp 10.129.13.230
Login:

text
Name: anonymous
Password: <Enter>
3.2 List remote directory
bash
pwd
ls
Output:

text
Remote directory: /
-rw-r--r--    1 0        0              32 Jun 04  2021 flag.txt
4. Downloading the flag
4.1 Handle potential passive mode issues
If needed:

bash
passive off
4.2 Download flag.txt
bash
get flag.txt
Exit FTP:

bash
bye
5. Reading the flag locally
Assuming current directory is ~/Downloads:

bash
ls
cat flag.txt
Flag:

text
035db21c881520061c53e0536e44f815

6. Lessons learned
FTP uses a control connection and a data connection.

Anonymous FTP can expose sensitive files if misconfigured.

FTP clients have their own command set (ls, get, put, cd, pwd, passive).

System commands like cat must be run outside the FTP client, after downloading files.

Pattern: Enumerate → Identify FTP → Check anonymous → Download → Analyze.
