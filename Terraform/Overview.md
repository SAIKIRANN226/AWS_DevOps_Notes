### Session-25
- What is terraform & why it is used ? In how many ways we configured our project ? Why we prefer ansible
  as configuration management while configuring the big project ? Another name of ansible ?
- Why we din't prefer manual configuration over ansible and shellscript ?
- What are the advantages of terraform ? V,C,A,I,C,A,M,H
- What is Inventory management in terraform ? It is about tracking all the infrastructure resources which
  terraform provisions and manages using terraform state file (Terraform.tfstate). This state file acts like
  a inventory. When you terraform plan or apply. It will compare your desired state with current state.
- What is declarative in terraform and How to install terraform & setup ?
- Install "hashicorp terraform extension" to get colors.
- How to get authentication to AWS to push the created infra ? "aws CLI install"
- You can install aws cli in two ways ? One is regular method of downloading aws cli software and run the
  file in windows laptop & another one is just run the shown commands in cmd.
- How to test wether the aws CLI is installed or not in cmd & gitbash ? "aws --version"
- If credentials are not found, then "aws configure" Before that you need to create terraform administrator
  user in IAM ?
- Where this credentials like Secret-key and Access-key will be saved ? ".aws" folder
- What is the syntax of terrafrom to create any resources & what we call this syntax of terraform ?
- What is the importance of provider in terraform & what is the extension of terraform to save ?
- Where to run the terraform commands ? Terraform commands should be run in gitbash.
- What are the terraform commands and what is their functionality ?
- What is variable syntax ? Is really data-type in variable syntax is important ? NO!
- Go through this https://github.com/daws-76s/terraform
- We can also give Access-key and Secret-keys under region to get authentication to AWS in provider section,
  but why we dint prefer this ? Thats why we "aws CLI" to authenticate ?
- So Dont push the Access-key and Secret-key to the github (or) internet for safety reasons.
- Go through the all files in Terraform folder in VS.

### Session-26
- What is the importance of .gitignore file in terraform ?
- What is the use of terraform.tfvars ?
- How to give terraform.tfvars file from the command prompt for plan and apply ?
- Here terraform.tfvars name is not mandatory we can use any name like "saikiran.tfvars"
- If you dont give -var-file, then terraform will take default values from variables.tf file
- Write a terraform code using terraform.tfvars example ?
- Variable preferences in terraform are below ?
- Command line ---> terraform plan -var="instance_type=t3.small"
- Var_file ---> terraform plan -var-file="saikiran.tfvars"
- terraform.tfvars
- Environment variable.
- Write a terraform code, if mongodb then t3.small & remaining t2.micro using condition ?
- Create instances & route53 records using Count_based loop ?
- Create instances & route53 records using For_each loop ?
- Count_based is to iterate list & For_each is to iterate maps.
- What is function in terraform & what is length function here ? We cannot create our own functions, we
  have to use terraform inbuilt functions only.
- Why output block is used in terraform and what is the syntax of output ?
- Go through the output block in count folder VS ?

### Session-27 
- What is locals in terraform & what is the syntax of the locals ?
- How to call a local in terraform code ?
- What is Data-sources in terraform & why it is used ? How do we search ? For example if you want AMI, then
  "terraform query ami" in google
- Can we query data from the existing resources also apart from the providers ? YES!
- Types of loops ? Count_based, For_each, Dynamic_loop
- What is Dynamic_loop and where it is useful ?
- What is Terraform State (State and Remote state) ?
- What is Declarative state & Desired state ?
- What is Current state in terraform and where it will be stored ? terraform.tfstate
- When Desired state == Current state, then terraform will not take any action.
- When Desired state =//= Current state, then terraform will create.
- Why the terraform will create lock file while terraform is working on it ?
- Explain the concept of local state using example of 2 persons are working on same repo ?
- What errors these persons will face, if they are working on same repo ?
- So terraform will compare my state and devops person state. If both are running terraform apply, here
  duplicates may come & some may get error as already exists.
- So for this issue we have a central state file to check wether the infra already exists or not ? That is
  remote state (S3 bucket).
