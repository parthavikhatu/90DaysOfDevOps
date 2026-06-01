# Day 16 – Shell Scripting Basics

## hello.sh

**Script**

```
#!/bin/bash
echo "Hello DevOps"
```

**Output**

```
Hello DevOps
```

---

## variables.sh

**Script**

```
#!/bin/bash

Name="Parthavi"
Role="Cloud Engineer"

echo "Hello, I am $Name and my role is $Role"
```

**Output**

```
Hello, I am Parthavi and my role is Cloud Engineer
```

---

## user_input.sh

**Script**

```
#!/bin/bash

read -p "Name: " name
read -p "Tool: " tool

echo "Hello, I am $name and my favourite tool is $tool"
```

**Output**

```
Name: Parthavi
Tool: Docker
Hello, I am Parthavi and my favourite tool is Docker
```

---

## check_number.sh

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
Enter Number: 3
3 is positive.

Enter Number: -9
-9 is negative.

Enter Number: 0
0 is zero.
```

---

## file_check.sh

**Script**

```
#!/bin/bash

read -p "Enter the filename: " filename

if [[ -f "$filename" ]]; then
    echo "The file '$filename' exists."
else
    echo "The file '$filename' does not exist."
fi
```

**Output**

```
Enter the filename: notes.txt
The file 'notes.txt' exists.

Enter the filename: file.txt
The file 'file.txt' does not exist.
```

---

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

Do you want to check the status? (y/n): x
Invalid input. Please enter y or n.
```
