**Hands-On Lab Exercises** for mastering **Docker & Docker Hub**—built for real-world DevOps workflows with CI/CD, 
microservices, and local-to-cloud transition.

---

## 🧪 **Hands-On Docker Lab Exercises**

---

### ✅ **Lab 1: Docker Basics – Build & Run**

📌 *Goal:* Build a custom Docker image and run a container.

```bash
# 1. Create a basic Node.js app
mkdir docker-lab && cd docker-lab
echo "console.log('Hello from Docker')" > app.js
echo -e "FROM node:18\nCOPY . .\nCMD [\"node\", \"app.js\"]" > Dockerfile

# 2. Build the Docker image
docker build -t mynodeapp:1.0 .

# 3. Run the container
docker run --name node-demo mynodeapp:1.0
```

---

### ✅ **Lab 2: Container Networking & Port Binding**

📌 *Goal:* Expose a web app running in Docker.

```bash
# 1. Use a sample NGINX container
docker run -d -p 8080:80 --name web nginx

# 2. Test by visiting http://localhost:8080
```

---

### ✅ **Lab 3: Using Volumes for Persistent Storage**

📌 *Goal:* Run a MySQL container with persistent volume.

```bash
# 1. Create volume
docker volume create mysql_data

# 2. Run MySQL with volume mount
docker run -d --name mysql \
  -e MYSQL_ROOT_PASSWORD=root \
  -v mysql_data:/var/lib/mysql \
  mysql:5.7
```

---

### ✅ **Lab 4: Writing & Optimizing Dockerfiles**

📌 *Goal:* Dockerize a Java app using multi-stage build.

```Dockerfile
# Dockerfile (Spring Boot App)
FROM maven:3.8.6-openjdk-17 AS builder
WORKDIR /app
COPY . .
RUN mvn clean package

FROM openjdk:17
COPY --from=builder /app/target/*.jar app.jar
ENTRYPOINT ["java", "-jar", "app.jar"]
```

```bash
docker build -t springboot-app:1.0 .
docker run -d -p 8080:8080 springboot-app:1.0
```

---

### ✅ **Lab 5: Docker Compose – Multi-Service App**

📌 *Goal:* Run frontend, backend, and database together.

```yaml
# docker-compose.yml
version: '3'
services:
  db:
    image: postgres
    environment:
      POSTGRES_PASSWORD: root
    volumes:
      - db_data:/var/lib/postgresql/data

  backend:
    build: ./backend
    ports:
      - "5000:5000"
    depends_on:
      - db

  frontend:
    build: ./frontend
    ports:
      - "3000:3000"

volumes:
  db_data:
```

```bash
docker-compose up --build -d
```

---

### ✅ **Lab 6: Docker Hub – Push & Pull Image**

📌 *Goal:* Upload a custom image to Docker Hub.

```bash
docker login
docker tag springboot-app:1.0 pravindevops/springboot-app:1.0
docker push pravindevops/springboot-app:1.0
```

---

### ✅ **Lab 7: Docker Swarm (Cluster Basics)**

📌 *Goal:* Deploy a replicated service.

```bash
docker swarm init
docker service create \
  --name myapp \
  --replicas 3 \
  -p 8080:80 \
  nginx
```

---

### ✅ **Lab 8: Clean-up Commands**

📌 *Goal:* Clean images, containers, and volumes.

```bash
docker container prune
docker image prune -a
docker volume prune
```

---

## 🚀 Bonus: Combine With Jenkins

**Trigger build & deploy via Jenkins using:**

```groovy
pipeline {
  agent any
  stages {
    stage('Build Docker Image') {
      steps {
        sh 'docker build -t myapp:${BUILD_NUMBER} .'
      }
    }
    stage('Push to Docker Hub') {
      steps {
        withCredentials([string(credentialsId: 'dockerhub-token', variable: 'DOCKER_TOKEN')]) {
          sh '''
            echo $DOCKER_TOKEN | docker login -u pravindevops --password-stdin
            docker push pravindevops/myapp:${BUILD_NUMBER}
          '''
        }
      }
    }
  }
}
```

---
