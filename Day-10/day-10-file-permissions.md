# Day 10 Challenge

## Files Created

* devops.txt
* notes.txt
* script.sh
* project/

## Permission Changes

### script.sh

Before:
-rw-rw-r--

After:
-rwxrwxr-x

### devops.txt

Before:
-rw-rw-r--

After:
-r--r--r--

### notes.txt

Before:
-rw-rw-r--

After:
-rw-r-----

### project/

Permission:
drwxr-xr-x

## Commands Used

* touch devops.txt
* ls -l
* echo "Hello Dosto." > notes.txt
* cat notes.txt
* vim script.sh
* vim -R script.sh
* head -n 5 /etc/passwd
* tail -n 5 /etc/passwd
* chmod +x script.sh
* ./script.sh
* chmod 444 devops.txt
* chmod 640 notes.txt
* mkdir project
* chmod 755 project
* ls -ld project
* echo "test" >> devops.txt
* chmod -x script.sh

## What I Learned

1. Linux permissions control access to files and directories for the owner, group, and others.
2. The chmod command can modify permissions using symbolic or numeric notation.
3. Execute permission is required to run shell scripts, while read and write permissions control viewing and modifying file contents.
