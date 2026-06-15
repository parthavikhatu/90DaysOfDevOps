# Day 30 – Docker Images & Container Lifecycle

## Objective

Understand how Docker images and containers work, learn image layers and caching, and practice the complete container lifecycle.

---

# Task 1: Docker Images

## Pull Images from Docker Hub

```bash
docker pull nginx
docker pull ubuntu
docker pull alpine
```

## List All Images

```bash
docker images
```

### Observations

| Image  | Approximate Size |
| ------ | ---------------- |
| nginx  | ~190 MB          |
| ubuntu | ~80 MB           |
| alpine | ~8 MB            |

### Ubuntu vs Alpine

Ubuntu is a full-featured Linux distribution that includes many utilities and packages.

Alpine is designed specifically for containers. It uses BusyBox and musl libc, making it lightweight and secure.

Therefore, Alpine is significantly smaller than Ubuntu.

## Inspect an Image

```bash
docker image inspect nginx
```

### Information Available

* Image ID
* Repository Tags
* Creation Date
* Architecture
* Environment Variables
* Entrypoint
* Working Directory
* Layers
* Image Size

## Remove an Image

```bash
docker rmi ubuntu
```

---

# Task 2: Image Layers

## View Image History

```bash
docker image history nginx
```

### Observation

The output displays multiple layers that make up the image.

Some layers show sizes because they add files or packages.

Some layers show 0B because they only contain metadata instructions such as CMD, ENV, or EXPOSE.

## What Are Docker Layers?

Docker images are built using multiple read-only layers.

Example:

```dockerfile
FROM ubuntu
RUN apt update
RUN apt install nginx -y
COPY . /app
```

Layers created:

1. Ubuntu Base Layer
2. apt update Layer
3. nginx Installation Layer
4. Application Files Layer

## Why Docker Uses Layers

* Faster image builds
* Reuse existing layers
* Efficient storage usage
* Faster image distribution
* Supports caching

---

# Task 3: Container Lifecycle

## Create Container

```bash
docker create --name test-container ubuntu
```

State: Created

## Start Container

```bash
docker start test-container
```

State: Running

## Pause Container

```bash
docker pause test-container
```

State: Paused

## Unpause Container

```bash
docker unpause test-container
```

State: Running

## Stop Container

```bash
docker stop test-container
```

State: Exited

## Restart Container

```bash
docker restart test-container
```

State: Running

## Kill Container

```bash
docker kill test-container
```

State: Exited

## Remove Container

```bash
docker rm test-container
```

State: Deleted

### Lifecycle Diagram

```text
Create
  ↓
Created
  ↓
Start
  ↓
Running
 ↙     ↘
Pause  Stop
 ↓      ↓
Paused Exited
 ↓      ↓
Unpause Restart
 ↓      ↓
Running
  ↓
Kill
  ↓
Exited
  ↓
Remove
  ↓
Deleted
```

---

# Task 4: Working with Running Containers

## Run Nginx Container in Detached Mode

```bash
docker run -d --name my-nginx -p 8080:80 nginx
```

Verify:

```bash
docker ps
```

## View Logs

```bash
docker logs my-nginx
```

## Follow Logs in Real Time

```bash
docker logs -f my-nginx
```

Exit:

```bash
Ctrl + C
```

## Enter Running Container

```bash
docker exec -it my-nginx bash
```

If bash is unavailable:

```bash
docker exec -it my-nginx sh
```

## Run a Single Command

```bash
docker exec my-nginx ls /
```

## Inspect Container

```bash
docker inspect my-nginx
```

### Useful Information Found

* Container ID
* IP Address
* Port Mappings
* Mounts
* Network Settings
* Environment Variables

---

# Task 5: Cleanup

## Stop All Running Containers

```bash
docker stop $(docker ps -q)
```

## Remove All Containers

```bash
docker rm $(docker ps -aq)
```

## Remove Unused Images

```bash
docker image prune -a
```

## Check Docker Disk Usage

```bash
docker system df
```

## Remove All Unused Docker Resources

```bash
docker system prune -a
```

---

# Key Learnings

* Docker Images are templates used to create containers.
* Containers are running instances of images.
* Images are built using multiple layers.
* Layer caching speeds up image builds.
* Containers move through different lifecycle states such as Created, Running, Paused, Exited, and Deleted.
* Docker provides commands to inspect, manage, and troubleshoot containers.
* Cleanup commands help reclaim disk space and maintain a healthy Docker environment.

---

# Screenshots Included

* docker images
* docker image inspect nginx
* docker image history nginx
* docker ps -a during lifecycle operations
* docker logs my-nginx
* docker inspect my-nginx
* docker system df

## Conclusion

Today I learned how Docker images and containers work internally, how image layers improve efficiency through caching, and how to manage containers throughout their complete lifecycle. I also practiced inspecting images, viewing logs, and performing Docker cleanup operations.
