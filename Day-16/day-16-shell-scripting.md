# Day 16 – Shell Scripting Basics

# Task 1: Your First Script

## What is Shebang?

`#!/bin/bash` tells Linux which interpreter should execute the script.

### What happens if you remove the shebang line?

The system may not know which interpreter to use. The script might fail or run using the current shell, which can lead to unexpected behavior.

### hello.sh

**Script**

```
#!/bin/bash

echo "Hello DevOps"
```

**Commands**

```
chmod +x hello.sh
./hello.sh
```

**Output**

```
Hello DevOps
```

---

# Task 2: Variables

## What is a Variable?

A variable stores data that can be reused throughout a script.

### variables.sh

**Script**

```
#!/bin/bash

NAME="Parthavi"
ROLE="Cloud Engineer"

echo "Hello, I am $NAME and I am a $ROLE"
```

**Output**

```
Hello, I am Parthavi and I am a Cloud Engineer
```

---

## Single Quotes vs Double Quotes

### Single Quotes

Variables are not expanded.

**Example**

```
NAME="Parthavi"
echo 'Hello, I am $NAME'
```

**Output**

```
Hello, I am $NAME
```

### Double Quotes

Variables are expanded.

**Example**

```
NAME="Parthavi"
echo "Hello, I am $NAME"
```

**Output**

```
Hello, I am Parthavi
```

---

# Task 3: User Input with read

## What is read?

The `read` command accepts input from the user and stores it in a variable.

### greet.sh

**Script**

```
#!/bin/bash

read -p "Enter your name: " name
read -p "Enter your favourite tool: " tool

echo "Hello $name, your favourite tool is $tool"
```

**Output**

```
Enter your name: Parthavi
Enter your favourite tool: Docker
Hello Parthavi, your favourite tool is Docker
```

---

# Task 4: If-Else Conditions

## What is if-else?

It allows a script to make decisions based on conditions.

### check_number.sh

**Script**

```
#!/bin/bash

read -p "Enter Number: " number

if [[ $number -gt 0 ]]; then
    echo "$number is positive."
elif [[ $number -lt 0 ]]; then
    echo "$number is negative."
else
    echo "$number is zero."
fi
```

**Output**

```
Enter Number: 5
5 is positive.

Enter Number: -3
-3 is negative.

Enter Number: 0
0 is zero.
```

---

## What does -f mean?

`-f` checks whether a file exists and is a regular file.

### file_check.sh

**Script**

```
#!/bin/bash

read -p "Enter filename: " filename

if [[ -f "$filename" ]]; then
    echo "The file '$filename' exists."
else
    echo "The file '$filename' does not exist."
fi
```

**Output**

```
Enter filename: notes.txt
The file 'notes.txt' exists.

Enter filename: file.txt
The file 'file.txt' does not exist.
```

---

# Task 5: Combine It All

## server_check.sh

**Script**

```
#!/bin/bash

service="sshd"

read -p "Do you want to check the status? (y/n): " choice

if [ "$choice" = "y" ]; then

    if systemctl is-active --quiet "$service"; then
        echo "$service is active."
    else
        echo "$service is not active."
    fi

    systemctl status "$service"

elif [ "$choice" = "n" ]; then
    echo "Skipped."

else
    echo "Invalid input. Please enter y or n."
fi
```

**Output**

```
Do you want to check the status? (y/n): y
sshd is active.

Do you want to check the status? (y/n): n
Skipped.
```

---

# Key Commands Learned

```
chmod +x filename.sh
./filename.sh
read
echo
if
elif
else
fi
```

---

# What I Learned

* Shebang defines the interpreter used to run a script.
* Variables store reusable values.
* read accepts user input.
* if-else helps make decisions in scripts.
* Shell scripts can automate system administration tasks.