- Terraform.tfstate is a crucial file, should not delete.
- What are the two disadvantages in local state ? For that only we have a remote state s3.
- So create s3 bucket & lock that bucket using dynamodb table ?
- What are the different remote states we have & why we use only "terraform s3 remote state"
- Where to keep this remote state in terraform code ?
- Another name of remote state ? Backend.
- If we write more lines of script we say configuration is increasing.
- S3 buckets are chargeable in aws, so delete after practice.
- Use different key names in s3 bucket like in the previous you have used different key "foreach" you can use
  as per your wish but not with the same key names because it will merge all.
- Interview question ? We are using S3 bucket with Dynamodb locking, here local state will not work because
  it will create duplicates and errors, security will not be there inside the local. So thats why we have to
  keep it safely in the remote storage like S3 bucket, it will provide better collaboration among the team
  members and errors free.

### Session-28
- How to create multiple environments with terraform in 3 ways ? Using same code but with different
  configuration ?
- First method is terraform.tfvars & what does this do ?
- How do you control different environments in tfvars method ? Using "startswith" function ?
- We create different buckets & dynamodb tables for Dev & Prod in tfvars method.
- And also we create different folders for Dev & Prod in VS.
- Can we use 1 bucket for both Dev and Prod in tfvars method ? YES!
- So create 2 Buckets & 2 Dynamodb tables in aws console in tfvars method ?
- You need to initialize Dev backend while "terraform init" & same for Prod also.
- When you are switching from one env to another env, you must reinitialize it.
- Then you can terraform plan, apply (or) destroy using -var-file
- What if you forgot to give -var-file ? It will load default values from variables.tf
- What if you commented variables.tf file ? It will ask the user to prompt inputs.
- So that you will come to know i forgot to give -var-file.
- Only 1 bucket is created for workspace, inside that it will automatically create a default folder "env:/"
  and inside this env folder, terraform will automatically create Dev/Prod workspaces.
- If you want to know workspace commands just "terraform workspace"
- How to create workspace ? "terraform workspace new dev" do it in gitbash.
- When you are using terraform it has default variable that is "terraform.workspace"
- So we use "lookup" function in workspace method to control different environments.
- lookup(map, key) ---> Giving input as map and passing the key below is the example.
- lookup(var.instance_type, terraform.workspace) ---> 1st one is map and another is key.
- So which approach is better ? Tfvars, Workspace, Different repos for different envs ?
- Provisioners are used to execute the commands on a local machine (or) remote server after it's created,
  typically used for initial configuration like boot strapping.
- Provisioners are used only for instances (or) EC2.
- What is local-exec provisioner in terraform & what is the syntax ? It enables a keyword ${self.id}
- Local-exec --> Run on your local machine --> Use case is to notify, trigger local scripts etc --> No
  remote access is need.
- What is remote-exec provisioner in terraform & what is the syntax ?
- Remote-exec --> Runs on your remote server --> Use case is to install softwares, configure ec2 post setup,
  need SSH/WinRM to access remote host.
- What is the disadvantage of local-exec ? Local-exec provisioner runs only one time not every time.
- Provisioners are useful to integrate terraform with configuration management tools like ansible to get end
  to end automation.
- We can write multiple provisioners also like for example "on_failure = continue" nothing but same as ignore
  errors in ansible.
- What is the difference between Terraform and Ansible ?
- We can also create ec2 instances using ansible but it does not have state file as terraform does, that is
  why terraform is best for creation of infrastructure & ansible is best for configuration management.
- What is Creation time & Destroy time in terraform ? Why we use them ?

### Session-29
- What is Module Development in terraform & what is the syntax ? Go through the code of EC2 module in
  Terraform-modules in VS. Here provider.tf will not be there in module developing.
- How many types of Modules and How many types of Roles are there ?
- It is DevOps engineer responsibility to write README.md file to let others know how to use module.
- Create a VPC in aws console ? CIDR (10.0.0.0/16)
- Google has given some PrivateIP address ranges those only allocated to PrivateIP not for PublicIP,
  there you can see 24,20,16 bit-blocks.
- Even ISP people will configure your PrivateIP address in any range among these 3 bit-blocks only.
- We can select any range, but siva selected as 10.0.0.0/16 range.
- Atleast you need to create 16 servers to use VPC, 10.0.0.0/28 ---> 16 servers, 10.0.0.0/16 ---> 65k
  servers, generally we give VPC CIDR as 10.0.0.0/16 only, because it does not cost anything, so we can
  go for maximum.
