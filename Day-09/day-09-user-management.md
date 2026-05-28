# Day 09 Challenge

## Users & Groups Created

### Users
- tokyo
- berlin
- professor
- nairobi

### Groups
- developers
- admins
- project-team

---

## Group Assignments

| User | Groups |
|------|--------|
| tokyo | developers, project-team |
| berlin | developers, admins |
| professor | admins |
| nairobi | project-team |

---

## Directories Created

| Directory | Group | Permissions |
|-----------|------|-------------|
| /opt/dev-project | developers | 775 |
| /opt/team-workspace | project-team | 775 |

---

## Commands Used

```bash
sudo useradd -m tokyo
sudo useradd -m berlin
sudo useradd -m professor
sudo passwd tokyo
sudo passwd berlin
sudo passwd professor

sudo groupadd developers
sudo groupadd admins

sudo usermod -aG developers tokyo
sudo usermod -aG developers berlin
sudo usermod -aG admins berlin
sudo usermod -aG admins professor

groups tokyo
groups berlin
groups professor

sudo mkdir /opt/dev-project
sudo chgrp developers /opt/dev-project
sudo chmod 775 /opt/dev-project

sudo -u tokyo touch /opt/dev-project/tokyo.txt
sudo -u berlin touch /opt/dev-project/berlin.txt

sudo useradd -m nairobi
sudo passwd nairobi

sudo groupadd project-team

sudo usermod -aG project-team nairobi
sudo usermod -aG project-team tokyo

sudo mkdir /opt/team-workspace
sudo chgrp project-team /opt/team-workspace
sudo chmod 775 /opt/team-workspace

sudo -u nairobi touch /opt/team-workspace/test.txt
```

---

## What I Learned

1. How to create Linux users and groups
2. How Linux permissions work using chmod
3. How shared group access works in Linux


Check Permissions
ls -ld /opt/dev-project
