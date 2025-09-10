### What is jenkins and why it is used ?
Jenkins is an open-source automation tool used for CICD. It allows developers to automatically build, test and deploy the code. In DevOps it reduce manual work and integrate with tools like Git and provide pipeline as code for automation.

### Explain the difference between Freestyle Jobs & Pipeline Jobs in Jenkins ?
Freestyle job is nothing but creating job in jenkins console, here anybody can do the changes and we dont have any idea about that. Pipeline job is a code based creation in jenkins console like using groovy script. Here also anybody can do the changes. Nobody is using freestyle now, everybody is using "Pipeline script from SCM"

### How do you configure Jenkins to integrate with GitHub ?
Using WebHook, we can configure jenkins to integrate with Github and we select GitSCM as source while creating job.

### What is a Jenkinsfile and what are its types ?
We have Scripted pipeline and Declarative pipeline. Both the syntax is same, but in Scripted pipeline is old one and groovy will not work in scripted but in Declarative everything will work and the syntax starts with pipeline {}

### How do you handle secrets in Jenkins ?
We use jenkins credentials plugin to securely store passwords, API tokens, SSH keys. We keep this in jobs in environment section to avoid hard coding and can be used anywhere in the stages.

### Can you explain Jenkins Master-Slave (Agent) architecture ?
- Master (Controller) Handles scheduling jobs, managing configurations, UI, and reporting.
- Slave (Agent) Executes build tasks. Multiple agents can run in parallel on different environments.
- This architecture improves scalability, as builds can be distributed across multiple nodes (Linux, Windows,
  Docker, Kubernetes).

### How do you trigger a Jenkins job automatically ?
- SCM Polling, Jenkins polls Git repo periodically.
- Webhooks, GitHub/GitLab sends an event trigger to Jenkins (preferred).
- Cron Syntax, Scheduled jobs (H/15 * * * * for every 15 minutes).
- Parameterized Trigger, Trigger job from another job with parameters.

### How do you integrate Jenkins with Docker and Kubernetes ?
- Use Docker plugin to build images inside Jenkins.
- Run builds inside Docker containers for isolation.
- Push built images to Docker Hub/ECR.
- Use Jenkins Kubernetes plugin to dynamically spin up build agents as pods.
- Deploy applications directly into Kubernetes clusters using kubectl or Helm inside Jenkins pipelines.

### What are Jenkins Shared Libraries ?
Shared Libraries allow teams to create reusable pipeline code (Groovy scripts) stored in a Git repository. Instead of duplicating code across Jenkinsfiles, you import the shared library and reuse predefined functions.

### How do you troubleshoot a failed Jenkins build ?
- Check the Console Output logs for errors.
- Verify job configuration (SCM URL, credentials, plugins).
- Ensure correct build tools (Maven, Gradle, Node, etc.) are installed.
- If running on an agent, confirm agent connectivity.

### How do you implement parallel stages in Jenkins pipeline ?
Using a parallel key word in stages

### What are Jenkins Plugins you frequently use ?
- Pipeline utility steps plugin
- AnsiColor plugin
- Git Plugin (SCM)
- Docker & Kubernetes Plugins
- SonarQube Plugin (code quality)

### How do you integrate Jenkins with AWS ?
- Install AWS CLI and configure IAM credentials in Jenkins.
- Use AWS CodeDeploy, CodePipeline, or S3 plugins.
- Store artifacts in S3 and deploy using CodeDeploy/CloudFormation/Terraform.
- Jenkins pipeline can push Docker images to Amazon ECR and deploy to EKS or ECS.
