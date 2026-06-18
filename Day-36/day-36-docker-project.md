# Day 36 – Docker Project: Dockerize a Full Application

## Objective

The objective of this project was to Dockerize a complete application from development to deployment. The project includes containerizing a Flask application, integrating a PostgreSQL database, configuring Docker Compose, implementing persistent storage, creating a custom network, using environment variables, and publishing the final image to Docker Hub.

---

## Project Overview

### Application Chosen

**Flask Web Application with PostgreSQL Database**

### Why This Application?

This project was selected because it demonstrates real-world Docker concepts:

* Application containerization
* Database integration
* Multi-container orchestration
* Persistent data storage
* Environment management
* Docker networking
* Health checks
* Docker Hub deployment

---

## Project Structure

```text
day36-flask-app/
│
├── app.py
├── requirements.txt
├── Dockerfile
├── docker-compose.yml
├── .dockerignore
├── .env
└── README.md
```

---

## Dockerfile

```dockerfile
# Stage 1: Build dependencies
FROM python:3.12-alpine AS builder

WORKDIR /app

COPY requirements.txt .

RUN pip install --no-cache-dir \
    --prefix=/install \
    -r requirements.txt

# Stage 2: Final runtime image
FROM python:3.12-alpine

RUN addgroup -S appgroup && \
    adduser -S appuser -G appgroup

WORKDIR /app

COPY --from=builder /install /usr/local

COPY . .

RUN chown -R appuser:appgroup /app

USER appuser

EXPOSE 5000

CMD ["python", "app.py"]
```

---

## Dockerfile Explanation

### Builder Stage

```dockerfile
FROM python:3.12-alpine AS builder
```

Uses a lightweight Alpine-based Python image to install application dependencies.

### Working Directory

```dockerfile
WORKDIR /app
```

Sets the working directory inside the container.

### Copy Requirements

```dockerfile
COPY requirements.txt .
```

Copies dependency definitions.

### Install Dependencies

```dockerfile
RUN pip install --no-cache-dir --prefix=/install -r requirements.txt
```

Installs dependencies without storing cache files to reduce image size.

### Final Runtime Stage

```dockerfile
FROM python:3.12-alpine
```

Creates a clean runtime image.

### Create Non-Root User

```dockerfile
RUN addgroup -S appgroup && \
    adduser -S appuser -G appgroup
```

Improves container security.

### Copy Dependencies

```dockerfile
COPY --from=builder /install /usr/local
```

Copies only required packages from the build stage.

### Copy Application Files

```dockerfile
COPY . .
```

Copies source code.

### Change Ownership

```dockerfile
RUN chown -R appuser:appgroup /app
```

Ensures proper file permissions.

### Switch User

```dockerfile
USER appuser
```

Runs application as a non-root user.

### Expose Port

```dockerfile
EXPOSE 5000
```

Makes the application accessible.

### Start Application

```dockerfile
CMD ["python", "app.py"]
```

Launches the Flask application.

---

## Docker Compose Configuration

```yaml
services:

  app:
    build: .
    container_name: flask-app

    ports:
      - "5000:5000"

    env_file:
      - .env

    depends_on:
      db:
        condition: service_healthy

    networks:
      - app-network

  db:
    image: postgres:16-alpine

    container_name: postgres-db

    environment:
      POSTGRES_DB: ${POSTGRES_DB}
      POSTGRES_USER: ${POSTGRES_USER}
      POSTGRES_PASSWORD: ${POSTGRES_PASSWORD}

    volumes:
      - postgres-data:/var/lib/postgresql/data

    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U postgres"]
      interval: 10s
      retries: 5
      timeout: 5s

    networks:
      - app-network

volumes:
  postgres-data:

networks:
  app-network:
```

---

## Features Implemented

### Multi-Stage Build

Reduces image size by separating build and runtime stages.

### Non-Root User

Improves container security.

### PostgreSQL Database

Stores application data.

### Docker Volumes

Provides persistent storage for database data.

### Custom Docker Network

Allows communication between containers.

### Environment Variables

Stores configuration separately from code.

### Health Checks

Ensures the database is healthy before starting the application.

---

## Commands Used

### Build Application

```bash
docker compose build
```

### Start Services

```bash
docker compose up -d
```

### View Running Containers

```bash
docker ps
```

### View Logs

```bash
docker compose logs
```

### Stop Services

```bash
docker compose down
```

### List Volumes

```bash
docker volume ls
```

### List Networks

```bash
docker network ls
```

---

## Challenges Faced

### Challenge 1: Database Startup Timing

#### Problem

The Flask application attempted to connect before PostgreSQL was ready.

#### Solution

Added a health check and configured:

```yaml
depends_on:
  db:
    condition: service_healthy
```

This ensured the application started only after the database became healthy.

---

### Challenge 2: Large Image Size

#### Problem

Initial image size was large.

#### Solution

* Used Alpine Linux image
* Implemented multi-stage builds
* Used pip --no-cache-dir

This significantly reduced image size.

---

### Challenge 3: Container Security

#### Problem

Application was running as root.

#### Solution

Created a dedicated non-root user and executed the application with limited privileges.

---

## Docker Hub Deployment

### Login

```bash
docker login
```

### Tag Image

```bash
docker tag day36-flask-app-app yourdockerhub/flask-app:v1
```

### Push Image

```bash
docker push yourdockerhub/flask-app:v1
```

### Docker Hub Repository

```text
https://hub.docker.com/r/yourdockerhub/flask-app
```

Replace **yourdockerhub** with your Docker Hub username.

---

## Testing Fresh Deployment

### Remove Containers

```bash
docker compose down
```

### Remove Images

```bash
docker rmi yourdockerhub/flask-app:v1
```

### Pull From Docker Hub

```bash
docker pull yourdockerhub/flask-app:v1
```

### Start Again

```bash
docker compose up -d
```

The application successfully started using only the Docker Hub image and Compose file.

---

## Final Image Size

Approximate image size:

```text
70 MB – 100 MB
```

depending on installed dependencies.

---

## Learning Outcomes

Through this project, I learned:

* Writing production-ready Dockerfiles
* Multi-stage image builds
* Running containers securely as non-root users
* Managing environment variables
* Creating persistent storage using Docker volumes
* Container networking
* Database health checks
* Docker Compose orchestration
* Publishing images to Docker Hub
* Testing deployments from scratch

---

## Conclusion

This project demonstrates a complete end-to-end Docker workflow. The application was successfully containerized, integrated with PostgreSQL, orchestrated using Docker Compose, and published to Docker Hub. The implementation follows Docker best practices such as multi-stage builds, non-root users, environment variable management, health checks, and persistent storage.
