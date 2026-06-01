# Day 17 – Shell Scripting: Loops, Arguments & Error Handling

## Objective

Learn how to:

* Use `for` loops
* Use `while` loops
* Work with command-line arguments
* Automate package installation
* Handle errors in shell scripts

---

# Task 1: For Loop

## What is a For Loop?

A `for` loop executes a block of code repeatedly for each item in a list.

### for_loop.sh

**Script**

```
#!/bin/bash

for fruit in Apple Banana Mango Orange Grapes
do
    echo "$fruit"
done
```

**Output**

```
Apple
Banana
Mango
Orange
Grapes
```

---

### count.sh

**Script**

```
#!/bin/bash

for i in {1..10}
do
    echo "$i"
done
```

**Output**

```
1
2
3
4
5
6
7
8
9
10
```

---

# Task 2: While Loop

## What is a While Loop?

A `while` loop continues running as long as a condition remains true.

### countdown.sh

**Script**

```
#!/bin/bash

read -p "Enter a number: " num

while [ $num -ge 0 ]
do
    echo "$num"
    num=$((num-1))
done

echo "Done!"
```

**Output**

```
Enter a number: 5
5
4
3
2
1
0
Done!
```

---

# Task 3: Command-Line Arguments

## What are Command-Line Arguments?

Arguments are values passed to a script when it is executed.

### Important Variables

| Variable | Description         |
| -------- | ------------------- |
| $0       | Script name         |
| $1       | First argument      |
| $2       | Second argument     |
| $#       | Number of arguments |
| $@       | All arguments       |

---

### greet.sh

**Script**

```
#!/bin/bash

if [ $# -eq 0 ]; then
    echo "Usage: ./greet.sh <name>"
else
    echo "Hello, $1!"
fi
```

**Output**

```
./greet.sh Parthavi

Hello, Parthavi!
```

**Output (No Argument)**

```
./greet.sh

Usage: ./greet.sh <name>
```

---

### args_demo.sh

**Script**

```
#!/bin/bash

echo "Script Name: $0"
echo "Total Arguments: $#"
echo "All Arguments: $@"
```

**Output**

```
./args_demo.sh aws docker kubernetes

Script Name: ./args_demo.sh
Total Arguments: 3
All Arguments: aws docker kubernetes
```

---

# Task 4: Install Packages via Script

## Why Check for Root User?

Package installation requires administrative privileges.

### install_packages.sh

**Script**

```
#!/bin/bash

if [ "$EUID" -ne 0 ]; then
    echo "Please run as root."
    exit 1
fi

packages="nginx curl wget"

for package in $packages
do
    if dpkg -s $package &>/dev/null; then
        echo "$package is already installed."
    else
        echo "Installing $package..."
        apt install -y $package
    fi
done
```

**Output**

```
nginx is already installed.
curl is already installed.
Installing wget...
```

**Output (Non-Root User)**

```
Please run as root.
```

---

# Task 5: Error Handling

## What is set -e?

`set -e` causes the script to exit immediately if any command fails.

---

## What is || ?

The OR operator (`||`) runs the command on the right if the command on the left fails.

Example:

```
mkdir /tmp/devops-test || echo "Directory already exists"
```

---

### safe_script.sh

**Script**

```
#!/bin/bash

set -e

mkdir /tmp/devops-test || echo "Directory already exists"

cd /tmp/devops-test || {
    echo "Failed to enter directory"
    exit 1
}

touch test.txt || {
    echo "Failed to create file"
    exit 1
}

echo "Script completed successfully."
```

**Output**

```
Script completed successfully.
```

**Output (Directory Exists)**

```
Directory already exists
Script completed successfully.
```

---

# Key Commands Learned

```
for
while
read
$0
$1
$#
$@
set -e
||
dpkg -s
apt install
```

---

# Interview Questions

### What is the difference between a for loop and a while loop?

* A `for` loop runs for a predefined list or range.
* A `while` loop runs until a condition becomes false.

### What does $1 represent?

The first command-line argument passed to a script.

### What does $# represent?

The total number of arguments passed to a script.

### What does $@ represent?

All arguments passed to a script.

### Why use set -e?

To stop script execution immediately when a command fails.

### Why check for root before installing packages?

Package installation requires administrative privileges.

### What does || do in shell scripting?

Executes the second command only if the first command fails.

---

# What I Learned

* Automating repetitive tasks using loops.
* Accepting user input through command-line arguments.
* Installing packages automatically using scripts.
* Handling failures gracefully using `set -e` and `||`.
* Writing safer and more reliable shell scripts.
