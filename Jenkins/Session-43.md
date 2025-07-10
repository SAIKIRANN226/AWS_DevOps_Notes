### Input in Directives
Taking approval before going to the next stage.

### Jenkins file
- If it is a small project, every resources will be in one folder like sg.tf, vpc.tf, ec2.tf files etc. If it
  is a big project then we can keep resources in separate folders (repos) like "Roboshop-Infra-Dev" so that
  we can reduce the refresh time, if we put all resources in one folder then "Refreshing Time" will be longer.
  Incase if we do any small changes also, it will take some time to reflect the resources.
- Go through the example of Jenkinsfile in "01-vpc" in "Roboshop-Infra-Dev" folder, that means we can write
  Jenkins file (or) we can create pipeline for Infrastructure also.
- So create ROBOSHOP-INFRA (anyname) folder in jenkins UI and add VPC in this folder as pipeline project,
  script path should be "01-vpc/jenkinsfile" similarly do for other infra like SG also just for practice.
- You may get ERROR:: Terraform command not found because it is running in the agent and agent dont have 
  terraform, so we need to install few tools in node server like "terraform command" and "aws configure" If
  you are using ony master then install it in master only. While "aws configure" do not configure through root
  user because, master is connecting using centos, it is not taking the sudo access, master may not know
  everything but agent should know everything, because agent will only work here, however the logs will be
  showed in the jenkins-master, but the running application will be in nodes.
- To enable colours we have "ansiColor" plugin keep "ansiColor('exterm')" in the options aswel & install
  plugin in the jenkins console also, manage_jenkins/plugins/available_plugins, make sure to restart jenkins
  in jenkins-master "sudo systemctl restart jenkins"
- We have "when" with parameters condition in Jenkins pipeline (search in google) that means overall we can
  write CICD for infra also like vpc, sg, vpn etc.

Should we keep infra ready to create CICD for applications ? Project infra should be ready what is the project infra ? like vpc, sg, vpn, databases, app-alb, acm, web-alb etc. Whichever are long term that are project infra, whichever are short term those are application infra, so before you do CICD for applications we need to keep project infra ready, so now we should do CICD for catalogue app, for that we should have 1. Catalogue application should be in git and 2. Write a Jenkinsfile for catalogue application.

### CI (Continous Integration)
Continous Integration is nothing but whenever developers pushes the code to the git continously, we should take the code and compile, build, scan, unitesting and saving the artifacts, if CI success then only we should go for CD. What should be stages in catalogue Jenkins file is the below.
- Get the catalogue version first if required
- Clone the catalogue code
- Install Dependencies
- Unit tests
- Multiple types of scans like Sonar scan, SAST, DAST, Open-source etc.
- Build the code
- Publish artifacts to nexus (nexus is a repo to hold artifacts)
- Deploy the code
- Post Build

### CD (Continous Deployment)
- Deploy to Dev/Sit/Uat/Prod environments
- Functional test cases
- Publish the results

Create one separate repo in git and folder in VS for catalogue and keep the catalogue code in this folder, code can be downloaded from the "daws" repository. Refer Catalogue folder in VS, package.json and server.json is the main code of catalogue and write a Jenkinsfile for this catalogue and refer "Jenkinsfile.bkp" for full script. We can see few dependencies are there in package.json and server.json, so we should write a code in pipeline syntax to download those dependencies.

### Build step in pipeline
When you install npm in agent server, a folder (node_modules) will create automatically and all the libraries will come here, when server.js is in run, then it uses node_modules to work. So here zip all files including node_modules and when you unzip in another server, there you NO need to install npm or node_modules. We store this zip file in nexus repository.

### Nexus repository
Storing the artifacts in nexus repository, we dont store code here, we only store the output of the code in the form of zip file. We use "sonatype nexus" because it is popular. So create instance with minumum 2gb ram and 30gb (t3.medium). Generally these installations will be done by SRE Team but we need to know, few companies uses "yum repositories" instead of downloading libraries from the internet, companies will put all libraries in yum repositories to use them, that is why nexus is the single point of contact for the artifacts and libraries.

### Commands to run in the nexus server
- sudo su -
- labauto
- Then select "nexus" (or) type "nexus"
- Select option no.2
- netstat -lntp ---> It will take sometime to open port number of nexus 8081
- systemctl status nexus
- Now take the IPaddress of the nexus server and paste in the chrome with 8081 port
- Sign in process will be same as Jenkins and enable anonymous access
- Now create a repository in the nexus for the catalogue to hold the catalogue artifacts by going to admin,
  then settings options, repositories (here you have lot of options, we can see yum respositories also), so
  create repo with "maven2 (hosted)" is popular format.
- Name: Catalogue (any-name), Version policy: Release/Snapshot/Mixed ---> Snapshot=Dev_env, Release=Prod_env,
  we selected mixed, Layout policy: Permissive, Deployment policy: Allow redeploy because in Dev_env we deploy
  multiple times.
- Now you will get the URL, where we can store the artifacts of catalogue.
- Remove workspace folder in pipeline in post section "deleteDir()" this is must
- What is maven2 format ?
  1. For example 1000 students in a class, is there a chance of
  2. First name is same ? (possible) or
  3. First name + Last name is same ? (may be possible) or
  4. First name + Last name + DOB ? (may be possible) or
  5. So that means at some of time, if you add different combinations, it will become unique
- Similarly we have Project in company and inside the project we have modules like cart module, catalogue etc.
  and they have versions also. So terraform will follow a proper folder structure to store.
  1. Project  ---> Roboshop (with in the company we have a project)
  2. Modules ---> catalogue, cart etc.
  3. Versions ---> 1.0.0. 1.1.0, 2.0.0 etc. will increase versions in future. Using these three we can create
     an artifact ID, for example below
  4. Group_ID ---> Nothing but roboshop group, we give "com.roboshop" in reverse order
  5. Artifact_ID ---> Catalogue
  6. Version ---> 10.0.0
  7. Folder structure be like com/roboshop/version/version files.

### Points to remember
- To get "stageview" in pipeline you need to install plugin called "stageview"
- Declarative pipeline is more simplified than scripted pipeline
- Node modules are mandatory to run the server.js
- Whatever we are writing pipline syntax in VS is nothing but declarative pipeline (latest one) we have old
  one also that is scripted pipeline (groovy will not work in this) so everybody is writing the code using
  declarative pipeline. Declarative pipeline starts with pipeline {}
- To view the pipeline in a stage wise, you need to download the "Pipeline Stage View Plugin"
- To create accesskey and secretkey go to the SecurityCredentials from the profile/users/click on your
  user(saikiranuser)/make sure delete old keys and create new keys and download the csv file for future
  reference, because secret keys will be only view once.
