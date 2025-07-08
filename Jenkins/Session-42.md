### Merge conflicts in Git
If git finds different code in the same line number, git cannot understand, for example below.
- Developer-1 creates 1 branch named as conflict-1 & clone the main branch, and write his code.
- Developer-2 also creates 1 branch named as conflict-2 & clone the main branch, and write his code.
- Now Developer-1 raise PR and got approved from the reviewers, then he will merge into main.
- But Developer-2 is still writing his code, and later he also raise PR, now he will get "This branch has
  conflicts that must be resolved" then he should understand main branch moved forward, so he need to pull
  those changes in local first then resolve conflicts with Developer-1 by discussions then Developer-2 will
  push to the github stating that conflicts are resolved in commit message. Now Developer-2 can merge without
  issue. If you see in conflicts, we can see few lines are from Developer-1 and few lines of code are from
  Developer-2. So Pull before Push is the best strategy because we dont know what other people did it.

### Installation of Jenkins (CICD tool)
- Create 1 instance using t3.small AMI with 30gb, because it is heavy application and use default SG.
- Take Jenkins Public_IP and connect in the superputty (Username: centos ; Password: DevOps321)
- Go to the "Jenkins.io" click on download then select "CentOS" and run the first 4 commands in the server.
  Jenkins is developed on java, so installing java is mandatory in server for Jenkins. No need to install
  jenkins in the agent, java is enough to work for agent, Jenkins-Master not required to know everything,
  but agent should know everything because actual work is done by the agent, However logs will be shown in
  the Jenkins-Master.
- systemctl start jenkins ; systemctl enable jenkins ; systemctl status jenkins
- Take Jenkins instance PublicIP and open in chrome with jenkins port number 8080. Usage: 173.34.65:8080/ in
  chrome, proceed to click on the "continue to site"
- Once you are connected to jenkins, Password will be in the shown path, just cat with root user.
- Install suggested plugins.
- Set the Username and Password then start using jenkins.

Whatever we do in the jenkins we call it as job, nothing but it has some work to do, just create one sample job (or) pipeline in "Freestyle Project" is nothing but everything you do it in UI, this can be done easily. Like for example we can create terraform resources in the aws console also, that is nothing but a free-style and later we started creating resources through terraform scripting, so now create a sample freestyle job take buildsteps as "execute shell" then apply and save and click on "buildnow' and check in the console output. Here build is the main job iam giving to jenkins to work on this. That means i have given a job to jenkins is to just print "hello world" 

### What is the diff btw creating aws resources through aws console and scripting ?
Advantanges are we can control the versions like if something goes wrong we can rollback the changes to the previous version and we have PR process to understand what is happening etc. When you create a jobs in freestyle we dont know who created ? who did the changes ? and restoring is difficult, and maintaining is difficult because it doesn't have any versions etc. So nobody is using free-style but still jenkins is providing the option to create jobs using free-style. 

### What is the diff btw free-style job and pipeline job ?
Free-style job is no one is preffering, since everything can be done from the console and it is very easy for everyone to do the changes and we dont understand who did what changes and it is very difficult to restore to the normal stage because of this we moved to the pipeline.

Now understand the pipeline syntax "Jenkins pipeline" search in google like "Jenkins pipeline" for example create a job with pipeline project and select "hello-world" from the pipeline script just for sample and try to build, you can add any number of stages in the hello-world script. Here if you put the pipeline in the jenkins, here also anybody can come and do the changes, so we have another option called "Pipeline script from SCM". If you put this pipeline in the git then jenkins will automatically pull from the git and build it, we call this as "GitOps" this is the best approch.

Create a project in the VS ---> Learn-Jenkins, jenkins script always start with capital letter "J" as name "Jenkinsfile" and select job as "Pipeline script from SCM" in the jenkins UI and select git from "SCM" and then give the created "Learn-jenkins" git URL in Repository URL. NO need of credentials because it is public and script path as same name created "Jenkinsfile" apply, save and build.  

