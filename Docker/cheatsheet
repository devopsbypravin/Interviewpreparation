
# 🐳 **Docker Cheat Sheet for DevOps Engineers**

---

## 📦 **Core Concepts**

| Term               | Description |
|--------------------|-------------|
| **Image**           | Read-only blueprint used to create containers |
| **Container**       | Lightweight, isolated instance from an image |
| **Dockerfile**      | Script to automate image creation |
| **Volume**          | Persistent storage outside the container |
| **Docker Hub**      | Public registry to store/share images |
| **Docker Daemon**   | Background service managing containers |
| **Docker Client**   | CLI tool to interact with Docker Daemon |

---

## 📁 **Basic Docker CLI Commands**

```bash
# Install Docker (Ubuntu)
sudo apt update && sudo apt install docker.io -y

# Check Docker version
docker --version

# Run a container from an image
docker run -d -p 8080:80 nginx

# List running containers
docker ps

# List all containers (including stopped)
docker ps -a

# Stop, start, and remove a container
docker stop <id>
docker start <id>
docker rm <id>

# Remove unused images and containers
docker system prune -a
```

---

## 🛠️ **Working with Images**

```bash
# Build image from Dockerfile
docker build -t myapp:1.0 .

# Pull image from Docker Hub
docker pull nginx

# Push image to Docker Hub
docker tag myapp:1.0 mydockerhub/myapp:1.0
docker push mydockerhub/myapp:1.0

# List local images
docker images

# Remove an image
docker rmi <image-id>
```

---

## ⚙️ **Dockerfile Essentials**

```Dockerfile
FROM node:18-alpine         # Base image
WORKDIR /app                # Set working directory
COPY . .                    # Copy local files
RUN npm install             # Install dependencies
EXPOSE 3000                 # Port to expose
CMD ["node", "app.js"]      # Default command
```

---

## 🧱 **Volumes & Persistence**

```bash
# Create named volume
docker volume create mydata

# Mount volume in container
docker run -v mydata:/var/lib/mysql mysql

# Bind mount from host
docker run -v /host/path:/container/path nginx
```

---

## 🧩 **Docker Compose**

### `docker-compose.yml` Example:
```yaml
version: '3.8'
services:
  web:
    image: nginx
    ports:
      - "8080:80"

  db:
    image: mysql:5.7
    environment:
      MYSQL_ROOT_PASSWORD: root
    volumes:
      - db_data:/var/lib/mysql

volumes:
  db_data:
```

### Common Commands:
```bash
docker-compose up -d      # Start all services
docker-compose down       # Stop and remove containers/networks
docker-compose logs       # View logs
docker-compose ps         # List running services
```

---

## 🕸️ **Docker Networking**

```bash
docker network ls              # List networks
docker network create mynet    # Create custom network
docker run --network=mynet ... # Run container in a specific network
```

---

## 🔁 **Docker Swarm Quick Commands**

```bash
docker swarm init                             # Initialize Swarm
docker service create --replicas 3 ...        # Create service
docker service scale web=5                    # Scale service
docker node ls                                # View Swarm nodes
```

---

## 📋 **Docker Logs & Exec**

```bash
docker logs <container-id>                 # View logs
docker exec -it <container-id> bash        # Shell into container
docker inspect <container-id>              # Full container info
```

---

## 🧪 **Real-Life Examples**

```bash
# Docker run with env & volume
docker run -d \
  -p 8080:80 \
  -v logs:/app/logs \
  -e ENV=prod \
  myapp:1.0

# Multi-stage Docker build (optimization)
FROM node:18-alpine as builder
WORKDIR /app
COPY . .
RUN npm install && npm run build

FROM nginx
COPY --from=builder /app/build /usr/share/nginx/html
```

---
