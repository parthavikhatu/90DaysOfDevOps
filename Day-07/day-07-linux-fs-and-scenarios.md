# Day 07 – Linux File System Hierarchy & Scenario Practice

## Part 1: Linux File System Hierarchy

### Core Directories

| Directory  | Purpose                                            | Example Files/Folders     | I would use this when... |
| ---------- | -------------------------------------------------- | ------------------------- | ------------------------ |
| `/`        | Root directory, starting point of Linux filesystem | `home`, `etc`             | navigating entire system |
| `/home`    | Stores normal user files and folders               | `parthavi/`, `Downloads/` | accessing user data      |
| `/root`    | Home directory of root user                        | `.bashrc`                 | working as admin/root    |
| `/etc`     | System configuration files                         | `hostname`, `passwd`      | changing configs         |
| `/var/log` | Stores system and service logs                     | `syslog`, `auth.log`      | troubleshooting issues   |
| `/tmp`     | Temporary files storage                            | temp files                | storing short-term files |

### Additional Directories

| Directory  | Purpose                     | Example Files/Folders | I would use this when...   |
| ---------- | --------------------------- | --------------------- | -------------------------- |
| `/bin`     | Essential Linux commands    | `ls`, `cp`            | running basic commands     |
| `/usr/bin` | User-level command binaries | `git`, `python3`      | using installed apps       |
| `/opt`     | Third-party applications    | `tomcat/`             | checking optional software |

---

## Useful Commands

```bash
# Find largest log files
du -sh /var/log/* 2>/dev/null | sort -h | tail -5

# View hostname config
cat /etc/hostname

# Check home directory
ls -la ~
```

---

# Part 2: Scenario-Based Practice

## Scenario 1: Service Not Starting

### Step 1

```bash
systemctl status myapp
```

Why: Check if service is failed/running.

### Step 2

```bash
journalctl -u myapp -n 50
```

Why: Check recent logs for errors.

### Step 3

```bash
systemctl is-enabled myapp
```

Why: Verify auto-start on boot.

### Step 4

```bash
systemctl restart myapp
```

Why: Try restarting after checks.

---

## Scenario 2: High CPU Usage

### Step 1

```bash
top
```

Why: View live CPU usage.

### Step 2

```bash
ps aux --sort=-%cpu | head -10
```

Why: Find top CPU-consuming processes.

### Step 3

```bash
kill -9 PID
```

Why: Stop problematic process if needed.

---

## Scenario 3: Finding Service Logs

### Step 1

```bash
systemctl status docker
```

Why: Check service status.

### Step 2

```bash
journalctl -u docker -n 50
```

Why: View recent logs.

### Step 3

```bash
journalctl -u docker -f
```

Why: Follow logs in real-time.

---

## Scenario 4: File Permission Issue

### Step 1

```bash
ls -l /home/user/backup.sh
```

Why: Check current permissions.

### Step 2

```bash
chmod +x /home/user/backup.sh
```

Why: Add execute permission.

### Step 3

```bash
./backup.sh
```

Why: Run the script again.

---

# Quick Revision Points

* `/etc` → Config files
* `/var/log` → Logs
* `/home` → User files
* `/tmp` → Temporary files
* `systemctl` → Manage services
* `journalctl` → View service logs
* `top` / `ps aux` → CPU troubleshooting
* `chmod +x` → Make script executable
