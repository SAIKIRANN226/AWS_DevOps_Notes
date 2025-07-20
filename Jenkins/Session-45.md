### Types of scannings in Jenkins pipeline
- Static Source Code Analysis ---> Is a method of debugging the source code of a program without executing it.
  It will find the potential bugs, security vulnerabilities, code quality issues, and ensure we are meeting the
  project or company standards or not ? "Sonarqube" is the most popular tool for this testing.
- Static Application Security Testing (SAST) ---> Mainly focus on the security without executing the program to
  identify security vulnerabilities early in the software development lifecycle (SDLC). "Fortify" is the tool.
- Dynamic Application Security Testing (DAST) ---> Like if anybody hacks how they test the application, same
  intense testing will be done by DAST while application is running in Dev itself & the tool is "Web inspect"
- Open Source Library Scanning ---> We get all the libraries from the internet right ? to scan these we use a
  tool called "Nexus IQ"
- Docker Image Scanning ---> We have "TwistLock" or "ECR Scanning"
- We are using "Shift-Left" method, we do all types of scanning in Dev enviroment itself to make sure
  everything is ok, then we can go for higher environments.
- All the tools are costly except Sonarqube and Docker, so we used only these two as of now.

### Sonarqube installation and setup
- First create 1 instance for Sonarqube (t3.medium) with 30GB, actually this should be taken care by
  SRE team only.
- Take sudo access "sudo su -"
- Then "labauto" command
- Select the number for 60 which is "sonarqube"
- Then "netstat -lntp" to know the port of sonarqube (9000)
- Now take the IP address of sonarqube with port 9000 and enter into the URL
- Username: admin ; Password: admin
- Then change the password
- When you login then you can see the console that is nothing but "Sonarqube" console (or) server.
- Install "scanner cli" in agent-server then sudo su - ; labauto ; select 61 (sonar-scanner)
- In which location this sonar-scanner will install ? /opt/sonar/conf
- vim sonar-scanner.properties, here give the sonarqube URL like "http://44.333.22.206:9000" here publicIP
  is changing, so better to give privateIP
- Next give the login information by generating token sonarqube console My_account/Security.
- In this token only, sonarqube authentication will be there, just enter & "sonar.login=token_number"
- Now sonar-scanner cli will able to publish the results into the sonarqube console.

### Sonar-project.properties
If you want to configure in pipeline, you need to create this file. Go through the code in VS. sonar-scanner is the command to read sonar-project.properties to scan the code and uploading the results

### Quality Gates in sonarqube
As a devops engineer, we need clean code like 0 bugs, 0 code snells, security rating should be A, code coverage should be 80 etc. to deploy into the production. So create a Quality Gate (any-name) and add condition On Overall Code, here we need developer to choose among different options, but rightnow we are going for one option "Condition coverage" and value 80, and also add another condition like code snells should be 0, vulnerability should be 0, bugs should be 0, maintainability rating should be A, security rating should be A. So in this way you can add any number of conditions by sitting with developer. You can also keep same conditions for new code also and click on the "Set as Default". If quality gates failed, should we fail the pipeline ? or inform developers to fix this code ? we need to inform developers. So we should keep a condition in the pipeline (sonar-project.properties) to fail the pipeline "sonar.qualitygate.wait=true" node modules are comes from internet, so no need to scan node_modules directory here, so we put this line of code in properties "sonar.exclusions=node_modules**

### How the Sonarqube scanner will work ?
- Note that same process for any scanning tools.
- Jenkins-Agent will clone the code in his server, and jenkins agents have scanner cli software which need
  to be installed, it will scan the code and upload to the "Sonarqube" console (or) server.
- Then developers can see the results in "Sonarqube" console (or) server.

### Actual scenario in the company
In Git we have multiple branches, so single pipeline will not work, we need to create multi-branch pipeline. We have language (catalogue is node js) and deployment platform (we can deploy in aws vm, docker,kubernetes, or on-premise). Depends up on these two, we need to create pipeline because different languages and deployment platforms have different commands. For example HDFC bank have 200 projects and many microservices, here if you write a pipeline for node js and VM, it should applicable to all node js and vm projects instead of duplicating the pipeline, nothing but if you want to add one small stage in the pipeline, you cannot add in all the multiple pipelines right ? so instead we can change at one place and it will applicable to all node js and vm projects, this is same as terraform modules for reuse. So for this only jenkins has given an option called "Jenkins shared library" treat your pipeline as library and use it where ever you want.

### Process for the above concept
- Create a feature branch in catalogue
- Configure multi-branch pipeline
- Configure Jenkins shared libraries

### Jenkins shared library (centralized pipeline)
Go through the code of "Roboshop-shared-library" in VS, here we can write our pipelines with minimum code. Inside the vars folder, we created a centralized pipeline "nodejsVM.groovy" this pipeline will work for all nodejs and VM projects, we need to call this in jenkins pipeline. We need to inform this Jenkins shared library repo to the jenkins by going to the manage jenkins/system/global pipeline libraries/add here default version should ne main, and name (any-name)/project repo should be gut URL. Refer this in jenkins pipeline using groovy syntax. We have created a centralized pipeline for nodejsvm, we need to send parameters, similarly we can also create for javavm/pythonvm/govm etc.

### PipelineDecission.groovy
We need to decide which pipeline to call here.

### Points to remember
- For Jenkins, database will be stored inside the server in /var/lib/jenkins, but for Sonarqube especially
  in production env, the storage will be in databases like postssql, mysql. That means Sonarqube configuration
  will be stored in these databases only.
- So we have a developer version for sonarqube, we can install in the server without database.
- You can create multiple quality gates in sonarqube
- How to backup the jenkinsfile ? "Jenkinsfile.bkp"
- You should say we are using multi-branch pipeline in jenkins
- Who is the owner of the catalogue repo ? developer is the owner not devops engineer.