- Create Public subnet in aws console ? CIDR 10.0.1.0/24
- Create Private subnet in aws console ? CIDR 10.0.2.0/24
- Create Database subnet in aws console ? CIDR 10.0.3.0/24
- Create Public, Private & Database route tables in aws console ?
- And associate Public, Private & Database route tables with their respective subnets ?
- Give internet access to the Public subnets.
- Enable Auto-asign public IPv4 address only to the Public subnet.
- Create Internet Gateway and attach to your created VPC in aws console ?
- What is the difference between Public subnet and Private subnet ?
- CIDR (Classless Inter-Domain Routing) ? We can asign custom IP address range to the subnets.
- Use always terraform best practices for naming convention like using "_" avoid double naming.
- We used Open source modules sometimes, we have dedicated cloud team who develops module & we use them.
- How do you check internet is working or not ? ping google.com, Ipv4 is 32bit & Ipv6 is 64 bit.
- Router (Internet Gateway) ---> It has PublicIP & PrivateIP. PublicIP is nothing but just type what
  is my ip in google, there you can see Ipv4 address that is your PublicIP, not ipv6. What is your PrivateIP
  just ipconfig in cmd there you can see IPv4 address Under wireless LAN adapter Wifi.
- What is your actual IPaddress ? Just type in google what is my IP, if anybody wants to connect to my
  laptop you can connect using this IP address only. You cannot connect with PrivateIP address.
- AWS wont charge for VPC, subnets, route tables, it only charges when you are creating server.
- We can create as many private subnets we want, however for functionality purpose we have only two subnets
  which is Public & Private subnets.
- Watch from 26:11 to 1:14:21 to understand how VPC works.

### Session-30
- What resources we have created inside the VPC in aws console ?
- First we have created VPC in aws (Your created VPC is Isolated, even aws dont have access to it). It is
  like your Private Data-Center in aws cloud.
- Created Internet Gateway (IGW) and attached to the VPC.
- Created Public, Private & Database subnets in atleast 2-AZs for High Availability.
- Created Route tables (Public, Private & Database) & associated it with their respective subnets in both
  regions 1a and 1b.
- Added Internet Gateway route in Public Route table, because internet should be enabled in Public not in
  Private, that is the difference between Public and Private subnets.
- Enabled Auto-asign Public IPv4 address only to the Public subnet not to the Private subnet.
- When you create a VPC, a default route table also known as main route table is automatically created
  to that VPC. It contains a local route that enables communication with the subnets within the VPC. While
  this default route table cannot be deleted, its routes can be modified and custom route tables can be
  created and associated with specific subnets to provide more granular control over network traffic.
- What is NAT Gateway and why it is used ?
- NAT Gateway should be created in Public subnet (1a or 1b) and why only in Public subnet ?
- Creating NAT Gateway is not enough we need to add routes between Private subnets and to the Internet
  gateway (NAT) which is in Public subnet.
- Which ever Private subnets like Database subnet (or) any other Private subnets wants to connect to the
  internet, they should add route to the NAT gateway which is in Public subnet. How to add routes is
  the below line ?
- Select any of the Private subnet/Routes/Edit routes/Add route (Destination = 0.0.0.0/0, Target = NAT
  gateway, then select default one in dropdown under Target section only)
- When you create a NAT gateway, aws will create instance in the background, We dont have access to that
  instance, this instance IP is dynamic, whenever you off and on. So create ElasticIP for this instance first
  and then create NAT Gateway.
- NAT and ElasticIP is chargeable, so delete after practice.
- Can we get StaticIP for this instance ? YES! we can get but it is very costly thing.
- Even your home PublicIP is Dynamic. If you want StaticIP, you need to pay money to ISP provider.
- What is VPC peering and what is the condition to create VPC peering connection ?
- Create a VPC peering connection between Roboshop_VPC & Default_VPC
- So let us take Requestor VPC = Roboshop VPC ; Acceptor VPC = Default VPC
- Accept request in the same account and then add routes in VPC.
- Try to add routes in main route table, because it is the default route table which is created automatically   to communicate between the subnets, if not reflecting, then add explicitly ?
- If you want only one (or) two Private subnets wants to connect to the vpc peering main road then you can
  add in those two route tables only.