### Raw syntax of a pipeline interview-question
    pipeline {
          agent {
             node {
                 label 'saikiran-agent'
             }
          }
          stages {
              stage('Build') {
                   steps {
                      echo 'Building...'
                   }
              }
              stage('Test') {
                   steps {
                      echo 'Testing...'
                   }
              }
              stage('Deploy') {
                   steps {
                      echo 'Deploying...'
                   }
              }
          }
          post {
              always {
                   echo 'I will always say hello'
              }
              failure {
                   echo 'This will run if failure'
              }
              success {
                   echo 'This will run if pipeline is success'
              }
          }
    }

### What is agent in jenkins ?
- For example 1 person can do ---> 1 acre land of agriculture.
- If 100 acres ? ---> Then he will recruit employees and distribute the work.
- Similarly if you are using only one project then 1 "Jenkins-Master" is enough, if you have multiple
  projects, 1 Jenkins server cannot handle the load all alone, for that we have agents "Master ---> Agent"
  Here agent is nothing but another server, so create another server in the aws for the agent.

### How do you configure the Master-Agent architecture in jenkins ?
We have multiple agents, we configure them through Manage jenkins ---> Nodes ---> Create node, in this we have one option called "executors" nothing but how many jobs can be run at a time, this depends on instance config as of now we put 3 and "remote root directory" generally jenkins has created a folder in which jenkins entire database is in /var/lib/jenkins/ similarly while creating agent also we need to create a folder for agent and Path should be in /home/centos/jenkins-agent (any-name), because CentOS dont have sudo access in this location /var/lib/jenkins, it has only in the home folder (or) click on the question mark symbol ? there you can see how to give the path. "Labels" we can set multiple lables, as of now agent-1 and we have "Launch methods" 1. Master asking agent to work 2. Agent comming to master and asking for work. We can use any of them, as of now we are going for Master asking agent to work that is nothing but "Launch agents via ssh" that means master is connecting to agent through ssh protocol, then what is the host ? Do we need to give agent Public_IP (or)  Private_IP ? we can give any of them but siva took PrivateIP. Then configure the credentials using Username: centos, click on Treat username as secret and Password: DevOps321, ID = ssh-auth, Host key verification strategy ? ---> Non-verifying verification startegy, that means when you are creating, it will not ask for the prompt, we can add any number of agents like 1 agent is for java, 1 agent is for roboshop, 1 agent is for flipkart project.

### Triggers
We have a "WebHook" is nothing but when there is an event occurs in one system, then it should inform to the other systems, it is called "Event based communication" what is event in this scenario, whenever developer pushes the code to git, then we want pipeline to run automatically, here we have two systems "Git" & "Jenkins" Event will come in git, so Git should have information about jenkins (URL), so go the webhook option in Github in your working repository only, click on add "WebHook" add the jenkins URL must be in the format like "http://12.233.34.53:8080/github-webhook/" --> Payload URL, Content type = Application json, you have multiple events, we can select according to our requirements as of now we selected "Pushes". Similarly in jenkins also we need to check the box "GitHub hook trigger for GITScm polling" and Now try to do changes and see wether it is working or not.

### Environment in Jenkins pipeline
In a Jenkins Pipeline, the environment block is used to define environment variables that are accessible throughout the pipeline or within specific stages. These variables can hold values such as configuration settings, credentials, file paths, API tokens, and more. Instead of repeating values (like URLs, credentials, or file names), define them once in the environment block and reuse. You can see in the Jenkinsfile code i have mentioned example. If you run shell command like "env" in the stage, you will get all env variables you can use as per your requirement. If you want to write shellscript in the stages use sh """ enter """

### Parameters in Jenkins pipeline 
In Jenkins Pipelines, parameters are used to accept user inputs before the pipeline starts. These inputs can be values like strings, choices, booleans, etc. which you can then use throughout your pipeline. Typical use cases for parameters are like choosing build environments (dev, test, prod). When you are using parameters for the first time jenkins is not aware of this params, when you build 2nd time then you will get "Build with parameters" option

### What all sections we have used in the Jenkins pipeline ?
- Agent
- Environment
- Options
- Parameters
- Stages
- Post pipeline conditions

### Points to remember
- You can directly generate keys in .ssh fodler also using "ssh-keygen -f <file_name>"
- No need to install "jenkins" in agents but install "java"
- Post is nothing but after build, what should we do ?
- How many agents you are using in your company ? We are supporting multiple programming languages like java,
  python, nodesjs, .net for each language, we have 2-2 agents.
