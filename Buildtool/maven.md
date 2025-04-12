Based on the **"Understanding and Using Build Tool"** documentation, here's a full set of **interview questions** categorized by **beginner, intermediate, advanced**, and **scenario-based** — tailored to current DevOps interviews (especially Maven-based builds in CI/CD pipelines).

---

## 🔹 **Beginner-Level Questions (Conceptual Understanding)**

1. **What is a build tool and why is it important in software development?**
2. **What is Apache Maven and how does it differ from Ant or Gradle?**
3. **What is a POM file in Maven? What essential information does it contain?**
4. **What is the purpose of the `mvn compile` command?**
5. **Explain the build lifecycle in Maven. Name at least three phases.**
6. **What are Maven archetypes and how do they help in project creation?**
7. **What is the difference between `mvn install` and `mvn deploy`?**
8. **What does `mvn clean install` do in a single command?**
9. **Where does Maven store downloaded dependencies on your system?**
10. **What are dependencies in Maven, and how are they defined?**

---

## 🔸 **Intermediate-Level Questions (Working Knowledge)**

11. **Explain the difference between a local, remote, and central repository in Maven.**
12. **How does Maven resolve transitive dependencies?**
13. **What is the use of the `mvn dependency:tree` command?**
14. **What is the role of plugins in Maven? Name two commonly used ones.**
15. **How do you customize the build process in Maven using profiles?**
16. **What is `maven-surefire-plugin` used for?**
17. **How can you generate documentation for your project using Maven?**
18. **How do you configure and use custom Maven plugins in a project?**
19. **What are Maven goals and how do they relate to build phases?**
20. **What does "Convention over Configuration" mean in the context of Maven?**

---

## 🔧 **Advanced-Level Questions (CI/CD & Real Projects)**

21. **How do you integrate Maven with Jenkins for a CI pipeline?**
22. **What happens when two dependencies bring in conflicting versions of the same library? How can you resolve this in Maven?**
23. **How can you use different build configurations for Dev, QA, and Prod using Maven profiles?**
24. **What are SNAPSHOT versions in Maven? Why are they used and how do they behave differently from release versions?**
25. **How do you secure internal artifacts and publish to a private Maven repository (like Nexus or Artifactory)?**
26. **What is the role of the `maven-compiler-plugin`? How can you configure Java version in POM?**
27. **How do you manage multimodule Maven projects?**
28. **Explain the build order in a multimodule Maven setup.**
29. **What is Maven’s effective POM and how do you view it?**
30. **How would you override a dependency version in Maven if it is coming from a transitive dependency?**

---

## 🎯 **Scenario-Based Questions (Real-World DevOps Use Cases)**

### ✅ Scenario 1: Production Deployment Pipeline
> *You're tasked with setting up a Maven-based build pipeline in Jenkins. Walk through how you'd go from code commit to deployment.*

🧠 **Expected Discussion:**
- Use `mvn clean install`
- Run `unit` & `integration` tests via `maven-surefire-plugin`
- Package into `.jar` or `.war`
- Archive artifact and deploy using `mvn deploy` to Nexus/Artifactory
- Use Maven goals as Jenkins build steps

---

### ✅ Scenario 2: Dependency Conflict
> *You're seeing build failures due to conflicting library versions. How would you debug and resolve it?*

🧠 **Expected Discussion:**
- Use `mvn dependency:tree` to identify conflicts
- Use `<dependencyManagement>` to enforce correct version
- Exclude transitive dependency from specific artifact

---

### ✅ Scenario 3: Project Bootstrapping
> *Your team wants to start a Spring Boot project. What is the fastest and most standardized way to set it up using Maven?*

