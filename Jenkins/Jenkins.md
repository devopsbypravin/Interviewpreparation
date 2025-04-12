🔹 Beginner-Level Jenkins Questions
What is Jenkins, and why is it used in DevOps?

What are the core features of Jenkins?

What is a Freestyle job in Jenkins?

How do you install Jenkins on Ubuntu?

What plugins are commonly used with Jenkins?

What are the differences between Continuous Integration and Traditional Integration?

What is a build trigger in Jenkins? Give examples.

What is the role of Jenkinsfile?

How can you secure Jenkins after installation?

What’s the default port for Jenkins and how do you change it?

🔸 Intermediate Jenkins Questions
Explain the Jenkins Master-Slave architecture.

How do you configure a Jenkins slave node?

What is the difference between Declarative and Scripted Pipelines?

What’s the use of agent block in a Jenkins pipeline?

How can you trigger a Jenkins job using GitHub webhook?

What’s the purpose of the “Build Now” and “Build Periodically” options?

How do you manage tools (Java, Git, Maven) in Jenkins?

How does Jenkins integrate with Maven? Provide a step-by-step.

How can you archive artifacts in Jenkins?

What is the difference between build and post-build actions in Jenkins?

🔧 Advanced Jenkins Questions
How do you handle parallel execution in Jenkins Pipeline?

What is Blue Ocean in Jenkins?

How do you implement environment-specific deployment in a pipeline?

How do you use input step in Jenkins pipeline to pause for manual approval?

How do you pass parameters to a Jenkins pipeline job?

How do you handle failures and retries in Jenkins pipeline?

How can you integrate SonarQube or Checkstyle for static code analysis in Jenkins?

How do you integrate code coverage tools like JaCoCo with Jenkins?

What are shared libraries in Jenkins pipeline? Why and how are they used?

What are best practices for managing credentials in Jenkins securely?

🎯 Scenario-Based Jenkins Questions (Real Projects)
✅ Scenario 1: CI/CD Pipeline Design
You need to set up a CI/CD pipeline that builds a Java project, runs tests, checks code quality using SonarQube, packages the artifact, and deploys it to dev/staging/prod.
🧠 What would your Jenkinsfile look like? What plugins/tools are required?

✅ Scenario 2: Handling Pipeline Failures
One of your pipeline stages fails intermittently. How do you debug and resolve this while keeping the build history clean?
🧠 Hint: Use retry, post { failure { ... } }, and logs.

✅ Scenario 3: GitHub → Jenkins Webhook
Your team is working with GitHub. You want the pipeline to trigger automatically on push to main.
🧠 Explain how you configure GitHub and Jenkins to achieve this.

✅ Scenario 4: Agent-Specific Builds
You have a Windows slave and a Linux slave. Some build steps require Windows.
🧠 How would you structure your pipeline to run certain stages only on a specific node label?

✅ Scenario 5: Plugin Conflict After Jenkins Upgrade
After updating plugins, a job fails that previously worked.
🧠 How do you roll back plugins or troubleshoot plugin compatibility issues?

✅ Scenario 6: Secure Deployment
Your pipeline deploys to production using SSH keys. You’ve been asked to enhance security.
🧠 How would you use Jenkins Credentials Binding to secure secrets?
