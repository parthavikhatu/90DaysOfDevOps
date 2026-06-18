# Day 32 – Docker Volumes & Networking

## Objective

Learn how Docker handles:

* Data persistence using Volumes
* Sharing files using Bind Mounts
* Container communication using Networks

Containers are ephemeral by default. Any data stored inside a container is lost when the container is removed. Docker Volumes solve this problem. Docker Networks allow containers to communicate with each other.

---

# Task 1: The Problem – Data Loss Without Volumes

## Run PostgreSQL Container

```bash
docker run -d \
--name postgres-db \
-e POSTGRES_PASSWORD=admin123 \
-p 5432:5432 \
postgres
```

## Create Data

Connect to PostgreSQL:

```bash
docker exec -it postgres-db psql -U postgres
```

Create a database and table:

```sql
CREATE DATABASE testdb;
\c testdb

CREATE TABLE employees (
id SERIAL PRIMARY KEY,
name VARCHAR(50)
);

INSERT INTO employees(name)
VALUES ('Parthavi');

SELECT * FROM employees;
```

## Remove Container

```bash
docker stop postgres-db
docker rm postgres-db
```

## Create New Container

```bash
docker run -d \
--name postgres-db-new \
-e POSTGRES_PASSWORD=admin123 \
-p 5432:5432 \
postgres
```

### Observation

The database and table no longer exist.

### Reason

Container data is stored in the container's writable layer. When the container is removed, the writable layer is also deleted.

---

# Task 2: Named Volumes

## Create a Volume

```bash
docker volume create postgres-data
```

Verify:

```bash
docker volume ls
```

## Run PostgreSQL with Volume

```bash
docker run -d \
--name postgres-vol \
-e POSTGRES_PASSWORD=admin123 \
-v postgres-data:/var/lib/postgresql/data \
-p 5432:5432 \
postgres
```

## Create Data

```bash
docker exec -it postgres-vol psql -U postgres
```

```sql
CREATE DATABASE companydb;
\c companydb

CREATE TABLE staff (
id SERIAL PRIMARY KEY,
name VARCHAR(50)
);

INSERT INTO staff(name)
VALUES ('Parthavi');
```

## Remove Container

```bash
docker stop postgres-vol
docker rm postgres-vol
```

## Start New Container Using Same Volume

```bash
docker run -d \
--name postgres-vol-new \
-e POSTGRES_PASSWORD=admin123 \
-v postgres-data:/var/lib/postgresql/data \
-p 5432:5432 \
postgres
```

### Verification

```bash
docker exec -it postgres-vol-new psql -U postgres
```

```sql
\c companydb
SELECT * FROM staff;
```

### Observation

The data still exists.

### Reason

Docker Volumes are stored independently of containers.

---

## Inspect Volume

```bash
docker volume ls
docker volume inspect postgres-data
```

---

# Task 3: Bind Mounts

## Create Local Folder

```bash
mkdir nginx-site
cd nginx-site
```

Create an HTML file:

```html
<h1>Hello from Host Machine</h1>
```

## Run Nginx with Bind Mount

```bash
docker run -d \
--name nginx-bind \
-p 8080:80 \
-v $(pwd):/usr/share/nginx/html \
nginx
```

Open:

```text
http://localhost:8080
```

## Modify index.html

```html
<h1>Docker Bind Mount Works!</h1>
```

Refresh the browser.

### Observation

Changes appear immediately without restarting the container.

---

# Named Volume vs Bind Mount

| Feature          | Named Volume        | Bind Mount              |
| ---------------- | ------------------- | ----------------------- |
| Managed By       | Docker              | Host OS                 |
| Storage Location | Docker Storage Area | Any Host Directory      |
| Best Use Case    | Databases           | Application Source Code |
| Portability      | High                | Low                     |
| Security         | Better              | Direct Host Access      |

---

# Task 4: Docker Networking Basics

## List Networks

```bash
docker network ls
```

Example:

```text
bridge
host
none
```

## Inspect Default Bridge Network

```bash
docker network inspect bridge
```

## Run Two Containers

```bash
docker run -dit --name ubuntu1 ubuntu
docker run -dit --name ubuntu2 ubuntu
```

Install ping utility if needed:

```bash
apt update
apt install iputils-ping -y
```

## Ping by Container Name

```bash
docker exec -it ubuntu1 ping ubuntu2
```

### Result

Name resolution fails.

## Ping by IP Address

Find IP:

```bash
docker inspect ubuntu2
```

Ping:

```bash
docker exec -it ubuntu1 ping <container-ip>
```

### Result

Ping succeeds.

### Observation

Default bridge network does not automatically provide DNS-based name resolution.

---

# Task 5: Custom Networks

## Create Custom Network

```bash
docker network create my-app-net
```

## Run Containers on Custom Network

```bash
docker run -dit \
--name app1 \
--network my-app-net \
ubuntu
```

```bash
docker run -dit \
--name app2 \
--network my-app-net \
ubuntu
```

## Test Communication

```bash
docker exec -it app1 ping app2
```

### Result

Ping succeeds using the container name.

### Why?

User-defined bridge networks include Docker's built-in DNS service. Containers can discover each other using container names.

---

# Task 6: Volumes + Networking Together

## Create Network

```bash
docker network create my-db-network
```

## Create Volume

```bash
docker volume create pgdata
```

## Run PostgreSQL

```bash
docker run -d \
--name postgres-final \
--network my-db-network \
-e POSTGRES_PASSWORD=admin123 \
-v pgdata:/var/lib/postgresql/data \
postgres
```

## Run Application Container

```bash
docker run -dit \
--name app-final \
--network my-db-network \
ubuntu
```

## Install PostgreSQL Client

```bash
apt update
apt install postgresql-client -y
```

## Connect Using Container Name

```bash
psql -h postgres-final -U postgres
```

### Verification

The application container successfully connects to PostgreSQL using the container name instead of an IP address.

---

# Key Learnings

* Containers are ephemeral and lose data when removed.
* Docker Volumes provide persistent storage.
* Bind Mounts allow containers to access files directly from the host.
* Default Bridge Network supports communication via IP addresses.
* Custom Bridge Networks provide DNS-based container discovery.
* Volumes and Networks are essential building blocks for real-world Docker applications.

---

# Commands Summary

```bash
# Volumes
docker volume create myvolume
docker volume ls
docker volume inspect myvolume

# Bind Mount
docker run -v $(pwd):/container/path image

# Networks
docker network ls
docker network inspect bridge
docker network create my-app-net

# Run on Custom Network
docker run --network my-app-net image

# Ping Container
docker exec -it container1 ping container2
```

## Conclusion

In this lab, I learned how Docker handles persistent storage through volumes and how containers communicate using Docker networks. I explored named volumes, bind mounts, default bridge networking, custom bridge networking, and combined both storage and networking to simulate a real-world application setup.
