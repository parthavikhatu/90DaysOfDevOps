# Day 29 – Introduction to Docker

## Objective

Learn the fundamentals of Docker, understand containerization, install Docker, and run your first containers.

---

# Task 1: What is Docker?

## What is a Container?

A container is a lightweight, standalone package that contains everything needed to run an application, including:

* Application code
* Runtime
* Libraries
* Dependencies
* Configuration files

Containers ensure that applications run consistently across different environments.

### Why Do We Need Containers?

Before containers:

* Applications worked on one machine but failed on another.
* Dependency conflicts were common.
* Environment setup took a lot of time.

Containers solve these problems by packaging the application and its dependencies together.

### Benefits of Containers

* Lightweight
* Fast startup
* Portable
* Consistent environments
* Easy deployment
* Better resource utilization

---

# Containers vs Virtual Machines

| Feature              | Containers  | Virtual Machines |
| -------------------- | ----------- | ---------------- |
| Virtualization Level | OS Level    | Hardware Level   |
| Size                 | MBs         | GBs              |
| Startup Time         | Seconds     | Minutes          |
| Performance          | Near Native | Slower           |
| OS Included          | No          | Yes              |
| Resource Usage       | Low         | High             |

## Virtual Machine Architecture

```text
Hardware
│
Hypervisor
│
├── VM1 (Guest OS + App)
├── VM2 (Guest OS + App)
└── VM3 (Guest OS + App)
```

## Container Architecture

```text
Hardware
│
Host OS
│
Docker Engine
│
├── Container 1
├── Container 2
└── Container 3
```

Containers share the host operating system kernel, making them lightweight.

---

# Docker Architecture

Docker follows a Client-Server architecture.

## Components

### Docker Client

The command-line interface used by users.

Examples:

```bash
docker run
docker ps
docker images
```

---

### Docker Daemon (dockerd)

Background service that:

* Builds images
* Runs containers
* Manages networks
* Manages volumes

---

### Docker Images

Read-only templates used to create containers.

Examples:

```text
nginx
ubuntu
mysql
redis
```

---

### Docker Containers

Running instances of Docker images.

Example:

```bash
docker run nginx
```

Creates a container from the nginx image.

---

### Docker Registry

Storage location for Docker images.

Popular registry:

Docker Hub

https://hub.docker.com

---

# Docker Architecture Diagram

```text
+-------------------+
|   Docker Client   |
+---------+---------+
          |
          |
          V
+-------------------+
|  Docker Daemon    |
+---------+---------+
          |
  -----------------
  |               |
  V               V

Images      Containers

          ^
          |
          |
+-------------------+
|   Docker Hub      |
|    Registry       |
+-------------------+
```

Flow:

1. User runs docker command.
2. Docker Client sends request.
3. Docker Daemon processes request.
4. Image is pulled from Docker Hub if unavailable locally.
5. Container is created and started.

---

# Task 2: Install Docker

## Verify Installation

```bash
docker --version
```

Example Output:

```text
Docker version 28.x.x
```

---

## Check Docker Service

```bash
sudo systemctl status docker
```

---

## Run Hello World Container

```bash
docker run hello-world
```

### What Happened?

1. Docker checked local images.
2. Image not found locally.
3. Pulled image from Docker Hub.
4. Created container.
5. Executed application.
6. Displayed success message.

Output confirms Docker is working correctly.

---

# Task 3: Run Real Containers

## Run Nginx Container

```bash
docker run -d -p 8080:80 nginx
```

Explanation:

* d = detached mode
* p = port mapping
* 8080 = host port
* 80 = container port

---

## Verify Running Container

```bash
docker ps
```

Sample Output:

```text
CONTAINER ID   IMAGE   STATUS
abcd1234       nginx   Up 2 minutes
```

---

## Access Nginx

Browser:

```text
http://localhost:8080
```

You should see:

```text
Welcome to nginx!
```

---

## Run Ubuntu Container

```bash
docker run -it ubuntu bash
```

Explanation:

* i = interactive
* t = terminal
* bash = shell

---

## Check Ubuntu Version

Inside Container:

```bash
cat /etc/os-release
```

---

## Exit Container

```bash
exit
```

---

## List Running Containers

```bash
docker ps
```

---

## List All Containers

```bash
docker ps -a
```

---

## Stop Container

```bash
docker stop <container_id>
```

Example:

```bash
docker stop abcd1234
```

---

## Remove Container

```bash
docker rm <container_id>
```

Example:

```bash
docker rm abcd1234
```

---

# Task 4: Explore Docker Features

## Detached Mode

Run container in background:

```bash
docker run -d nginx
```

### Difference

Interactive Mode:

```bash
docker run -it ubuntu bash
```

Detached Mode:

```bash
docker run -d nginx
```

Interactive mode gives terminal access.

Detached mode runs in background.

---

## Give Container Custom Name

```bash
docker run -d --name mynginx nginx
```

Verify:

```bash
docker ps
```

Output:

```text
mynginx
```

---

## Port Mapping

```bash
docker run -d -p 8080:80 nginx
```

Meaning:

```text
Host Port 8080
      ↓
Container Port 80
```

Access:

```text
http://localhost:8080
```

---

## Check Logs

```bash
docker logs mynginx
```

Shows container output and application logs.

---

## Execute Command Inside Running Container

```bash
docker exec -it mynginx bash
```

If bash unavailable:

```bash
docker exec -it mynginx sh
```

Example:

```bash
ls
pwd
whoami
```

Exit:

```bash
exit
```

---

# Common Docker Commands Cheat Sheet

## Images

```bash
docker images
docker pull nginx
docker rmi nginx
```

## Containers

```bash
docker ps
docker ps -a
docker run nginx
docker stop container_id
docker start container_id
docker restart container_id
docker rm container_id
```

## Logs

```bash
docker logs container_name
```

## Execute Commands

```bash
docker exec -it container_name bash
```

## Port Mapping

```bash
docker run -p 8080:80 nginx
```

## Detached Mode

```bash
docker run -d nginx
```

## Custom Name

```bash
docker run --name mycontainer nginx
```

---

# Key Learnings

* Docker is a containerization platform.
* Containers package applications and dependencies together.
* Containers are lightweight compared to VMs.
* Docker architecture consists of Client, Daemon, Images, Containers, and Registry.
* Docker Hub is the default image registry.
* Containers can run in interactive or detached mode.
* Port mapping exposes container services to users.
* Docker logs help troubleshoot applications.
* docker exec allows access inside running containers.

---

# Conclusion

Today I learned the fundamentals of Docker, understood the difference between containers and virtual machines, explored Docker architecture, installed Docker, ran my first containers, and practiced essential Docker commands. This forms the foundation for learning Docker Images, Volumes, Networking, Docker Compose, and Kubernetes in the upcoming days.
