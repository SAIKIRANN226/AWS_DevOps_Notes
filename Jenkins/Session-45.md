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
- In which location this sonar-scanner will install ? 


### How the Sonarqube scanner will work ?
- Note that same process for any scanning tools.
- Jenkins-Agent will clone the code in his server, and jenkins agents have scanner cli software which need
  to be installed, it will scan the code and upload to the "Sonarqube" console (or) server.
- Then developers can see the results in "Sonarqube" console (or) server.




### Points to remember
- For Jenkins, database will be stored inside the server in /var/lib/jenkins, but for Sonarqube especially
  in production env, the storage will be in databases like postssql, mysql. That means Sonarqube configuration
  will be stored in these databases only.
- So we have a developer version for sonarqube, we can install in the server without database.