- You need to add from the other side also not just one side. This is nothing but routes in VPC.
- Go through the Terraform-aws-vpc-module, how we developed VPC & resources inside it.
- We have a Tagging strategy because we have more resources, so we use better tagging strategy.
- We have Common_tags and Resource_tags ? What is the difference between them ?
- We used merg function in tagging strategy to merge Common_tags & Resource_tags.
- You can also create s3 bucket in VPC module development.

### Session-31
- Go through the code of Terraform-aws-vpc-module in VS.
- While developing VPC module, we come across Peering section, is really Peering connection is required ?
  Peering may not require for everyone, when this Peering is useful ?
- By default Peering connection between two VPC is not possible.
- If we want to connect with the resources which are in another VPC, then you require peering.
- How to connect to other VPC which is in another company ? Install VPN in Default_VPC & Connect.
- Example consider Requestor is Roboshop & Acceptor is User provided VPC or Default VPC.
- In VPC peering, when you are adding routes in VPC, if acceptor VPC is not in our control what you will do ?
  We should inform them to add the acceptor route in their terraform code.
- Big companies depends on multiple companies to deal different modules.
- So users can decide if peering is required or not ? If required they have to give VPC peering id, if they
  are not giving, we should consider default VPC. Go through the peering.tf file
- Overall developing your VPC module is completed & you pushed it to the internet (Github), then how to refer
  this ? source = "git::<https_URL>ref=main"
- So when you do terraform init the module will be downloaded in where we are testing the code & it will
  automatically create a folder called module.
- Till now we used Allow-all method while creating SG, but now we use strict rules.
- How to use Security Groups effectively according to the Roboshop documentation ?
- We install VPN in Default_VPC to connect to Private instances which are Present in Roboshop_VPC.
- We can create a folder (Example) & keep all the testing code in it, so that it will be easy for everyone to
  use the module.
- We keep all our resources in 1a zone.
- In VPC module developing, we need to publish outputs then only users can get the information.
- We have a Database subnet group, because Databases have different behaviour, nothing but just adding
  database subnet ids.
- We also have Open source modules for VPC, if you search in google you can use that also, instead of
  developing, but for practice you need to know.

### Session-32
- Till now we used Allow-all method while creating SG, it is just for practice only, but now we need to
  follow strict SG rules according to the Roboshop Documentation only.
- We have developed our own customized module for creating VPC right ? In this session also we are going
  to develop our own customized module for SG. Refer Roboshop-aws-sg-module in VS.
- We created Security groups & SG rules for all components according to the Roboshop Documentation.
- Why we created separate folders for every resources in Roboshop-terraform ? Refresh time
- Since they are in separate folders, consider they are like different projects.
- Go through 01-vpc, 02-sg, 03-vpn, 04-ec2 code in Roboshop-terraform in VS.
- What is the main input required to create a SG ? VPC_ID
- For example in Big companies, 1 team is taking care for VPC, another team is taking care for SG etc. How do
  you get the information of resource which is in another team, project, folder ? SSM Parameter store
- What is SSM Parameter store in AWS systems manager ? Configuration storage.
- What does Configuration storage (or) Central storage do ?
- What is the Naming convention while storing Configuration (or) Key-Value pair in SSM ?
- Generally Naming format will be in linux structure like /roboshop/dev/vpc_id
- As we know Data-sources is used to query the data dynamically from the providers & also from the existing
  resources right ? But to query from the existing resource, we need to give some input like vpc_id, this
  vpc_id we cannot get from the data source, but we used data source only to query the default vpc_id, but to
  take the created vpc_id, again data-source is not an option, because we need to give vpc_id as input.
- Since VPC is in different folder, how do we get vpc_id in SG ? You need to store vpc_id in SSM Parameter
  store first & then read that saved Key-Value in SG using data-source option.
- Generally it is not mandatory to create ingress rules while creating SG & why ? But egress is static
  because this traffic is creating from our server, mostly it will be constant.
