### Session-42
- How to install Jenkins in server ?
- Installing java in Jenkins is mandatory because jenkins is developed on java only, but no need to install
  jenkins in agent (Java is enough for the agent to work).
- Jenkins-Master may not required to know everything, but agent must know everything because actual work is
  done by the agent only, however logs will be shown in Jenkins-Master.
- Jenkins port number is 8080, Nexus port number is 8081
- What is Free-style project in Jenkins ?
- What is the difference between creating aws resources in aws console & through code ?
- Difference between Free-style job & Pipeline job ?
- Create a job first using Free-style & then Pipeline ?
- What is Pipeline script from SCM or GitOps ? 
- Write a RAW syntax of a Declarative pipeline ?
- What is agent in Jenkins ? How many agents are required ?
- How do you configure Master-Agent architecture in jenkins ? Manage jenkins, nodes, create node, executors,
  remote root directory, labels, launch methods, host, configure credentials, host key verification strategy. 
- Where does the entire jenkins database will be ? /var/lib/jenkins, similarly we need to create a directory
  for agent also in /home/centos/jenkins-agent (Any-name) because CentOS dont have sudo access in
  /var/lib/jenkins, it has only in home folder (or) click on question mark ? symbol, there you can see how to
  give the path.
- How many agents you are using in your company ? We are supporting multiple programming languages like java,
  python, nodesjs, .net for each language, we have 2-2 agents.
- Triggers in Jenkins pipeline ?
- Environment in Jenkins pipeline ?
- Options in Jenkins pipeline ?
- Parameters in Jenkins pipeline ?

### Session-43
- Difference between Scripted pipeline & Declarative pipeline ?
- Input option in Jenkins pipeline ?
- Create a Jenkins file in infra for vpc. Use terraform init, plan, apply. Use input option before apply.
  Since this pipeline is running on agent. We need to install terraform command & aws credentials (Aws
  configure) in agent server. While aws configure dont take sudo access because jenkins-master is connecting
  to agent using centos. Search in google like install terraform linux.
- To get colours we have a plugin called ansiColor('xterm') in options itself. So install this plugin in
  manage jenkins, plugins. Also write a code in jenkins file in options. If plugins are not working even after
  installing just do systemctl restart jenkins.
- Jenkins pipeline when with parameters.
- That means overall we can write CICD for infra also. But in this project we are creating infra in normal way
  like using terraform in gitbash. We create CICD for only applications like catalogue, shipping etc.
- Before doing CICD for application infra, project infra should be ready.
- What does CI part & CD part stages in application like catalogue ?
- What is pipeline utility steps plugin ? To read the Json file.
- Next is installing dependency ? Installing nodejs (From the roboshop documentation) in agent is mandatory
  in order to install npm dependency.
- Next zip (Build) the above catalogue output code nothing but artifact & store in nexus repository.
- We use Sonatype nexus because it is a widely adopted and reliable artifact repository manager. Create an
  instance with a minimum of 2GB RAM & 30GB storage (T3.medium). While the actual installation is typically
  handled by the SRE (Site Reliability Engineering) team, it's important to understand the concept. Dont worry
  about installation or updates. What is internal YUM repositories ? This is why Nexus acts as a central point
  not only for storing build artifacts but also for serving as a local repository for all required libraries
  and dependencies.
- Now create a cataloge repository to hold the catalogue artifacts using "maven2 hosted" format. What is
  maven2 hosted format ? It is popular format, used for maintaining application artifacts in unique way. Group
  id ---> com.roboshop, artifact id ---> catalogue, version ---> 1.0.0. Folder structure be like
  com/roboshop/catalogue/version folder 1.0.0, 1.0.1, 2.0.0 etc.
- We have version policy Release (Prod), Snapshot (Dev), Mixed (Both)
- Allow redeploy in Deployment policy because we are in dev.
- Now we get URL of that repository.
- Remove workspace directory after pipeline success.
- Install "Pipeline Stage View Plugin" in jenkins.
- How to create any file as backup ? Example Jenkinsfile.bkp (or) main.tf.bkp

### Session-44
- We have artifact in jenkins, how to push this to catalogue nexus repository ? We have Nexus artifact
  uploader plugin, install this in jenkins UI & also keep the code in jenkinsfile.
- What is the Algorithm for Catalogue (CI) ?
- What is the Algorithm for Catalogue (CD) ?
- Go through the code of Catalogue CI & CD in VS.
- What is Upstream (CI) & Downstream (CD) in jenkins pipeline ?
- How to call another pipeline from jenkins pipeline ? Using Buildjob
- You need to attach vpn SG to the agent, because catalogue is accepting connections from vpn.

### Session-45
- Types of scannings in jenkins pipeline ? Static source code analysis, Static Application Security Testing
  (SAST), Dynamic Application Security Testing (DAST), Open Source Library Scanning, Docker Image Scanning.
- We are using "Shift-Left" method, we do all types of scannings in Dev enviroment itself, to make sure
  everything is ok, then only we can go for the higher environments.
- How the Sonarqube scanner will work ? Installation of sonarqube is taken care by SRE team. Jenkins-Agent
  will clone the code in his server, and jenkins agents have scanner cli software which need to be installed,
  it will scan the code and upload to the "Sonarqube" console (or) server. Then developers will see the
  results in "Sonarqube" console (or) server.
- Port number of sonarqube is 9000.
- Sonar-project.properties ?
- Quality Gates in sonarqube (We keep some standards) ?
- What is multi branch pipeline ? We are using multi branch pipeline in jenkins.
- What is Jenkins shared library ? What is the process ?
- For example developers are the owner of the catalogue repository, but jenkinsfile will be managed by the
  DevOps engineer only. So DevOps engineer doing frequent changes in devops repo (Catalogue) is not good. For
  this only we have jenkins shared library (Centralized pipeline). For example if we have 20 repos we need to
  write same jenkinsfile for every repo, instead we can create and maintain the shared library repo (Groovy
  code, reusable pipeline steps). We can keep all multiple pipelines in jenkins shared library for different
  languages and deployment platforms.
- We need to inform this Jenkins shared library repo to the jenkins by going to the manage jenkins, system,
  global pipeline libraries, add here, default version should be main and name (Any-name), project repo should
  be git URL. Refer this library in jenkins pipeline using @Library('roboshop-shared-library'). We use groovy
  syntax in jenkinsfile #!groovy
- How to call these pipelines ? For example nodejsVM, javaVM, pythonVM is a centralized pipeline, we need to
  send parameters like what type of application and component to "pipelineDecission.groovy"

### Session-46
- 
### Session-47
