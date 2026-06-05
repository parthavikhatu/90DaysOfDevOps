# Shell Scripting Cheat Sheet for DevOps Engineers

## Quick Reference Table

| Topic    | Syntax                 | Example                          |
| -------- | ---------------------- | -------------------------------- |
| Variable | VAR="value"            | NAME="Parthavi"                  |
| Argument | $1, $2                 | ./script.sh arg1                 |
| If       | if [ condition ]; then | if [ -f file ]; then             |
| For Loop | for i in list; do      | for i in 1 2 3; do               |
| Function | name() { ... }         | greet() { echo "Hi"; }           |
| Grep     | grep pattern file      | grep -i "error" app.log          |
| Awk      | awk '{print $1}' file  | awk -F: '{print $1}' /etc/passwd |
| Sed      | sed 's/old/new/g' file | sed -i 's/foo/bar/g' config.txt  |

---

# 1. Basics

## Shebang

Tells Linux which interpreter should execute the script.

```bash
#!/bin/bash
```

## Running Scripts

```bash
chmod +x script.sh
./script.sh

bash script.sh
```

## Comments

```bash
# Single line comment

echo "Hello" # Inline comment
```

## Variables

```bash
NAME="Parthavi"

echo $NAME
echo "$NAME"
echo '$NAME'
```

### Quotes

```bash
echo "$NAME"   # Expands variable
echo '$NAME'   # Prints literally
```

## User Input

```bash
read -p "Enter Name: " NAME
echo $NAME
```

## Command-Line Arguments

```bash
$0   # Script name
$1   # First argument
$2   # Second argument
$#   # Number of arguments
$@   # All arguments
$?   # Exit code
```

Example:

```bash
./script.sh aws docker
```

---

# 2. Operators and Conditionals

## String Comparison

```bash
[ "$a" = "$b" ]
[ "$a" != "$b" ]
[ -z "$var" ]
[ -n "$var" ]
```

## Integer Comparison

```bash
-eq   Equal
-ne   Not Equal
-lt   Less Than
-gt   Greater Than
-le   Less Than or Equal
-ge   Greater Than or Equal
```

Example:

```bash
[ "$num" -gt 10 ]
```

## File Tests

```bash
-f file    # File exists
-d dir     # Directory exists
-e path    # Exists
-r file    # Readable
-w file    # Writable
-x file    # Executable
-s file    # Not empty
```

## If Statement

```bash
if [ condition ]; then
    command
elif [ condition ]; then
    command
else
    command
fi
```

## Logical Operators

```bash
&&   AND
||   OR
!    NOT
```

Example:

```bash
[ -f file ] && echo "Exists"
```

## Case Statement

```bash
case $option in

start)
    echo "Starting"
    ;;

stop)
    echo "Stopping"
    ;;

*)
    echo "Invalid Option"
    ;;
esac
```

---

# 3. Loops

## For Loop

```bash
for fruit in apple mango orange
do
    echo $fruit
done
```

## C-Style For Loop

```bash
for ((i=1;i<=5;i++))
do
    echo $i
done
```

## While Loop

```bash
count=1

while [ $count -le 5 ]
do
    echo $count
    count=$((count+1))
done
```

## Until Loop

```bash
count=1

until [ $count -gt 5 ]
do
    echo $count
    count=$((count+1))
done
```

## Loop Control

```bash
break
continue
```

## Loop Through Files

```bash
for file in *.log
do
    echo $file
done
```

## Loop Through Command Output

```bash
cat file.txt | while read line
do
    echo $line
done
```

---

# 4. Functions

## Define Function

```bash
greet() {
    echo "Hello"
}
```

## Call Function

```bash
greet
```

## Function Arguments

```bash
greet() {
    echo "Hello $1"
}

greet Parthavi
```

## Return vs Echo

```bash
sum() {
    echo $(($1+$2))
}
```

```bash
return 0
```

## Local Variables

```bash
demo() {
    local name="Parthavi"
}
```

---

# 5. Text Processing Commands

## grep

