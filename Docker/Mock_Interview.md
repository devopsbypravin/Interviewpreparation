Here's a 🔥 **Mock DevOps Interview Script** focused on **Docker & Containerization** — featuring a realistic 
Q&A flow between **Interviewer (I)** and **You (Pravin, DevOps Engineer)**. This is aligned with real interviews 
from top product & cloud-based companies.

---

## 🎤 **Mock Interview: Docker & Containerization**

---

### 🧑‍💼 **Interviewer:**  
Hi Pravin, welcome! Let’s start with the basics. What is Docker and how is it different from a virtual machine?

---

### 👨‍💻 **You (Pravin):**  
Thank you! Docker is a containerization platform that allows us to package applications along with their dependencies in isolated environments called containers.  
Unlike VMs, Docker containers share the host OS kernel and are much more lightweight and faster to start. This makes them ideal for DevOps and microservices deployments.

---

### 🧑‍💼 **Interviewer:**  
Great. Can you explain what happens when you run `docker run nginx`?

---

### 👨‍💻 **You (Pravin):**  
Sure. When I run `docker run nginx`:
1. Docker checks if the `nginx` image exists locally.
2. If not, it pulls it from Docker Hub.
3. It creates a new container from that image.
4. By default, it runs in the foreground unless I specify `-d` for detached mode.

---

### 🧑‍💼 **Interviewer:**  
What’s the difference between an image and a container?

---

### 👨‍💻 **You (Pravin):**  
An **image** is a static, read-only template used to create containers — it contains the app code, OS dependencies, etc.  
A **container** is a runtime instance of an image — it's live, isolated, and can be started/stopped as needed.

---

### 🧑‍💼 **Interviewer:**  
Nice. How do you persist data in a Docker container?

---

### 👨‍💻 **You (Pravin):**  
I use **volumes**. For example:
```bash
docker run -v mydata:/var/lib/mysql mysql
```
This creates a named volume (`mydata`) that persists data even if the container is removed.  
For host path mounting:
```bash
-v /host/logs:/app/logs
```

---

### 🧑‍💼 **Interviewer:**  
Let’s talk about Dockerfile. What are the most commonly used instructions?

---

### 👨‍💻 **You (Pravin):**  
Key Dockerfile instructions include:
- `FROM`: Base image
- `WORKDIR`: Set working directory
- `COPY` / `ADD`: Copy files into image
- `RUN`: Execute shell commands during build
- `EXPOSE`: Document listening port
- `CMD` / `ENTRYPOINT`: Set default runtime command

---

### 🧑‍💼 **Interviewer:**  
Say you're running multiple containers for frontend, backend, and database. How do you manage that?

---

### 👨‍💻 **You (Pravin):**  
I'd use **Docker Compose** to define all services in a `docker-compose.yml`. It handles:
- Service definitions
- Networking
- Volume mounting
- Environment configs  
Example:
```yaml
services:
  web:
    build: ./web
    ports: ["3000:3000"]
  db:
    image: postgres
    volumes:
      - dbdata:/var/lib/postgresql/data
```

---

### 🧑‍💼 **Interviewer:**  
Nice. Now, how would you push your custom image to Docker Hub?

---

### 👨‍💻 **You (Pravin):**  
1. Tag the image:
```bash
docker tag myapp:latest pravindevops/myapp:1.0
```
2. Login to Docker Hub:
```bash
docker login
```
3. Push the image:
```bash
docker push pravindevops/myapp:1.0
```

---

### 🧑‍💼 **Interviewer:**  
Last one – you need to deploy the app on 3 nodes using Docker Swarm. What’s your approach?

---

### 👨‍💻 **You (Pravin):**  
I’d do the following:
1. Initialize the Swarm on the manager:
```bash
docker swarm init
```
2. Join workers using the token:
```bash
docker swarm join --token <token> <manager-ip>:2377
```
3. Deploy a service:
```bash
docker service create --replicas 3 --name webapp -p 80:80 myapp:1.0
```
4. Use `docker service ls` and `docker service ps webapp` to monitor rollout.

---

### 🧑‍💼 **Interviewer:**  
Excellent answers, Pravin. You're clearly strong in containerization. Thanks for your time!

---

### 👨‍💻 **You (Pravin):**  
Thank you! It was great sharing. Always excited about clean CI/CD with containers.

---
