# Day 38 – YAML Basics

## Objective

Learn YAML syntax, create YAML files manually, understand indentation rules, work with lists and nested objects, use multi-line strings, and validate YAML files.

---

## Task 1: Key-Value Pairs

### person.yaml

```yaml
name: Parthavi Khatu
role: DevOps Engineer
experience_years: 1
learning: true
```

### Verification

```bash
cat person.yaml
```

Output:

```yaml
name: Parthavi Khatu
role: DevOps Engineer
experience_years: 1
learning: true
```

---

## Task 2: Lists

Updated `person.yaml`

```yaml
name: Parthavi Khatu
role: DevOps Engineer
experience_years: 1
learning: true

tools:
  - Docker
  - Kubernetes
  - Jenkins
  - AWS
  - Git

hobbies: [Reading, Yoga, Coding]
```

### Two Ways to Write Lists in YAML

#### Block Style

```yaml
tools:
  - Docker
  - Kubernetes
  - Jenkins
```

#### Inline Style

```yaml
tools: [Docker, Kubernetes, Jenkins]
```

---

## Task 3: Nested Objects

### server.yaml

```yaml
server:
  name: web-server
  ip: 192.168.1.10
  port: 8080

database:
  host: localhost
  name: mydb

  credentials:
    user: admin
    password: admin123
```

### Tab Error Test

Incorrect:

```yaml
server:
	name: web-server
```

Error:

```text
found character '\t' that cannot start any token
```

YAML supports spaces only and does not allow tabs.

---

## Task 4: Multi-Line Strings

Updated `server.yaml`

```yaml
server:
  name: web-server
  ip: 192.168.1.10
  port: 8080

database:
  host: localhost
  name: mydb

  credentials:
    user: admin
    password: admin123

startup_script_preserve: |
  #!/bin/bash
  echo "Starting application"
  systemctl start nginx

startup_script_fold: >
  This startup script installs
  dependencies and starts
  the application.
```

### Difference Between `|` and `>`

#### `|` Literal Block

Preserves line breaks exactly.

Example Output:

```text
#!/bin/bash
echo "Starting application"
systemctl start nginx
```

Used for:

* Shell scripts
* Configuration files
* Certificates
* Multi-line commands

#### `>` Folded Block

Converts line breaks into spaces.

Example Output:

```text
This startup script installs dependencies and starts the application.
```

Used for:

* Documentation
* Descriptions
* Long text fields

---

## Task 5: YAML Validation

### Install yamllint

```bash
sudo apt update
sudo apt install yamllint -y
```

### Validate Files

```bash
yamllint person.yaml
yamllint server.yaml
```

No output means the files are valid.

### Broken Indentation Example

```yaml
tools:
 - Docker
  - Jenkins
```

Validation Error:

```text
syntax error: expected <block end>, but found '<block sequence start>'
```

Fixed Version:

```yaml
tools:
  - Docker
  - Jenkins
```

---

## Task 6: Spot the Difference

### Correct

```yaml
name: devops

tools:
  - docker
  - kubernetes
```

### Broken

```yaml
name: devops

tools:
- docker
  - kubernetes
```

### Issue

The list items are not consistently indented under the `tools` key. YAML relies on indentation to define structure, so improper spacing can cause parsing errors or unexpected behavior.

Correct Version:

```yaml
tools:
  - docker
  - kubernetes
```

---

## What I Learned

1. YAML uses spaces for indentation and does not allow tabs.
2. Lists can be written in block style (`- item`) or inline style (`[item1, item2]`).
3. The `|` operator preserves line breaks, while the `>` operator folds multiple lines into a single line.

---

## Conclusion

This exercise helped me understand the fundamentals of YAML, including key-value pairs, lists, nested objects, multi-line strings, and validation. These concepts are essential for working with DevOps tools such as Docker Compose, Kubernetes, GitHub Actions, Jenkins pipelines, and Ansible.
