# Day 31 – Dockerfile: Build Your Own Images

## Objective

Learn how to create custom Docker images using Dockerfiles, understand common Dockerfile instructions, compare CMD and ENTRYPOINT, build a simple web application image, use .dockerignore, and optimize Docker builds using layer caching.

---

# Task 1: Your First Dockerfile

## Dockerfile

```dockerfile
FROM ubuntu

RUN apt-get update && apt-get install -y curl

CMD ["echo", "Hello from my custom image!"]
```

## Build Image

```bash
docker build -t my-ubuntu:v1 .
```

## Run Container

```bash
docker run my-ubuntu:v1
```

## Output

```text
Hello from my custom image!
```

### What I Learned

* `FROM` specifies the base image.
* `RUN` executes commands during image build.
* `CMD` defines the default command executed when a container starts.
* Docker images can be customized with additional software and configurations.

---

# Task 2: Dockerfile Instructions

## Project Structure

```text
dockerfile-demo/
├── Dockerfile
└── index.html
```

## Dockerfile

```dockerfile
FROM nginx:alpine

WORKDIR /usr/share/nginx/html

COPY index.html .

RUN echo "Build Successful"

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
```

## Build Image

```bash
docker build -t nginx-demo:v1 .
```

## Run Container

```bash
docker run -d -p 8080:80 --name nginx-demo nginx-demo:v1
```

## Dockerfile Instructions Explained

| Instruction | Purpose                         |
| ----------- | ------------------------------- |
| FROM        | Defines base image              |
| RUN         | Executes commands during build  |
| COPY        | Copies files into image         |
| WORKDIR     | Sets working directory          |
| EXPOSE      | Documents container port        |
| CMD         | Defines default startup command |

---

# Task 3: CMD vs ENTRYPOINT

## CMD Example

```dockerfile
FROM ubuntu

CMD ["echo", "hello"]
```

### Run

```bash
docker run cmd-demo
```

Output:

```text
hello
```

### Override CMD

```bash
docker run cmd-demo date
```

Output:

```text
Current date and time
```

CMD is replaced by the new command.

---

## ENTRYPOINT Example

```dockerfile
FROM ubuntu

ENTRYPOINT ["echo"]
```

### Run

```bash
docker run entry-demo hello
```

Output:

```text
hello
```

### Run With Arguments

```bash
docker run entry-demo Docker
```

Output:

```text
Docker
```

Arguments are appended to ENTRYPOINT.

### CMD vs ENTRYPOINT

| CMD                      | ENTRYPOINT                                               |
| ------------------------ | -------------------------------------------------------- |
| Provides default command | Provides fixed executable                                |
| Easy to override         | Harder to override                                       |
| Used for defaults        | Used when container should always run a specific program |

---

# Task 4: Build a Simple Web App Image

## index.html

```html
<!DOCTYPE html>
<html>
<head>
    <title>Docker Website</title>
</head>
<body>
    <h1>Hello From Docker!</h1>
</body>
</html>
```

## Dockerfile

```dockerfile
FROM nginx:alpine

COPY index.html /usr/share/nginx/html/index.html

EXPOSE 80
```

## Build

```bash
docker build -t my-website:v1 .
```

## Run

```bash
docker run -d -p 8080:80 --name website my-website:v1
```

## Verify

Open:

```text
http://localhost:8080
```

The custom HTML page is displayed.

---

# Task 5: Using .dockerignore

## .dockerignore

```text
node_modules
.git
*.md
.env
```

## Benefits

* Reduces build context size
* Speeds up image builds
* Prevents sensitive files from being copied
* Creates smaller Docker images

---

# Task 6: Build Optimization and Layer Caching

## Initial Dockerfile

```dockerfile
FROM ubuntu

COPY . .

RUN apt-get update

CMD ["bash"]
```

Any file change causes Docker to rebuild layers after COPY.

---

## Optimized Dockerfile

```dockerfile
FROM ubuntu

RUN apt-get update

COPY . .

CMD ["bash"]
```

Now Docker can reuse cached layers and only rebuild changed layers.

### Why Layer Order Matters

Docker builds images layer by layer.

```text
Layer 1 → FROM
Layer 2 → RUN
Layer 3 → COPY
Layer 4 → CMD
```

Best Practice:

* Put stable instructions first.
* Put frequently changing files later.
* Maximize cache reuse.
* Reduce build time.

---

# Key Commands Used

```bash
docker build -t image:tag .

docker images

docker run image:tag

docker run -d -p 8080:80 image:tag

docker ps

docker ps -a

docker stop container_name

docker rm container_name

docker rmi image_name

docker logs container_name
```

---

# Summary

Today I learned how to:

* Create custom Docker images using Dockerfiles.
* Use Dockerfile instructions such as FROM, RUN, COPY, WORKDIR, EXPOSE, and CMD.
* Understand the difference between CMD and ENTRYPOINT.
* Build and deploy a static website using Nginx.
* Use .dockerignore to exclude unnecessary files.
* Optimize Docker builds using layer caching.

This knowledge is essential for packaging, shipping, and deploying applications efficiently using Docker.
