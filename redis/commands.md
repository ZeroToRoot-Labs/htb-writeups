###############################################
# Redis Enumeration – Command Reference (Bash)
###############################################

# Connect to Redis (default port 6379)
redis-cli -h <IP>

# Connect with a custom port
redis-cli -h <IP> -p <PORT>

# ---------------------------------------------
# BASIC ENUMERATION
# ---------------------------------------------

# List all keys (Redis equivalent of 'ls')
KEYS *

# Retrieve the value of a key
GET <key>

# Check the type of a key
TYPE <key>

# ---------------------------------------------
# SERVER INFORMATION
# ---------------------------------------------

# Display full server information and statistics
INFO

# Display only keyspace information (keys per DB)
INFO keyspace

# ---------------------------------------------
# DATABASE NAVIGATION
# ---------------------------------------------

# Select a specific database (default is DB 0)
SELECT <db_number>

# ---------------------------------------------
# KEY MANAGEMENT (Optional)
# ---------------------------------------------

# Create or update a key
SET <key> <value>

# Delete a key
DEL <key>

# Check if a key exists (returns 1 or 0)
EXISTS <key>

# ---------------------------------------------
# TYPICAL WORKFLOW (HTB Redeemer)
# ---------------------------------------------

redis-cli -h <IP>   # Connect to Redis
KEYS *              # List all keys
GET flag            # Retrieve the flag
INFO                # (Optional) View server statistics
