# Day 35 – Multi-Stage Builds & Docker Hub

## Objective

The goal of this lab was to learn how to optimize Docker images using multi-stage builds, apply Docker image best practices, and publish images to Docker Hub.

---

## Task 1: Single-Stage Build

### Application

A simple Node.js application was created.

### app.js

```javascript
console.log("Hello from Docker!");
```

### package.json

```json
{
  "name": "docker-demo",
  "version": "1.0.0",
  "main": "app.js"
}
```

### Single-Stage Dockerfile

```dockerfile
FROM node:20

WORKDIR /app

COPY . .

CMD ["node", "app.js"]
```

### Build Command

```bash
docker build -f Dockerfile.single -t node-single .
```

### Verify Image Size

```bash
docker images
```

Example Output:

```text
REPOSITORY    TAG       SIZE
node-single   latest    1.1GB
```

### Run Container

```bash
docker run --rm node-single
```

Output:

```text
Hello from Docker!
```

---

## Task 2: Multi-Stage Build

### Multi-Stage Dockerfile

```dockerfile
# Build Stage
FROM node:20 AS builder

WORKDIR /app

COPY . .

# Runtime Stage
FROM node:20-alpine

WORKDIR /app

COPY --from=builder /app .

CMD ["node", "app.js"]
```

### Build Command

```bash
docker build -f Dockerfile.multi -t node-multi .
```

### Verify Image Size

```bash
docker images
```

Example Output:

```text
REPOSITORY    TAG       SIZE
node-multi    latest    180MB
```

---

## Image Size Comparison

| Build Type   | Image Size |
| ------------ | ---------- |
| Single-Stage | 1.1 GB     |
| Multi-Stage  | 180 MB     |

### Why is the Multi-Stage Image Smaller?

The builder stage contains all dependencies, build tools, and temporary files required to build the application.

The runtime stage copies only the final application files into a lightweight image, removing unnecessary build dependencies.

Benefits:

* Smaller image size
* Faster image downloads
* Reduced attack surface
* Improved security
* Faster deployments

---

## Task 3: Push Image to Docker Hub

### Login

```bash
docker login
```

### Tag Image

```bash
docker tag node-multi <dockerhub-username>/node-demo:v1
```

Example:

```bash
docker tag node-multi parthavi123/node-demo:v1
```

### Push Image

```bash
docker push parthavi123/node-demo:v1
```

### Verify

Remove the image locally:

```bash
docker rmi parthavi123/node-demo:v1
```

Pull again from Docker Hub:

```bash
docker pull parthavi123/node-demo:v1
```

Run the container:

```bash
docker run --rm parthavi123/node-demo:v1
```

Output:

```text
Hello from Docker!
```

---

## Task 4: Docker Hub Repository

### Repository Description

```text
Simple Node.js application demonstrating Docker Multi-Stage Builds and Docker image optimization.
```

### Understanding Tags

Examples:

```text
v1
v2
v3
latest
```

Pull latest version:

```bash
docker pull parthavi123/node-demo
```

Pull a specific version:

```bash
docker pull parthavi123/node-demo:v1
```

Using version tags ensures predictable and reproducible deployments.

---

## Task 5: Docker Image Best Practices

### 1. Use Minimal Base Images

Instead of:

```dockerfile
FROM ubuntu:24.04
```

Use:

```dockerfile
FROM alpine:3.22
```

Benefits:

* Smaller image size
* Faster downloads
* Better security

---

### 2. Avoid Running as Root

```dockerfile
FROM node:20-alpine

RUN adduser -D appuser

USER appuser

WORKDIR /app

COPY . .

CMD ["node", "app.js"]
```

Benefits:

* Improved container security
* Reduced privileges

---

### 3. Use Specific Image Tags

Avoid:

```dockerfile
FROM node:latest
```

Prefer:

```dockerfile
FROM node:20-alpine
```

Benefits:

* Consistent builds
* Easier troubleshooting

---

### 4. Reduce Image Layers

Instead of:

```dockerfile
RUN apk update
RUN apk add curl
RUN apk add git
```

Use:

```dockerfile
RUN apk update && apk add curl git
```

Benefits:

* Smaller image size
* Faster build times

---

## Final Production-Ready Dockerfile

```dockerfile
# Builder Stage
FROM node:20-alpine AS builder

WORKDIR /app

COPY . .

# Runtime Stage
FROM node:20-alpine

RUN adduser -D appuser

USER appuser

WORKDIR /app

COPY --from=builder /app .

CMD ["node", "app.js"]
```

---

## Key Commands Used

```bash
docker build
docker images
docker run
docker login
docker tag
docker push
docker pull
docker rmi
```

---

## Learning Outcomes

* Understood the difference between single-stage and multi-stage builds.
* Reduced Docker image size significantly using multi-stage builds.
* Learned how to publish images to Docker Hub.
* Explored Docker image versioning using tags.
* Applied Docker image optimization and security best practices.
* Created a production-ready Docker image.

---

## Conclusion

Successfully built and optimized a Docker image using multi-stage builds, pushed it to Docker Hub, and implemented industry-standard Docker best practices. Multi-stage builds help create smaller, faster, and more secure container images suitable for production environments.
