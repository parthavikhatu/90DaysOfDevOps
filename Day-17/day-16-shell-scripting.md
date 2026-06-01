# hello.sh

### Code

```bash
#!/bin/bash

echo "Hello DevOps"
```

### Output

```text
Hello DevOps
```

---

# variables.sh

### Code

```bash
#!/bin/bash

Name="Parthavi"
Role="Cloud Engineer"

echo "Hello, I am $Name and my role is $Role"
```

### Output

```text
Hello, I am Parthavi and my role is Cloud Engineer
```

---

# user_input.sh

### Code

```bash
#!/bin/bash

read -p "Name: " name
read -p "Tool: " tool

echo "Hello, I am $name and my favourite tool is $tool"
```

### Output

```text
Name: Parthavi
Tool: Docker
Hello, I am Parthavi and my favourite tool is Docker
```

---

# check_number.sh

### Code

```bash
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

### Output

```text
Enter Number: 3
3 is positive.
```

```text
Enter Number: -9
-9 is negative.
```

```text
Enter Number: 0
0 is zero.
```

---

# file_check.sh

### Code

```bash
#!/bin/bash

read -p "Enter the filename: " filename

if [[ -f "$filename" ]]; then
    echo "The file '$filename' exists."
else
    echo "The file '$filename' does not exist."
fi
```

### Output

```text
Enter the filename: notes.txt
The file 'notes.txt' exists.
```

```text
Enter the filename: file.txt
The file 'file.txt' does not exist.
```

---

# server_check.sh

### Code

```bash
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

### Output

```text
Do you want to check the status? (y/n): y
sshd is active.
```

```text
Do you want to check the status? (y/n): n
Skipped.
```

```text
Do you want to check the status? (y/n): x
Invalid input. Please enter y or n.
```
