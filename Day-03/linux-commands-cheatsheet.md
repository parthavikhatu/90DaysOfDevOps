1. File Navigation & Listing
ls              → List files and directories
cd              → Change current directory
pwd             → Show present working directory
mkdir           → Create new directory
find            → Search files and directories
locate          → Quickly find files using index

2. File Operations
cp              → Copy files or directories
mv              → Move or rename files
rm              → Remove files or directories
rmdir           → Remove empty directory
touch           → Create empty file or update timestamp
ln              → Create hard or soft links
stat            → Show detailed file information

3. Viewing & Reading Files
cat             → Display file content
zcat            → View compressed .gz file
head            → Show first lines of file
tail            → Show last lines of file
less            → View file page by page
more            → Simple file viewer
grep            → Search text patterns in files

4. Text Processing Commands
cut             → Extract columns from text
sort            → Sort lines of text
wc              → Count lines, words, characters
tee             → Save and display output together
awk             → Advanced text processing tool
sed             → Stream editor for text replacement
diff            → Compare two files
tr              → Translate or delete characters

5. Process Management Commands ★ IMPORTANT
ps              → Show running processes
top             → Real-time process monitor
htop            → Interactive process viewer
kill            → Stop process using PID
killall         → Kill process by name
pgrep           → Find PID by process name
nohup           → Run process after logout
jobs            → Show background jobs
bg              → Run job in background
fg              → Bring job to foreground
nice            → Start process with priority
renice          → Change running process priority
fuser           → Show process using file/port
lsof            → List open files and ports
systemctl       → Manage system services

6. System Resource & Performance Commands
df              → Show disk filesystem usage
du              → Show directory size usage
free            → Show memory and swap usage
vmstat          → Show system performance stats
iostat          → Show CPU and disk I/O stats
uptime          → Show system uptime and load
dmesg           → Show kernel boot/system logs

7. User & Group Management Commands
who             → Show logged-in users
w               → Show user activity
whoami          → Show current username
id              → Show user and group IDs
sudo            → Run command as root
su              → Switch user account
passwd          → Change user password
useradd         → Create new user
userdel         → Delete user
usermod         → Modify user settings
groupadd        → Create new group
groupdel        → Delete group
gpasswd         → Manage group members

8. File Permission Commands
chmod           → Change file permissions
chown           → Change file owner
chgrp           → Change group ownership
umask           → Set default file permissions
getfacl         → View ACL permissions
setfacl         → Set ACL permissions

9. System Management Commands
uname           → Show system/kernel information
hostname        → Show system hostname
date            → Show or set date/time
which           → Show command path
whereis         → Locate binary/source/man files
env             → Show environment variables
export          → Set environment variables
history         → Show command history
shutdown        → Shut down system safely
reboot          → Restart system
journalctl      → View system logs
crontab         → Schedule recurring tasks

10. Package Management Commands
apt             → Debian package manager
dpkg            → Debian package tool
yum             → RHEL package manager
dnf             → Modern Fedora/RHEL package manager
rpm             → RPM package tool

11. Networking & Troubleshooting Commands ★ VERY IMPORTANT
ping            → Check network connectivity
traceroute      → Show packet route to destination
tracepath       → Trace network path
mtr             → Real-time network diagnostics
nslookup        → Query DNS records
dig             → Detailed DNS lookup
curl            → Send HTTP/API requests
ss              → Show socket/network connections
netstat         → Show network statistics and ports
tcpdump         → Capture and analyze packets
lsof            → Show open files and ports
ip a            → Show IP addresses/interfaces
ip route        → Show routing table
nc              → Test TCP/UDP connections
telnet          → Test remote host port connectivity
nmap            → Scan hosts and ports
iptables        → Configure firewall rules
ssh             → Secure remote login
arp             → Show ARP cache
route           → Show routing table
iwconfig        → Configure wireless network
watch           → Repeat command continuously
whois           → Show domain registration info
ifconfig        → Configure network interface

12. File Transfer & Archiving Commands
scp             → Securely copy files over SSH
rsync           → Sync files efficiently
sftp            → Secure file transfer
tar             → Archive/compress files

13. SSH & Remote Access Commands
ssh-keygen      → Generate SSH key pair
ssh-copy-id     → Copy SSH key to server
ssh-agent       → Store SSH keys in memory
tmux            → Persistent terminal session
screen          → Terminal session manager

14. Essential DevOps & Shell Commands
|               → Pipe output between commands
>               → Redirect output to file
>>              → Append output to file
alias           → Create command shortcut
xargs           → Build commands from input
strace          → Trace system calls
set -e          → Exit script on error
set -x          → Debug shell script
man             → Open command manual
echo            → Print text or variables
logrotate       → Rotate/compress log files

!5. MOST ASKED COMMANDS IN DEVOPS INTERVIEWS ★
ps
top
htop
kill
pgrep
nohup
jobs
nice
renice
systemctl
lsof
grep
find
tail -f
df -h
free -m
chmod
chown
curl
ss -tulnp
netstat
ip a
ip route
tcpdump
dig
ssh
scp
rsync
tar
journalctl
crontab
docker
kubectl
git