- In real time, whenever you want few ports to open, you need to write a mail to firewall team, then they
  will open the port, if they are using terraform they will do changes in main.tf file
- In Security groups, we have two names "Name" & "Security group name" what is the difference ?
- As a module developer, you must output the resources in output.tf file like IDs etc. So that other teams
  will use it.
- Now creating all Security groups according to the Roboshop Documentation, Mongodb --> Should accept
  connections from Catalogue & User, what should be the ingress (Security group rule) of mongodb now ? Source
  should be the CatalogueIP & Port 27017, Similarly for User also.
- Is CatalogueIP is constant everytime ? NO! then what should we do ? We need to take the ElasticIP which
  is very costly, because we have 12 Private servers, that means we need to create 12 EIPs. If it is Big
  project, we may need to create thousands of EIPs, this will generate huge bill to the company.
- So Security group has given 1 option, first create Mongodb & Catalogue Security groups.
- Then go to the Security groups in aws console & select created mongodb SG/Edit inbound rules/Add rule
  Type --> Custom TCP, Port 27017 & in source just type "sg" next to the custom, you will get the created
  SGs, in that select already created Catalogue SG. Same for the User also.
- Now write a terraform code for all the SGs according to the Roboshop Documentation.
- Now creating EC2s for the roboshop 04-ec2 in VS, using Open-source module from the internet.
- Here the only disadvantage is you cannot connect to this Private instances using SSH, because Private
  instances dont have PublicIP. We have two options Jump host & Installing VPN in Default VPC to connect
  to private instances which are in Roboshop VPC, but make sure you have Peering connection between
  Default VPC & Roboshop VPC.

### Session-33
- What are the two ways to connect to Private Instances ? Jump Host & VPN
- How to connect to Private Instances using VPN ?
- In which VPC should we install OpenVpn (or) create server for VPN ? Default_VPC
- We must have a peering connection between Default_VPC & Roboshop_VPC.
- All our private instances are in Roboshop_VPC only.
- How the traffic is routing from Home server to Private instances ?
- What is the SG rule when mongodb is accepting connections from OpenVpn ?
- Make sure to enable VPN in all private instances by giving SG of OpenVpn instance to all private instances.
  Add SSH rule.
- How to install OpenVpn in server & connect to it ? Configuring VPN is not our responsibility, we have
  separate team for this. We use Cisco VPN in our company. Which is costly, but for practice we used OpenVpn
  Connect.

### Session-34
- We have created VPC, Security groups, VPN, Instances. So now we want all instances to automatically
  configured, for that we need to create ansible server in default subnet (Default VPC) this server will
  provision all instances using ansible playbooks & also create SG for ansible on port SSH 22 to connect to
  all instances securely.
- For this we need to write a small shellscript to provision the instances ec2-provision.sh in VS. No need to
  give sudo access in this script, because userdata will get sudo access automatically but in provisioners we
  need to give sudo access.
- There is one disadvantage in user-data, if user-data fails one time, it will not come again, so we will
  address this issue with provisioners. So delete ansible-server & do again terraform init, plan, apply.
- User-data logs will be in sudo cd /var/log/, ls -la, tail -f cloud-init-output.log
- LB (Target groups & Rules) and Launch templates (Auto scaling & Policy)
- First create 2 nginx servers, while creating add user-data like #!/bin/bash yum install nginx -y mkdir -p
  /usr/share/nginx/html/ui echo "<h1GreaterthanSymbolHi we are from UI team<h1GreaterthanSymbol" >
  /usr/share/nginx/html/ui/index.html systemctl restart nginx.
- We are using Application LB becasue it is most intelligent and Classic LB is very old.
- Create LB security group, here from where the tarffic is coming to this LB ? From the internet, therefore
  ingress rule should be http & cidr is 0.0.0.0/0
- Create SGs for these two nginx servers, these servers will get request from LB, therefore ingress rule
  should be a SG which is attached to LB.
- Create target groups for example UI, UX in Listeners first, then register using include as pending in
  default subnet.
