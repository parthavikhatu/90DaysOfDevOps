# Docker Cheat Sheet

## Quick-Fire Questions

### 1. What is the difference between an image and a container?

* **Image:** A read-only template containing application code, dependencies, and configuration.
* **Container:** A running instance of an image.

Example:

```bash
docker run nginx
```

Creates a container from the nginx image.

---

### 2. What happens to data inside a container when you remove it?

Data stored inside the container's writable layer is deleted when the container is removed.

To persist data, use Docker Volumes:

```bash
docker volume create myvolume
```

---

### 3. How do two containers on the same custom network communicate?

Containers communicate using container names as hostnames.

```bash
docker network create mynet

docker run -d --name web --network mynet nginx
docker run -it --name client --network mynet busybox
```

Inside `client`:

```bash
ping web
```

---

### 4. What does `docker compose down -v` do differently from `docker compose down`?

| Command                  | Action                                    |
| ------------------------ | ----------------------------------------- |
| `docker compose down`    | Stops and removes containers and networks |
| `docker compose down -v` | Also removes associated volumes           |

---

### 5. Why are multi-stage builds useful?

Multi-stage builds reduce image size by separating build dependencies from runtime dependencies.

Benefits:

* Smaller images
* Faster deployments
* Improved security
* Reduced attack surface

---

### 6. What is the difference between COPY and ADD?

| COPY                           | ADD                                           |
| ------------------------------ | --------------------------------------------- |
| Copies local files/directories | Copies files and supports URLs/tar extraction |
| Preferred for most use cases   | Use only when extra functionality is needed   |

Example:

```dockerfile
COPY app.py /app/
```

```dockerfile
ADD archive.tar.gz /app/
```

---

### 7. What does `-p 8080:80` mean?

```bash
docker run -p 8080:80 nginx
```

Maps:

* Host Port: 8080
* Container Port: 80

Access application via:

```text
http://localhost:8080
```

---

### 8. How do you check how much disk space Docker is using?

```bash
docker system df
```

Detailed view:

```bash
docker system df -v
```

---

# Container Commands

| Command           | Description                |
| ----------------- | -------------------------- |
| `docker run`      | Create and start container |
| `docker ps`       | List running containers    |
| `docker ps -a`    | List all containers        |
| `docker stop`     | Stop container             |
| `docker start`    | Start container            |
| `docker restart`  | Restart container          |
| `docker rm`       | Remove container           |
| `docker exec -it` | Access container shell     |
| `docker logs`     | View container logs        |
| `docker inspect`  | Detailed container info    |

---

# Image Commands

| Command                   | Description       |
| ------------------------- | ----------------- |
| `docker build -t image .` | Build image       |
| `docker images`           | List images       |
| `docker pull`             | Download image    |
| `docker push`             | Upload image      |
| `docker tag`              | Create image tag  |
| `docker rmi`              | Remove image      |
| `docker history`          | Show image layers |

---

# Volume Commands

| Command                 | Description           |
| ----------------------- | --------------------- |
| `docker volume create`  | Create volume         |
| `docker volume ls`      | List volumes          |
| `docker volume inspect` | View volume details   |
| `docker volume rm`      | Remove volume         |
| `docker volume prune`   | Remove unused volumes |

---

# Network Commands

| Command                     | Description          |
| --------------------------- | -------------------- |
| `docker network create`     | Create network       |
| `docker network ls`         | List networks        |
| `docker network inspect`    | View network details |
| `docker network connect`    | Connect container    |
| `docker network disconnect` | Disconnect container |
| `docker network rm`         | Remove network       |

---

# Docker Compose Commands

| Command                  | Description                  |
| ------------------------ | ---------------------------- |
| `docker compose up`      | Start services               |
| `docker compose up -d`   | Start services in background |
| `docker compose down`    | Stop and remove services     |
| `docker compose ps`      | List services                |
| `docker compose logs`    | View logs                    |
| `docker compose build`   | Build services               |
| `docker compose restart` | Restart services             |
| `docker compose pull`    | Pull images                  |

---

# Cleanup Commands

### Remove Stopped Containers

```bash
docker container prune
```

### Remove Unused Images

```bash
docker image prune
```

### Remove Unused Networks

```bash
docker network prune
```

### Remove Unused Volumes

```bash
docker volume prune
```

### Remove Everything Unused

```bash
docker system prune -a
```

### Check Docker Disk Usage

```bash
docker system df
```

---

# Dockerfile Instructions

## FROM

Base image.

```dockerfile
FROM ubuntu:24.04
```

---

## RUN

Executes commands during image build.

```dockerfile
RUN apt update && apt install -y nginx
```

---

## COPY

Copies files into image.

```dockerfile
COPY . /app
```

---

## WORKDIR

Sets working directory.

```dockerfile
WORKDIR /app
```

---

## EXPOSE

Documents container port.

```dockerfile
EXPOSE 80
```

---

## CMD

Default command executed when container starts.

```dockerfile
CMD ["python", "app.py"]
```

---

## ENTRYPOINT

Defines main executable.

```dockerfile
ENTRYPOINT ["nginx"]
```

---

# Summary

This cheat sheet covers:

* Docker Containers
* Images
* Volumes
* Networks
* Docker Compose
* Docker Cleanup
* Dockerfile Instructions
* Frequently Asked Docker Interview Questions

A solid reference for DevOps engineers, Docker beginners, and interview preparation.
