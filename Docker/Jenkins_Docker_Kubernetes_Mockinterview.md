
# 🎤 **1. Jenkins + Docker Mock Interview Script**

---

### 🧑‍💼 **Interviewer:**  
Hi Pravin, welcome! Let's begin with CI/CD. How do you integrate Docker with Jenkins in a DevOps pipeline?

---

### 👨‍💻 **You (Pravin):**  
Thank you! I integrate Docker with Jenkins to automate the build, test, and deployment phases using containers. A typical pipeline includes:
- Cloning the codebase from Git
- Building a Docker image using `Dockerfile`
- Running tests inside a container
- Pushing the image to Docker Hub or a private registry
- Deploying the container to a staging or production environment

This can be defined using a `Jenkinsfile` for pipeline-as-code.

---

### 🧑‍💼 **Interviewer:**  
Nice. Can you walk me through a sample Jenkins pipeline stage for building and pushing a Docker image?

---

### 👨‍💻 **You (Pravin):**  
Sure! Here's a simplified declarative stage:

```groovy
stage('Build and Push Docker Image') {
  steps {
    script {
      dockerImage = docker.build("pravindevops/myapp:${BUILD_NUMBER}")
      docker.withRegistry('https://index.docker.io/v1/', 'dockerhub-cred-id') {
        dockerImage.push()
      }
    }
  }
}
```

I use `docker.build()` to create the image and `withRegistry()` to authenticate and push.

---

### 🧑‍💼 **Interviewer:**  
How do you pass credentials securely in Jenkins for Docker Hub?

---

### 👨‍💻 **You (Pravin):**  
I use **Jenkins Credentials Manager**. I store Docker Hub credentials as a secret (e.g., username/password or token), then use the `withCredentials` or `withRegistry` block to inject them into the pipeline.

---

### 🧑‍💼 **Interviewer:**  
Let’s say your Jenkins agent doesn’t have Docker installed. How do you handle it?

---

### 👨‍💻 **You (Pravin):**  
I’d use:
1. **Docker-in-Docker (DinD)** in Jenkins agents.
2. Or run Jenkins itself in Docker with the host socket mounted:
   ```bash
   -v /var/run/docker.sock:/var/run/docker.sock
   ```
   This gives Jenkins the ability to manage Docker on the host.

---

### 🧑‍💼 **Interviewer:**  
How do you use multi-stage builds in your `Dockerfile` to optimize your CI pipeline?

---

### 👨‍💻 **You (Pravin):**  
I use multi-stage builds to separate build-time dependencies from the final runtime image. It reduces image size and attack surface:

```Dockerfile
FROM maven:3.8 AS build
COPY . /app
RUN mvn -f /app/pom.xml clean package

FROM openjdk:17
COPY --from=build /app/target/*.jar app.jar
ENTRYPOINT ["java", "-jar", "app.jar"]
```

---

### 🧑‍💼 **Interviewer:**  
Solid. Let's move to Kubernetes now...

---

# ☸️ **2. Kubernetes Mock Interview Script (Next Step After Docker)**

---

### 🧑‍💼 **Interviewer:**  
Pravin, now that you're working with Docker and Jenkins, how do you scale this setup using Kubernetes?

---

### 👨‍💻 **You (Pravin):**  
Kubernetes (K8s) helps me manage containerized apps across a cluster. I use it to:
- Deploy apps as Pods within Deployments
- Expose services via ClusterIP/NodePort/Ingress
- Auto-scale containers using HPA
- Manage configs and secrets through ConfigMaps & Secrets

I also deploy Jenkins itself on Kubernetes using Helm.

---

### 🧑‍💼 **Interviewer:**  
Explain what a Pod is in Kubernetes.

---

### 👨‍💻 **You (Pravin):**  
A **Pod** is the smallest deployable unit in Kubernetes. It represents one or more containers that share the same network namespace, volume, and environment. It’s ephemeral — replaced by Deployments or ReplicaSets when terminated.

---

### 🧑‍💼 **Interviewer:**  
How do you perform a rolling update in Kubernetes?

---

### 👨‍💻 **You (Pravin):**  
I update the image version in the Deployment manifest and apply it:

```bash
kubectl set image deployment/myapp myapp=pravindevops/myapp:v2
```

Kubernetes gradually replaces Pods with the new version while keeping the service live — that’s rolling update by default.

---

### 🧑‍💼 **Interviewer:**  
What’s the difference between a ConfigMap and a Secret?

---

### 👨‍💻 **You (Pravin):**  
Both inject config data into Pods:
- **ConfigMap** stores non-sensitive data like env variables or app settings.
- **Secret** stores sensitive data like API keys or passwords (base64 encoded).

I mount them as volumes or use `envFrom`.

---

### 🧑‍💼 **Interviewer:**  
You deployed a pod but it's stuck in `CrashLoopBackOff`. How would you troubleshoot?

---

### 👨‍💻 **You (Pravin):**  
I’d run:
```bash
kubectl describe pod <pod-name>
kubectl logs <pod-name>
```
I’d check for misconfigured startup commands, missing configs, or image issues.

---

### 🧑‍💼 **Interviewer:**  
Nice. Final one: how do you expose a service externally?

---

### 👨‍💻 **You (Pravin):**  
There are three options:
1. **NodePort** – exposes service on a static port across all nodes.
2. **LoadBalancer** – provisions an external IP (e.g., on AWS/GCP).
3. **Ingress** – smart layer 7 routing with domain-based access.

I prefer **Ingress** for complex routing with NGINX or Traefik controllers.

---

### 🧑‍💼 **Interviewer:**  
Fantastic, Pravin. You clearly have a solid grip on CI/CD, Docker, and Kubernetes. Keep it up!

---

### 👨‍💻 **You (Pravin):**  
Thank you! Always excited to automate, containerize, and scale 🚀

---