- Now create Load Balancer with port 80 in Default_VPC subnet with min two AZs.
- Rules in Load balancers, there is default rule, you can add as many rules you want, you can put path as a
  condition in this UI/UX example, if path is /ui/* then send to UI target group. Keep Priority as 1.
- Load Balancer will give us a DNS name, generally we configure this name in route53 record, so create a new
  record, copy the DNS name & paste, and you need to keep Alias and select Alias to Application & Classic
  Load Balancer.
- Mostly in companies, errors are not because of coding, it is because of configuration change, even if we
  make small changes in configuration, we get errors, so thats why we need to keep config independently in
  SSM Parameter store (Central storage or Configuration storage)
- SG is very important, since we are connecting to every resources present in aws.
- Individually we can understand every concept, but when we configure the project using all concepts, it will
  create huge confusion, like for example if we give a request from client (or) from our laptop, the request
  should reach to the end service which is present in aws, request will cross many stages like client-side
  configuration should be clear, vpc, igw, subnets etc. have many resources to cross to reach the end
  service. So this visualization should there in us. Thats why SG is important to use in every resources.
- No Problem if you delete ".terraform" folder and lock file.
  
### Session-35
- Understand the concept of 3-Tier architecture diagram.
- Start a project Roboshop-infra-Dev in VS, this is for Dev environment, as this is multi-env, you have
  three options like Tfvars-method, Workspaces-method & Different repos for different env, present siva is
  now creating using different repos for different env method. Every method has pros & cons, you can tell
  this in interview. We also need to create for SIT, UAT, PROD. So any project starts with VPC.
- We keep Web-ALB in https on port 443, because it is facing to the public. App-ALB is private LB, since this
  App-ALB is in our network, we can keep this in http on port 8080
- No direct connections now, only through LB.
- We use Auto-scaling only for frontend & backend. For Databases we use RDS, DynamoDB etc.
- Creating Databases using PULL strategy. We have one disadvantage in PUSH. Once we pushed the configuration
  from the ansible server to the nodes and if the configuration is disturbed or anybody do changes in
  ansible server, we dont have any idea, so ansible implemented PULL architecture aswel, we can schedule a
  crontab to PULL the configuration periodically from Git not from the ansible-server and run it, since
  ansible is idempotence in nature, even if it runs the program multiple times nothing will happen. So go
  through the code of Roboshop-ansible-roles-Terraform in VS.
- Why we use terraform provisioners (Null resource) instead of user-data ? Because we dont know wether the
  user-data is succeeded or not until we see the logs in server and moreover it will run only one time. But
  in provisioner we can see on terminal if bootstraping is happening or not ?
- Every platform like azure, gcp or aws cloud platform will have its own solution to maintain configuration
  and secrets, in aws cloud we have more resources like ec2, dynamodb, lb etc. So for every service you may
  use passwords or any other secrets in the configuration at some point of time like in mysql we have
  password Roboshop@, so we have SSM Parameter store, services will refer this.
- For example in aws cloud, EC2 is a service and if this EC2 wants to retrieve the configuration or passwords
  which are present in the SSM Parameter, then this EC2 must have access to that SSM right ? for that only we
  give roles to the EC2 in IAM. Second thing is here we are using ansible to provision servers, so ansible
  should pull the configuration or passwords whatever present in the SSM Parameter, which is present in aws,
  then ansible should connect to the aws first, that means ansible should download "boto3 and botocore
  python" modules. Third thing is ansible-server should also have IAM role (or) IAM policy to PULL the
  configuration or passwords from the AWS. If these 3 things are there, we can implement vault.
- IAM role we have given in the code is iam_instance_profile = role-name, present this role has full admin
  access, later we can restrict in IAM concepts.
- We store passwords in SSM Parameter by manual only not automated.
- So first store the password in SSM Paramater, for example we have root_password in mysql right ? so store
  that and naming should be "roboshop/dev/msql_root_pass" and use "secure string" and value should be the
  password itself "Roboshop@1", so here ansible should retrieve this password, for that we have a syntax
  called "lookup" put this syntax in the ansible-roles, where ever this password is there.
- If you go manually like ansible.builtin.command/shell there is one disadvantage, there will be no
  idempotence behaviour, thats why mostly use module only. If there is no official modules from ansible, we
  can use community modules.
- Web & App tier (If traffic increases, Auto-scaling will create instances)

### Session-36
### Session-37
### Session-38
### Session-39
### Session-40
