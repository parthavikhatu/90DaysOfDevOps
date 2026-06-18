# Day 33 – Docker Compose: Multi-Container Basics

## Objective

The goal of this lab was to learn how Docker Compose simplifies the management of multi-container applications by defining services, networks, and volumes in a single YAML file.

---

## Task 1: Install & Verify Docker Compose

### Verify Docker Compose Installation

```bash
docker compose version
```

### Verify Docker Engine

```bash
docker version
```

### Result

Docker Compose was successfully installed and available for use.

---

## Task 2: First Docker Compose File

### Project Structure

```
compose-basics/
└── docker-compose.yml
```

### docker-compose.yml

```yaml
version: "3.9"

services:
  nginx:
    image: nginx:latest
    container_name: my-nginx
    ports:
      - "8080:80"
```

### Start the Service

```bash
docker compose up -d
```

### Verify Running Container

```bash
docker compose ps
```

### Access Application

Open in browser:

```
http://localhost:8080
```

### Stop and Remove

```bash
docker compose down
```

### Result

Successfully deployed and accessed an Nginx container using Docker Compose.

---

## Task 3: WordPress + MySQL Multi-Container Setup

### Project Structure

```
wordpress-compose/
├── docker-compose.yml
└── .env
```

### docker-compose.yml

```yaml
version: "3.9"

services:

  db:
    image: mysql:8.0
    container_name: mysql-db

    restart: always

    environment:
      MYSQL_DATABASE: wordpress
      MYSQL_USER: wpuser
      MYSQL_PASSWORD: wppassword
      MYSQL_ROOT_PASSWORD: rootpassword

    volumes:
      - mysql_data:/var/lib/mysql

  wordpress:
    image: wordpress:latest
    container_name: wordpress-app

    restart: always

    ports:
      - "8080:80"

    environment:
      WORDPRESS_DB_HOST: db:3306
      WORDPRESS_DB_USER: wpuser
      WORDPRESS_DB_PASSWORD: wppassword
      WORDPRESS_DB_NAME: wordpress

    depends_on:
      - db

volumes:
  mysql_data:
```

### Start Services

```bash
docker compose up -d
```

### Verify Containers

```bash
docker compose ps
```

### Access WordPress

Open:

```
http://localhost:8080
```

Complete the WordPress installation wizard.

### Verify Network Creation

```bash
docker network ls
```

Docker Compose automatically created a default network and connected both services.

### Verify Volume Creation

```bash
docker volume ls
```

A named volume was created for MySQL data persistence.

### Test Data Persistence

Stop services:

```bash
docker compose down
```

Start again:

```bash
docker compose up -d
```

WordPress data remained intact because the database data was stored in a named volume.

### Result

Successfully deployed a multi-container WordPress application with persistent MySQL storage.

---

## Task 4: Docker Compose Commands Practice

### Start Services

```bash
docker compose up -d
```

### View Running Services

```bash
docker compose ps
```

### View All Logs

```bash
docker compose logs
```

### Follow Logs

```bash
docker compose logs -f
```

### View Logs for a Specific Service

```bash
docker compose logs wordpress
```

```bash
docker compose logs db
```

### Stop Services

```bash
docker compose stop
```

### Restart Services

```bash
docker compose start
```

### Remove Containers and Networks

```bash
docker compose down
```

### Remove Containers, Networks and Volumes

```bash
docker compose down -v
```

### Rebuild Services

```bash
docker compose up -d --build
```

### Result

Practiced commonly used Docker Compose commands for managing applications.

---

## Task 5: Environment Variables

### .env File

```env
MYSQL_DATABASE=wordpress
MYSQL_USER=wpuser
MYSQL_PASSWORD=wppassword
MYSQL_ROOT_PASSWORD=rootpassword
```

### Using Variables in Compose

```yaml
services:
  db:
    image: mysql:8.0

    environment:
      MYSQL_DATABASE: ${MYSQL_DATABASE}
      MYSQL_USER: ${MYSQL_USER}
      MYSQL_PASSWORD: ${MYSQL_PASSWORD}
      MYSQL_ROOT_PASSWORD: ${MYSQL_ROOT_PASSWORD}
```

### Verify Environment Variables

```bash
docker exec -it mysql-db env
```

### Result

Successfully configured and loaded environment variables using a `.env` file.

---

## Key Learnings

* Docker Compose simplifies multi-container deployments.
* Services automatically communicate using service names.
* Compose automatically creates networks.
* Named volumes provide persistent storage.
* Environment variables can be managed through `.env` files.
* Docker Compose provides an efficient way to manage application lifecycles.

---

## Commands Cheat Sheet

```bash
# Start services
docker compose up -d

# Stop services
docker compose stop

# Start stopped services
docker compose start

# View running services
docker compose ps

# View logs
docker compose logs

# Follow logs
docker compose logs -f

# Service-specific logs
docker compose logs wordpress
docker compose logs db

# Rebuild services
docker compose up -d --build

# Remove containers and networks
docker compose down

# Remove containers, networks and volumes
docker compose down -v

# List networks
docker network ls

# List volumes
docker volume ls
```

## Conclusion

This lab demonstrated how Docker Compose simplifies container orchestration by managing multiple services, networking, storage, and environment variables from a single configuration file. It provided hands-on experience with deploying and managing a real-world WordPress and MySQL application stack.
