### Algorithm for Catalogue (CI)
- Create EC2 for Jenkins-Master, and connect to it in "super putty"
- Create EC2 for Agent and connect to it and install nodejs from the catalogue documentation, it is mandatory
  to install, so that we can install "npm" dependencies.
- Configure Jenkins-Agent and install plugins like AnsiColor, StageView, Pipeline Utility steps, Nexus
  artifact uploader.
- Create EC2 for Nexus and connect to it and download nexus by using "labauto" command
- Create repo in nexus for catalogue to store "catalogue.zip" artifact
- To push artifacts from jenkins to the nexus, we need to download plugin called Nexus artifact uploader, so
  for that we need to give the nexusURL and authentication, make sure to add nexus credentials in the manage
  jenkins.
- This is only the CI part of catalogue, you can see in VS. Untill creation of artifact is CI

### Semantic version
For example 1.0.0 is call semantic version, 1.1.0 is minor version, 2.0.0 is major version like that.

### Nexus artifact uploader plugin
So the created CI pipeline and artifact is in jenkins, how to upload that artifact into the nexus repo ? for that we have nexus artifact uploader, install this plugin in jenkins aswel as write a code in pipeline also.

### Algorithm for Catalogue (CD)
General Deployment of any application is below.
- Create the server.
- Provision the created server using ansible or any other scripting language.
- Stop the server.
- Take AMI.
- Create Launch template version.
- Refresh auto-scaling.
Create separate folder for "catalogue-CD" in VS and also create terraform folder inside the catalogue folder and copy the code of catalogue from the "Terraform-Infra-Dev" into this catalogue folder. First we need to create infrastructure, create atleast vpc, sg, vpn, databases, app-alb in order to work catalogue. Since the catalogue is a private instance, first connect to VPN.

Previously ansible was downloading the package from the s3 bucket and version we are giving hardcode, now ansible should download artifact and version from the nexus, so what should we give to the ansible as input ? "Nexus location and Artifact version" that means first it will call main playbook from the roles, so we need to send artifact version to the ansible playbook from the terraform. So create "Catalogue-CD" iin VS and we keep all the deployment scripts here and write Jenkinsfile for this. When you build with parameter, then this "Catalogue-CD" should send the values of "verison and environment", so how to call another pipeline from the jenkins pipeline using parameters ? For that we have a small syntax, should be used in the CI part in deploy stage "build job: "catalogue-deploy", wait: true, parameters: params".

Jenkins have application version, it should send that version to terraform, How does it send to terraform? So we should create a variable of app_version in variables section

We have a "Upstream job" and "Downstream job"









Industries will follow Semantic version like major version, minor version, patch version
Creating artifacts is nothing but CI

We can install plugin called "rebuilder"
