# Practical Shell Script Examples

In this section, we demonstrate practical examples to help you understand how to use shell scripting in real-world scenarios. These scripts are modular, reusable, and can be adapted for different environments.

---

## 1. Log Analysis Script

Analyze Apache web logs to determine the most visited pages and IP addresses generating the most traffic.

```bash
#!/bin/bash

LOG_FILE="/var/log/apache2/access.log"

echo "=== Most Visited Pages ==="
awk '{print $7}' "$LOG_FILE" | sort | uniq -c | sort -nr | head -5

echo "=== Top IP Addresses ==="
awk '{print $1}' "$LOG_FILE" | sort | uniq -c | sort -nr | head -5
```

**Explanation:**

- `awk '{print $7}'` – extracts the requested URL from log entries.  
- `sort | uniq -c | sort -nr` – counts occurrences and sorts numerically in descending order.  
- `head -5` – shows the top 5 results.

---

## 2. Backup Script

Create timestamped backups of important directories.

```bash
#!/bin/bash

# Simple Backup Script

SOURCE_DIR="/var/log/apache2"
BACKUP_DIR="/backup"
TIMESTAMP=$(date +"%Y-%m-%d_%H-%M-%S")
BACKUP_FILENAME="backup_$TIMESTAMP.tar.gz"

echo "Starting backup of $SOURCE_DIR to $BACKUP_DIR/$BACKUP_FILENAME"

# Create the backup
tar -czf "$BACKUP_DIR/$BACKUP_FILENAME" "$SOURCE_DIR"

if [ $? -eq 0 ]; then
    echo "Backup completed successfully."
else
    echo "Backup failed."
fi
```

**Enhancements:**

- Automatically includes timestamps for unique backup names.  
- Checks exit status with `$?` to confirm success.  

---

## 3. Disk Usage Monitor

Check disk space usage and send a warning if usage exceeds a threshold.

```bash
#!/bin/bash

THRESHOLD=80
df -H | grep -vE '^Filesystem|tmpfs|cdrom' | while read line; do
    USAGE=$(echo $line | awk '{print $5}' | sed 's/%//')
    PARTITION=$(echo $line | awk '{print $1}')
    if [ $USAGE -ge $THRESHOLD ]; then
        echo "Warning: Partition $PARTITION is ${USAGE}% full."
    fi
done
```

**Explanation:**

- `df -H` – displays human-readable disk usage.  
- `grep -vE '^Filesystem|tmpfs|cdrom'` – excludes non-physical drives.  
- Loops through each partition and checks usage against the threshold.

---

## 4. User Account Report

Generate a report of all users on the system and their home directories.

```bash
#!/bin/bash

echo "=== User Accounts ==="
awk -F: '{print "User: "$1, "UID: "$3, "Home: "$6}' /etc/passwd
```

Output will display all users, their UID, and home directories.

---

## 5. Automated Directory Cleanup

Remove files older than a certain number of days.

```bash
#!/bin/bash

TARGET_DIR="/tmp/logs"
DAYS_OLD=7

echo "Removing files older than $DAYS_OLD days from $TARGET_DIR"

find "$TARGET_DIR" -type f -mtime +$DAYS_OLD -exec rm -f {} \;

echo "Cleanup completed."
```

**Explanation:**

- `find ... -mtime +7` – selects files modified more than 7 days ago.  
- `-exec rm -f {}` – removes selected files.  

---

## 6. Simple Network Ping Checker

Check connectivity to a list of servers.

```bash
#!/bin/bash

SERVERS=("8.8.8.8" "1.1.1.1" "github.com")

for SERVER in "${SERVERS[@]}"; do
    ping -c 2 "$SERVER" &> /dev/null
    if [ $? -eq 0 ]; then
        echo "$SERVER is reachable."
    else
        echo "$SERVER is down."
    fi
done
```

**Explanation:**

- Loops over a list of servers.  
- Uses `ping -c 2` to send 2 packets.  
- Checks exit status to determine connectivity.

---

## 7. Mini Practice Tasks

1. Write a script to count the number of files in a directory.  
2. Write a script to archive all `.log` files older than 30 days.  
3. Write a script to check memory usage and alert if free memory < 500MB.  
4. Write a script to monitor CPU load and log it every 10 minutes.  

---

# Summary

These examples demonstrate how shell scripting can automate daily administrative tasks such as:

- Log analysis  
- Backups  
- Disk and memory monitoring  
- Cleanup operations  
- Network checks  

With these techniques, you can build **modular, reusable, and automated scripts** for real-world system administration.
