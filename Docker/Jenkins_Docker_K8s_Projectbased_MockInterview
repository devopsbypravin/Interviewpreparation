# 🧪 **Mock Interview: Project-Based DevOps Workflow (Jenkins + Docker + K8s)**

---

## 🎯 **Project Context:**
> You're a DevOps Engineer at a company building a Spring Boot application with a React frontend and a PostgreSQL DB.  
> Your role is to build a CI/CD pipeline that:
- Builds the backend & frontend using Docker
- Runs unit tests
- Pushes Docker images to Docker Hub
- Deploys to a Kubernetes cluster

---

### 🧑‍💼 **Interviewer:**  
Pravin, let’s start with your CI/CD setup. Walk me through the pipeline you built for this project.

---

### 👨‍💻 **You (Pravin):**  
Sure. I used a **Jenkins declarative pipeline** with the following stages:
1. **Checkout code** from GitHub
2. **Build backend JAR** using Maven
3. **Build frontend** with Node.js
4. **Dockerize** both apps using multi-stage builds
5. **Push Docker images** to Docker Hub
6. **Deploy to Kubernetes** using `kubectl` or Helm

Each step is codified in a `Jenkinsfile`.

---

### 🧑‍💼 **Interviewer:**  
Sounds solid. Can you explain how you handled Docker image tagging in the pipeline?

---

### 👨‍💻 **You (Pravin):**  
Yes. I tag images dynamically using the Jenkins build number or commit hash:

```groovy
def imageTag = "${env.BUILD_NUMBER}"
docker.build("pravindevops/backend:${imageTag}")
```

This helps version control and traceability in deployments.

---

### 🧑‍💼 **Interviewer:**  
What does your `Jenkinsfile` look like for this full pipeline?

---

### 👨‍💻 **You (Pravin):**  
Here's a simplified version:

```groovy
pipeline {
  agent any

  tools {
    maven 'maven3'
    nodejs 'node14'
  }

  environment {
    IMAGE_TAG = "${BUILD_NUMBER}"
    DOCKER_CREDENTIALS = 'dockerhub-creds'
  }

  stages {
    stage('Checkout') {
      steps { git 'https://github.com/org/myproject.git' }
    }

    stage('Build Backend') {
      steps { sh 'mvn clean package -f backend/pom.xml' }
    }

    stage('Build Frontend') {
      steps {
        dir('frontend') {
          sh 'npm install && npm run build'
        }
      }
    }

    stage('Dockerize & Push') {
      steps {
        script {
          docker.withRegistry('https://index.docker.io/v1/', DOCKER_CREDENTIALS) {
            docker.build("pravindevops/backend:${IMAGE_TAG}", 'backend').push()
            docker.build("pravindevops/frontend:${IMAGE_TAG}", 'frontend').push()
          }
        }
      }
    }

    stage('Deploy to K8s') {
      steps {
        sh "kubectl set image deployment/backend backend=pravindevops/backend:${IMAGE_TAG} -n dev"
        sh "kubectl set image deployment/frontend frontend=pravindevops/frontend:${IMAGE_TAG} -n dev"
      }
    }
  }

  post {
    success { echo 'Deployed successfully to Kubernetes' }
    failure { echo 'Build or Deploy failed' }
  }
}
```

---

### 🧑‍💼 **Interviewer:**  
Nice. Now, how did you define Kubernetes manifests for the app?

---

### 👨‍💻 **You (Pravin):**  
I used separate `deployment.yaml` and `service.yaml` for each component:

- Backend exposed as **ClusterIP**
- Frontend exposed via **Ingress**
- PostgreSQL with a **PersistentVolumeClaim**

I also used **ConfigMaps** for environment variables and **Secrets** for DB credentials.

---

### 🧑‍💼 **Interviewer:**  
How do you promote builds from Dev to Stage to Prod?

---

### 👨‍💻 **You (Pravin):**  
I use parameterized Jenkins pipelines or multi-branch pipelines. Once Dev is validated, I manually approve or auto-trigger deploys to Stage → Prod using:

```bash
kubectl apply -f k8s/prod/deployment.yaml
```

Or with Helm:

```bash
helm upgrade myapp ./helm-chart -f values-prod.yaml
```

---

### 🧑‍💼 **Interviewer:**  
What’s your rollback strategy if a deployment fails in K8s?

---

### 👨‍💻 **You (Pravin):**  
I keep previous image tags and can do a quick rollback with:

```bash
kubectl rollout undo deployment/backend
```

Also, `kubectl rollout status` helps check deployment progress before switching traffic.

---

### 🧑‍💼 **Interviewer:**  
Last one — how do you monitor this setup?

---

### 👨‍💻 **You (Pravin):**  
- Jenkins: **build logs, Slack alerts**
- Docker: monitored via **Prometheus exporters** inside containers
- Kubernetes: integrated **Prometheus + Grafana**, with alerting on pod crashes, high memory/CPU
- Also use **Kubernetes Dashboard**, `kubectl top`, and `lens IDE` for real-time cluster insights

---

### 🧑‍💼 **Interviewer:**  
Excellent, Pravin. You're clearly hands-on and process-oriented. Great job!

---

### 👨‍💻 **You (Pravin):**  
Thanks! I'm passionate about clean CI/CD, containerized microservices, and reliable deployments. 🙌

---
