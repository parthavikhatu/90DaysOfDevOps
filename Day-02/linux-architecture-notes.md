# Linux Architecture, Processes, and systemd

## 1. Core Components of Linux

### Hardware

* Physical components:

  * CPU
  * RAM
  * Disk
  * Network devices

### Kernel

* Core part of Linux OS
* Manages:

  * CPU
  * Memory
  * Devices
  * Filesystems
  * Processes
* Works between hardware and software

### System Libraries

* Provide APIs for applications
* Help programs communicate with kernel
* Example:

  * glibc

### System Utilities

* Specialized tools used for system management
* Examples:

  * ps
  * top
  * systemctl
  * grep

### Shell

* Command-line interface between user and OS
* Accepts commands from users
* Examples:

  * bash
  * zsh

### init / systemd

* First userspace process started during boot
* Runs as PID 1
* Responsible for:

  * Starting services
  * Managing background processes
  * Restarting failed services
  * Managing system boot

---

## 2. Linux Processes

* A process = running program
* Each process has:

  * PID (Process ID)
  * PPID (Parent Process ID)

### Process Creation

Linux creates processes using:

1. `fork()` → creates child process
2. `exec()` → loads program into process

Example:

* bash starts python script
* bash forks child process
* child executes python

---

## 3. Process States

| State    | Meaning                              |
| -------- | ------------------------------------ |
| Running  | Process using CPU                    |
| Sleeping | Waiting for event/input              |
| Stopped  | Process paused                       |
| Zombie   | Finished process waiting for cleanup |

---

## 4. What systemd Does

systemd is the modern Linux service manager.

### Tasks

* Starts services during boot
* Monitors services
* Restarts failed services
* Handles logs using journalctl

### Common Commands

```bash id="75ltw6"
systemctl status nginx
systemctl start nginx
systemctl stop nginx
journalctl -u nginx
```

---

## 5. Daily Linux Commands

```bash id="mnjx4w"
ps aux        # show processes
top           # monitor system usage
systemctl     # manage services
journalctl    # check logs
kill          # stop process
```