🧠 **Expected Discussion:**
- Use [Spring Initializr](https://start.spring.io/)
- Generate Maven project with selected dependencies
- Import into IDE
- Customize `pom.xml` as needed

---

### ✅ Scenario 4: Environment-Specific Builds
> *You want to run different builds for staging and production. How would you manage that in Maven?*

🧠 **Expected Discussion:**
- Use Maven profiles (`<profiles>`)
- Each profile includes environment-specific configs or dependencies
- Trigger via CLI: `mvn clean install -Pstaging`

---

### ✅ Scenario 5: Maven in Microservice Architecture
> *You’re building multiple microservices. How do you manage them in Maven?*

🧠 **Expected Discussion:**
- Use **multi-module Maven project**
- Parent POM manages shared dependencies
- Each service is a submodule with its own POM

 **Maven + Jenkins CI lab** and include **hands-on demo scripts** with `mvn` commands for a full DevOps-style pipeline.

---

## 🧪 **Maven + Jenkins CI Lab Setup Instructions**

### 🔧 Prerequisites
- ✅ Java (JDK 11 or later)
- ✅ Maven (3.6+)
- ✅ Jenkins (latest LTS)
- ✅ Git
- ✅ Sample Java Project (we’ll use a `maven-archetype-quickstart` app)

---

### 🔨 Step 1: Install Java & Maven

#### ✅ On Ubuntu:
```bash
sudo apt update
sudo apt install openjdk-11-jdk maven -y
java -version
mvn -version
```

---

### 🔨 Step 2: Install Jenkins

#### ✅ On Ubuntu:
```bash
wget -q -O - https://pkg.jenkins.io/debian/jenkins.io.key | sudo apt-key add -
sudo sh -c 'echo deb http://pkg.jenkins.io/debian binary/ > /etc/apt/sources.list.d/jenkins.list'
sudo apt update
sudo apt install jenkins -y
sudo systemctl start jenkins
sudo systemctl enable jenkins
```

➡️ Open `http://<your-ip>:8080` to complete setup.

---

### 🔨 Step 3: Install Jenkins Plugins
- Maven Integration
- Git plugin
- Pipeline
- Blue Ocean (optional, for UI)
- Credentials Binding

---

### 🔨 Step 4: Configure Tools in Jenkins
- Go to **Manage Jenkins → Global Tool Configuration**
- Set:
  - **JDK** (e.g., JDK 11)
  - **Maven** (give a name like `maven3`)
  - **Git** (default is usually fine)

---

### 🔨 Step 5: Create a Sample Maven Project

```bash
mvn archetype:generate \
  -DgroupId=com.pravin.devops \
  -DartifactId=demo-app \
  -DarchetypeArtifactId=maven-archetype-quickstart \
  -DinteractiveMode=false
cd demo-app
```

---

## 💻 **Hands-On Jenkins Pipeline for Maven CI/CD**

### 🔧 `Jenkinsfile` (Place this in project root)

```groovy
pipeline {
  agent any

  tools {
    maven 'maven3'  // As configured in Jenkins tool config
    jdk 'JDK11'     // Your configured JDK label
  }

  stages {
    stage('Checkout Code') {
      steps {
        git 'https://github.com/<your-username>/demo-app.git'
      }
    }

    stage('Build with Maven') {
      steps {
        sh 'mvn clean install'
      }
    }

    stage('Run Tests') {
      steps {
        sh 'mvn test'
      }
    }

    stage('Package Artifact') {
      steps {
        sh 'mvn package'
      }
    }

    stage('Archive Artifact') {
      steps {
        archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
      }
    }
  }

  post {
    success {
      echo 'Build completed successfully!'
    }
    failure {
      echo 'Build failed!'
    }
  }
}
```

---

## 🧪 **Demo Maven Commands in Pipeline**

| Command | Purpose |
|--------|--------|
| `mvn clean` | Deletes previous builds (clears `target/`) |
| `mvn compile` | Compiles Java code |
| `mvn test` | Runs unit tests |
| `mvn package` | Creates JAR/WAR file |
| `mvn install` | Installs the artifact in your local repo (~/.m2) |
| `mvn deploy` | Deploys artifact to remote repository |
| `mvn dependency:tree` | Visualizes dependency graph |

---

## 🧰 Bonus: GitHub → Jenkins Webhook Setup (CI Trigger)
- In GitHub: Repo → Settings → Webhooks → Add `http://<jenkins-ip>:8080/github-webhook/`
- In Jenkins: Enable GitHub hook trigger in project config

---

Would you like a downloadable **lab PDF + GitHub template repo** or setup guide with screenshots?

Or I can help you create a **multi-module Maven microservice CI/CD lab** with Spring Boot + Docker + Jenkins!
