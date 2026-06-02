# Day 19 – Shell Scripting Project: Log Rotation, Backup & Crontab

## Objective

Apply shell scripting concepts to real-world DevOps tasks:

* Log rotation and cleanup
* Automated backups
* Cron job scheduling
* Maintenance automation

---

# Task 1: Log Rotation Script

## Why Log Rotation?

Log files grow continuously and can consume disk space. Log rotation compresses old logs and removes very old archives.

### log_rotate.sh

**Script**

```
#!/bin/bash

set -euo pipefail

LOG_DIR=$1

if [ ! -d "$LOG_DIR" ]; then
    echo "Error: Directory does not exist."
    exit 1
fi

compressed=$(find "$LOG_DIR" -name "*.log" -mtime +7 | wc -l)

find "$LOG_DIR" -name "*.log" -mtime +7 -exec gzip {} \;

deleted=$(find "$LOG_DIR" -name "*.gz" -mtime +30 | wc -l)

find "$LOG_DIR" -name "*.gz" -mtime +30 -delete

echo "Compressed Files: $compressed"
echo "Deleted Files: $deleted"
```

**Output**

```
./log_rotate.sh /var/log/myapp

Compressed Files: 5
Deleted Files: 2
```

---

# Task 2: Server Backup Script

## Why Backups?

Backups help recover data during accidental deletion, corruption, or server failure.

### backup.sh

**Script**

```
#!/bin/bash

set -euo pipefail

SOURCE=$1
DESTINATION=$2

if [ ! -d "$SOURCE" ]; then
    echo "Source directory does not exist."
    exit 1
fi

DATE=$(date +%Y-%m-%d)

ARCHIVE="$DESTINATION/backup-$DATE.tar.gz"

tar -czf "$ARCHIVE" "$SOURCE"

if [ -f "$ARCHIVE" ]; then
    echo "Backup Created Successfully"
    ls -lh "$ARCHIVE"
fi

find "$DESTINATION" -name "*.tar.gz" -mtime +14 -delete
```

**Output**

```
./backup.sh /home/ubuntu/data /backups

Backup Created Successfully

-rw-r--r-- 1 root root 120M Feb 8 backup-2026-02-08.tar.gz
```

---

# Task 3: Crontab

## View Existing Cron Jobs

Command:

```
crontab -l
```

### What is Cron?

Cron is a Linux scheduler used to run commands automatically at specific times.

### Cron Format

```
* * * * * command
│ │ │ │ │
│ │ │ │ └── Day of Week (0-7)
│ │ │ └──── Month (1-12)
│ │ └────── Day of Month (1-31)
│ └──────── Hour (0-23)
└────────── Minute (0-59)
```

---

## Run log_rotate.sh Every Day at 2 AM

```
0 2 * * * /home/ubuntu/log_rotate.sh /var/log/myapp
```

---

## Run backup.sh Every Sunday at 3 AM

```
0 3 * * 0 /home/ubuntu/backup.sh /data /backups
```

---

## Run Health Check Every 5 Minutes

```
*/5 * * * * /home/ubuntu/health_check.sh
```

---

# Task 4: Scheduled Maintenance Script

## Goal

Combine backup and log rotation into a single maintenance script.

---

### maintenance.sh

**Script**

```
#!/bin/bash

set -euo pipefail

LOG_FILE="/var/log/maintenance.log"

log_message() {
    echo "$(date '+%Y-%m-%d %H:%M:%S') : $1" >> "$LOG_FILE"
}

rotate_logs() {

    log_message "Starting log rotation"

    find /var/log/myapp -name "*.log" -mtime +7 -exec gzip {} \;

    find /var/log/myapp -name "*.gz" -mtime +30 -delete

    log_message "Log rotation completed"
}

backup_server() {

    log_message "Starting backup"

    DATE=$(date +%Y-%m-%d)

    tar -czf "/backups/backup-$DATE.tar.gz" /home/ubuntu/data

    log_message "Backup completed"
}

main() {

    log_message "Maintenance Started"

    rotate_logs

    backup_server

    log_message "Maintenance Finished"
}

main
```

**Output**

```
2026-02-08 01:00:00 : Maintenance Started

2026-02-08 01:00:01 : Starting log rotation

2026-02-08 01:00:05 : Log rotation completed

2026-02-08 01:00:06 : Starting backup

2026-02-08 01:00:30 : Backup completed

2026-02-08 01:00:31 : Maintenance Finished
```

---

## Cron Entry for maintenance.sh

Run Daily at 1 AM

```
0 1 * * * /home/ubuntu/maintenance.sh
```

---

# Key Commands Learned

```
gzip
tar
find
crontab -l
crontab -e
date
wc -l
ls -lh
```

---

# Interview Questions

### What is log rotation?

The process of compressing, archiving, and deleting old log files to save disk space.

### Why compress logs?

To reduce storage usage while preserving historical logs.

### What is a .tar.gz file?

A compressed archive commonly used for backups in Linux.

### What does tar -czf do?

* c → Create archive
* z → Compress using gzip
* f → Specify filename

### What is cron?

A Linux job scheduler used to automate tasks.

### How do you view existing cron jobs?

```
crontab -l
```

### How do you edit cron jobs?

```
crontab -e
```

### Why delete old backups?

To prevent storage from filling up and maintain retention policies.

### Why log script execution?

To track maintenance activities and simplify troubleshooting.

---

# What I Learned

* Automating log management using shell scripts.
* Creating compressed backups using tar and gzip.
* Scheduling recurring tasks using cron.
* Combining multiple scripts into a maintenance workflow.
* Logging script execution for monitoring and troubleshooting.
