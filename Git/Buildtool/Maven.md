🔹 Beginner-Level Questions (Conceptual Understanding)
What is a build tool and why is it important in software development?

What is Apache Maven and how does it differ from Ant or Gradle?

What is a POM file in Maven? What essential information does it contain?

What is the purpose of the mvn compile command?

Explain the build lifecycle in Maven. Name at least three phases.

What are Maven archetypes and how do they help in project creation?

What is the difference between mvn install and mvn deploy?

What does mvn clean install do in a single command?

Where does Maven store downloaded dependencies on your system?

What are dependencies in Maven, and how are they defined?

🔸 Intermediate-Level Questions (Working Knowledge)
Explain the difference between a local, remote, and central repository in Maven.

How does Maven resolve transitive dependencies?

What is the use of the mvn dependency:tree command?

What is the role of plugins in Maven? Name two commonly used ones.

How do you customize the build process in Maven using profiles?

What is maven-surefire-plugin used for?

How can you generate documentation for your project using Maven?

How do you configure and use custom Maven plugins in a project?

What are Maven goals and how do they relate to build phases?

What does "Convention over Configuration" mean in the context of Maven?

🔧 Advanced-Level Questions (CI/CD & Real Projects)
How do you integrate Maven with Jenkins for a CI pipeline?

What happens when two dependencies bring in conflicting versions of the same library? How can you resolve this in Maven?

How can you use different build configurations for Dev, QA, and Prod using Maven profiles?

What are SNAPSHOT versions in Maven? Why are they used and how do they behave differently from release versions?

How do you secure internal artifacts and publish to a private Maven repository (like Nexus or Artifactory)?

What is the role of the maven-compiler-plugin? How can you configure Java version in POM?

How do you manage multimodule Maven projects?

Explain the build order in a multimodule Maven setup.

What is Maven’s effective POM and how do you view it?

How would you override a dependency version in Maven if it is coming from a transitive dependency?

🎯 Scenario-Based Questions (Real-World DevOps Use Cases)
✅ Scenario 1: Production Deployment Pipeline
You're tasked with setting up a Maven-based build pipeline in Jenkins. Walk through how you'd go from code commit to deployment.

🧠 Expected Discussion:

Use mvn clean install

Run unit & integration tests via maven-surefire-plugin

Package into .jar or .war

Archive artifact and deploy using mvn deploy to Nexus/Artifactory

Use Maven goals as Jenkins build steps

✅ Scenario 2: Dependency Conflict
You're seeing build failures due to conflicting library versions. How would you debug and resolve it?

🧠 Expected Discussion:

Use mvn dependency:tree to identify conflicts

Use <dependencyManagement> to enforce correct version

Exclude transitive dependency from specific artifact

✅ Scenario 3: Project Bootstrapping
Your team wants to start a Spring Boot project. What is the fastest and most standardized way to set it up using Maven?

🧠 Expected Discussion:

Use Spring Initializr

Generate Maven project with selected dependencies

Import into IDE

Customize pom.xml as needed

✅ Scenario 4: Environment-Specific Builds
You want to run different builds for staging and production. How would you manage that in Maven?

🧠 Expected Discussion:

Use Maven profiles (<profiles>)

Each profile includes environment-specific configs or dependencies

Trigger via CLI: mvn clean install -Pstaging

✅ Scenario 5: Maven in Microservice Architecture
You’re building multiple microservices. How do you manage them in Maven?

🧠 Expected Discussion:

Use multi-module Maven project

Parent POM manages shared dependencies

Each service is a submodule with its own POM