```bash
grep "error" app.log
grep -i "error" app.log
grep -r "error" .
grep -c "error" app.log
grep -n "error" app.log
grep -v "error" app.log
grep -E "ERROR|FAILED" app.log
```

## awk

```bash
awk '{print $1}' file.txt

awk -F: '{print $1}' /etc/passwd

awk 'BEGIN{print "Start"} {print $1} END{print "End"}' file.txt
```

## sed

```bash
sed 's/old/new/g' file.txt

sed '5d' file.txt

sed -i 's/foo/bar/g' file.txt
```

## cut

```bash
cut -d: -f1 /etc/passwd
```

## sort

```bash
sort file.txt
sort -n numbers.txt
sort -r file.txt
sort -u file.txt
```

## uniq

```bash
uniq file.txt
uniq -c file.txt
```

## tr

```bash
tr 'a-z' 'A-Z'
tr -d ','
```

## wc

```bash
wc -l file.txt
wc -w file.txt
wc -c file.txt
```

## head / tail

```bash
head -5 file.txt

tail -5 file.txt

tail -f app.log
```

---

# 6. Useful DevOps One-Liners

## Delete Files Older Than 30 Days

```bash
find /tmp -type f -mtime +30 -delete
```

## Count Lines In All Logs

```bash
wc -l *.log
```

## Replace String In Multiple Files

```bash
sed -i 's/old/new/g' *.txt
```

## Check Service Status

```bash
systemctl is-active nginx
```

## Disk Usage Alert

```bash
df -h | awk '$5+0 > 80'
```

## Parse JSON

```bash
cat data.json | jq '.name'
```

## Parse CSV

```bash
awk -F, '{print $1}' data.csv
```

## Real-Time Error Monitoring

```bash
tail -f app.log | grep ERROR
```

---

# 7. Error Handling & Debugging

## Exit Codes

```bash
exit 0
exit 1

echo $?
```

## Exit On Error

```bash
set -e
```

## Unset Variables As Error

```bash
set -u
```

## Catch Pipe Failures

```bash
set -o pipefail
```

## Debug Mode

```bash
set -x
```

## Strict Mode (Recommended)

```bash
set -euo pipefail
```

## Trap

```bash
cleanup() {
    rm -f temp.txt
}

trap cleanup EXIT
```

---

# 8. DevOps Must-Know Commands

## Disk Usage

```bash
df -h
du -sh *
```

## Memory Usage

```bash
free -h
```

## CPU & Processes

```bash
top
htop
ps aux
```

## Network

```bash
ss -tulpn
netstat -tulpn
```

## Logs

```bash
journalctl -xe
tail -f /var/log/syslog
```

## Services

```bash
systemctl status nginx
systemctl restart nginx
```

---

# 9. DevOps Best Practices (Very Important)

## Always Use Strict Mode

```bash
#!/bin/bash
set -euo pipefail
```

## Quote Variables

Good:

```bash
"$file"
```

Bad:

```bash
$file
```

## Check Script Arguments

```bash
if [ $# -lt 1 ]; then
    echo "Usage: $0 <arg>"
    exit 1
fi
```

## Verify Root Access

```bash
if [ "$EUID" -ne 0 ]; then
    echo "Run as root"
    exit 1
fi
```

## Use Functions

Makes scripts reusable and easier to maintain.

## Log Important Actions

```bash
echo "$(date): Backup completed" >> backup.log
```

## Use Meaningful Exit Codes

```bash
exit 0   # Success
exit 1   # Failure
```

---

# 10. Interview Revision

### Most Important Variables

```bash
$0
$1
$#
$@
$?
```

### Most Important Tests

```bash
-f
-d
-r
-w
-x
-z
-n
```

### Most Important Debugging

```bash
set -e
set -u
set -o pipefail
set -x
```

### Most Important Commands

```bash
grep
awk
sed
cut
sort
uniq
find
xargs
jq
```

### Most Important DevOps Tools

```bash
systemctl
journalctl
ss
ps
top
df
du
tar
cron
```
