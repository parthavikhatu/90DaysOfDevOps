# Day 11 Summary – File Ownership Challenge

## Key Concepts Learned

### 1. File Ownership
- Every file has an owner and a group.
- Owner has primary control over the file.
- Group allows multiple users to share access.

Example:
-rw-r----- 1 ubuntu ubuntu 12 May 31 notes.txt
            |      |
          owner  group

### 2. chown (Change Owner)
Used to change the owner of a file or directory.

Commands:
sudo chown tokyo devops-file.txt
sudo chown berlin devops-file.txt

### 3. chgrp (Change Group)
Used to change the group ownership.

Command:
sudo chgrp heist-team team-notes.txt

### 4. Change Owner and Group Together
Use user:group format.

Command:
sudo chown professor:heist-team project-config.yaml

### 5. Recursive Ownership (-R)
Changes ownership for a directory and everything inside it.

Command:
sudo chown -R professor:planners heist-project/

## Files and Directories Created

Files:
- devops-file.txt
- team-notes.txt
- project-config.yaml
- access-codes.txt
- blueprints.pdf
- escape-plan.txt
- gold.txt
- strategy.conf

Directories:
- app-logs/
- heist-project/
- bank-heist/

## Users Created

- tokyo
- berlin
- professor
- nairobi

## Groups Created

- heist-team
- planners
- vault-team
- tech-team

## Important Commands

| Command | Purpose |
|----------|----------|
| ls -l | View ownership and permissions |
| chown | Change owner |
| chgrp | Change group |
| chown user:group file | Change owner and group together |
| chown -R user:group dir | Recursive ownership change |
| useradd | Create user |
| groupadd | Create group |

## DevOps Real-World Use Cases

| Scenario | Why Ownership Matters |
|-----------|----------------------|
| Jenkins | Jenkins user must own build workspace |
| Nginx | Web server needs access to logs and web files |
| Docker Volumes | Containers need correct file ownership |
| Shared Team Folders | Multiple users access via groups |
| CI/CD Deployments | Deployment user requires file ownership |

## Quick Revision

- Owner = User who controls the file.
- Group = Users sharing access.
- chown = Change owner.
- chgrp = Change group.
- -R = Apply changes recursively.
- ls -l = Check ownership and permissions.

## Interview One-Liner

File ownership in Linux controls who can access and manage files. DevOps engineers frequently use chown, chgrp, and recursive ownership changes to manage Jenkins workspaces, Docker volumes, application logs, and deployment directories.
