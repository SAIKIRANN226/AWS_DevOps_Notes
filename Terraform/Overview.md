### Session-25
- What is terraform and why it is used ? and In how many ways we configured our project ? and why we prefer
  ansible as configuration management while configuring the big project, another name of ansible ?
- Why we din't prefer manual configuration over ansible and shellscript ?
- What are the advantages of terraform ? V,C,A,I,C,A,M,H.
- What is declarative in terraform and How to install terraform and setup ?
- Install "hashicorp terraform extension" to get colors.
- How to get authentication to AWS to push the created infra ? "aws CLI install"
- You can install aws cli in two ways ? one is regular method of downloading aws cli software and run the
  file in windows laptop and another one is just run the shown commands in cmd.
- How to test wether the aws CLI is installed or not in cmd & gitbash ? "aws --version"
- If credentials are not found, then "aws configure" Before "aws configure" you need to create terraform
  administrator user in IAM ?
- Where the credentials like Secret-key and Access-key will be saved ? in ".aws" folder
- What is the syntax of terrafrom to create any resources & what we call this syntax of terraform ?
- What is the importance of provider in terraform & what is the extension of terraform to save ?
- Where to run the terraform commands ? Terraform commands should be run in gitbash.
- What are the terraform commands and what is their functionality ?
- What is variable syntax ? Is really data-type in variable syntax is important ? NO!
- Go through this https://github.com/daws-76s/terraform
- We can also give Access-key and Secret-keys under region to get authentication to AWS in provider section,
  but why we dint prefer this ? Thats why we aws CLI to authenticate ?
- So Dont push the Access-key and Secret-key to the github (or) internet for safety reasons.
- Go through the all files in Terraform folder in VS.

### Session-26
- What is the importance of .gitignore in terraform ?
- What is the use of terraform.tfvars ?
- How to give terraform.tfvars file from the command prompt ? for plan and apply.
- Here terraform.tfvars name is not mandatory we can use any name like "saikiran.tfvars"
- If you dont give the -var-file, then terraform will take default value of variables.tf file
- Write a terraform code using terraform.tfvars example ?
- What are the variable preferences in terraform ?
- Command line ---> terraform plan -var="instance_type=t3.small"
- Var_file ---> terraform plan -var-file="saikiran.tfvars"
- terraform.tfvars
- Environment variable.
- Write a terraform code, if mongodb then t3.small and remaining t2.micro using condition ?
- Create instances and route53 records using Count_based loop ?
- Create instances and route53 records using For_each loop ?
- Count_based is to iterate list and For_each is to iterate maps.
- What is function in terraform and what is length function here ? We cannot create our own functions, we
  have to use terraform inbuilt functions only.
- Why output block is used terraform ? and what is the syntax of output ?
- Go through the output block in count folder VS ?

### Session-27 
- What is locals in terraform and what is the syntax of the locals ?
- How to call a local in terraform code ?
- What is Data-sources in terrafrom and why it is used ? How do we search ? for example if you want AMI, then
  "terraform query ami" in google
- Can we query data from the existing resources also apart from the providers ?
- Types of loops ? Count_based, For_each, Dynamic_loop
- What is Dynamic_loop and where it is useful ?
- What is Terraform State (State and Remote state) ?
- What is Declarative state and Desired state ?
- What is Current state in terraform ? and where it will be stored ? terraform.tfstate
- When Desired state == Current state, then terraform will not take any action.
- When Desired state =//= Current state, then terraform will create.
- Why the terraform will create lock file while terraform is working on it ?
- Explain the concept of local state using example of 2 developers are working on same repo ?
- What errors these developers will face, if they are working on same repo ?
- So terraform will compare my state and devops person state. If both are running terraform apply,
  here duplicates may come and some may get error as already exists.
- Terraform.tfstate is a crucial file, should not delete.
- What are the two disadvantages in local state ? for that only we have a remote state s3.
- So create s3 bucket and lock that bucket using dynamodb table ?
- What are the different remote states we have ? and why we use only "terraform s3 remote state"
- Where to keep this remote state in terraform code ?
- Another name of remote state ? we can also call as Backend.
- If we write more lines of script we say configuration is increasing.
- S3 buckets are chargeable in aws, so delete after practice.
- Use different key names in s3 bucket like in the previous you have used different key "foreach"
  you can use as per your wish but not with the same key names because it will merge all.
- Interview question ? We are using s3bucket with dynamodb locking, here local state will not work
  because it will create duplicates and errors, security will not be there inside the local. So thats
  why we have to keep it safely in the remote storage like s3 bucket it will provide better
  collaboration among the team members and errors free.

### Session-28
- How to create multiple environments with terraform in 3 ways ? Using same code but with different
  configuration ?
- First method is "terraform.tfvars" and what does this do ?
- How do you control different environments in tfvars method ? Using "startswith" function ?
- We create different buckets and dynamodb tables for Dev & Prod in tfvars method.
- And also we create different folders for Dev & Prod in VS.
- Can we use 1 bucket for both Dev and Prod in tfvars method ? YES!
- So create 2 Buckets & 2 Dynamodb tables in aws console in tfvars method ?
- You need to initialize Dev backend while "terraform init" and same for Prod also.
- When you are switching from one env to another env, you must reinitialize it.
- Then you can terraform plan, apply (or) destroy using -var-file
- What will happen when you forgot to give -var-file ? It will load default variables.tf
- What will happen when you comment variables.tf file ? It will ask the user to prompt inputs.
- So that you will come to know i forgot to give -var-file.
- Only 1 bucket is created for workspace, inside that it will automatically create a default folder
  "env:/" and inside this env folder, terraform will automatically create Dev/Prod workspaces.
- If you want to know workspace commands just "terraform workspace"
- How to create workspace ? "terraform workspace new dev" do it in gitbash.
- When you are using terraform it has default variable that is "terraform.workspace"
- So we use "lookup" function in workspace method to control different environments.
- What will lookup function do is the below ?
- lookup(map, key) ---> Giving input as map and passing the key below is the example.
- lookup(var.instance_type, terraform.workspace) ---> 1st one is map and another is key.
- So which approach is better ? tfvars, workspace, different repos for different envs ?
- Provisioners are used to execute the commands on a local machine (or) remote server after it's created,
  typically used for initial configuration like boot strapping.
- Provisioners are used only for instances (or) EC2.
- What is local-exec provisioner in terraform & what is the syntax ? It enables a keyword ${self.id}
- Local-exec --> Run on your local machine --> Use case is to notify, trigger local scripts etc --> No
  remote access is need.
- What is remote-exec provisioner in terraform & what is the syntax ?
- Remote-exec --> Runs on your remote server --> Use case is to install softwares, configure
  ec2 post setup --> Need SSH/WinRM to access remote host.
- What is the disadvantage of local-exec ? local-exec provisioner runs only one time not every time.
- Provisioners are useful to integrate terraform with configuration management tools like ansible
  to get end to end automation.
- We can write multiple provisioners also like for example "on_failure = continue" nothing but same
  as ignore errors in ansible.
- What is difference between Terraform and Ansible ?
- We can also create ec2 instances using ansbile but it does not have state file as terraform does,
  that is why terraform is perfect for creation of infrastructure only.
- What is Creation time and Destroy time in terraform ?
  
### Session-29
- What is Module Development in terraform and what is the syntax ? Go through the code of EC2 module in
  "Terraform-modules" in VS. Here provider.tf will not be there in module developing.
- How many types of Modules and How many types of Roles are there ?
- It is DevOps engineer responsibility to write README.md file to let others know how to use module.
- Develop yourself a terraform EC2 module and use it ?
- Create a VPC in aws console ? CIDR ---> 10.0.0.0/16
- Internet has given some "PrivateIP address ranges" those only allocated to PrivateIP not for PublicIP,
  there you can see 24,20,16 bit-blocks
- Even ISP people will configure your PrivateIP address in any range among these 3 bit-blocks only.
- We can select any range, but siva selected as 10.0.0.0/16 range.
- Atleast you need to create 16 servers to use VPC, 10.0.0.0/28 ---> 16 servers, 10.0.0.0/16 ---> 65k
  servers, generally we give VPC_CIDR 10.0.0.0/16 only, because it does not cost anything, so we can
  go for maximum.
- Create Public subnet in aws console ? CIDR ---> 10.0.1.0/24
- Create Private subnet in aws console ? CIDR ---> 10.0.2.0/24
- Create Database subnet in aws console ? CIDR ---> 10.0.3.0/24
- Create Public, Private & Database route tables in aws console ?
- And associate Public, Private & Database route tables ?
- Give internet access to the Public subnets.
- Enable Auto-asign public IPv4 address only to the Public subnet.
- Create Internet Gateway and attach to your created VPC in aws console ?
- What is the difference between Public subnet and Private subnet ?
- What is CIDR (Classless Inter-Domain Routing) ?
- Use always terraform best practices for naming convention.
- We used Open source modules sometimes, we have dedicated cloud team who develops module and we use them.
- How do you check internet is working or not ? "ping google.com" Ipv4 is 32bit and Ipv6 is 64 bit
- Router (Internet Gateway) ---> It has Public_IP & Private_IP. PublicIP is nothing but just type what
  is my ip in google, there you can see Ipv4 address that is your PublicIP, not ipv6. What is your PrivateIP
  just "ipconfig" in cmd there you can see IPv4 address under Under wireless LAN adapter Wifi.
- What is your actual IPaddress ? Just type in google "what is my IP", if anybody wants to connect to my
  laptop you can connect using this IP address only. You cannot connect with PrivateIP address.
- Your created VPC is Isolated, even aws dont have access to it.
- AWS wont charge for VPC's, subnets, route tables, it only charges when you are creating server.
- We can create as many private subnets we want, however for functionality purpose we have only two subnets
  which is Public and Private subnets.
- Watch from 26:11 to 1:14:21 to understand how VPC works.

### Session-30
- What resources we have created inside the VPC from aws console ?
- We have created VPC in aws (Your created VPC is Isolated, even aws dont have access to it)
- It is like your Private Data-Center in aws cloud.
- Created Internet Gateway (IGW) and attached to the VPC.
- Created Public, Private & Database subnets in atleast 2-AZ's for High Availability
- Created Route tables (Public, Private & Database) and associated it with their respective subnets in two
  regions 1a and 1b.
- Added Internet Gateway route in Public Route table, because internet should be enabled in Public not in
  Private, that is the difference between Public and Private subnets.
- Enabled Auto-asign Public IPv4 address only to the Public subnet not to the Private subnet.
- When you create a VPC, a default route table, also known as the main route table, is automatically created
  for that VPC. This main route table is initially associated with all subnets within the VPC that have not
  been explicitly associated with a custom route table. It contains a local route that enables communication
  within the VPC. While this default route table cannot be deleted, its routes can be modified, and custom
  route tables can be created and associated with specific subnets to provide more granular control over
  network traffic.
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
  instance, this instance IP is dynamic, whenever you off and on.
- So create ElasticIP for this instance first and then create NAT Gateway.
- NAT and ElasticIP is chargeable, so delete after practice.
- Can we get StaticIP for this instance ? yes we can get but it is very costly thing.
- Even your home PublicIP is Dynamic. If you want StaticIP, you need to pay money to ISP provider.
- What is VPC peering ? and what is the condition to create VPC peering connection ?
- Create a VPC peering connection between "Roboshop_VPC & Default_VPC"
- So let us take "Requestor VPC = Roboshop VPC ; Acceptor VPC = Default VPC".
- Accept request in the same account and then add routes in VPC.
- Try to add routes in main route table, because it is the default route table which is created automatically   created after vpc is created to communicate between subnets, if not reflecting, then add explicitly ?
- If you want only one (or) two Private subnets wants to connect to the vpc peering main road then you can
  add in those two route tables only.
- You need to add from the other side also not just one side. This is nothing but routes in VPC.
- Go through the "Terraform-aws-vpc-module" how we developed vpc and resources inside it.
- We have a Tagging strategy because we have more resources, so we use better tagging strategy.
- We have Common_tags and Resource_tags ? what is the difference between them ?
- We used "merg" function in tagging strategy to merge Common_tags and Resource_tags.
- You can also create s3 bucket for vpc module.

### Session-31
- Go through the code of "Terraform-aws-vpc-module" in VS.
- While developing VPC module, we come across Peering section, is really Peering connection is required ?
  Peering may not require for everyone, when this Peering is useful ?
- Bydefault Peering connection between two VPC's is not possible.
- If we want to connect with the resources which are in another VPC, then you require peering.
- How to connect to other VPC which is in another company ? Install VPN in Default_VPC & Connect.
- Example consider Requestor is "Roboshop" and Acceptor is "User" provided VPC or Default VPC.
- In VPC peering, when you are adding routes in VPC, if acceptor vpc is not in our control what you
  will do ? We should inform them to add the acceptor route in their terraform code.
- Big companies depends on multiple companies to deal different modules.
- So users can decide if peering is required or not ? if required they have to give VPC peering_id,
  if they are not giving, we should consider default_VPC. Go through the peering.tf file
- Overall developing your vpc module is completed and you pushed it to the internet (Github), then
  how to refer this ? "source = "git"::<https_URL>ref=main"
- So when you do "terraform init" the module will be downloaded in where we are testing the code and it
  will automatically create a folder called "module"
- Till now we used "Allow-all" method while creating SG, but now we use strict rules.
- How to use Security Groups effectively according to the roboshop documentation ?
- We install vpn in Default_VPC to connect Private instances which are Present in Roboshop_VPC.
- We can create a folder (Example) and keep all the testing code in it, so that it will be easy for
  everyone to use the module.
- We keep all our resources in 1a zone.
- In vpc module developing, we need to publish outputs then only users can get the information.
- We have a Database subnet groups, because Databases have different behaviour, nothing but just adding
  database subnet ids.
- We also have Open-source modules for vpc also, if you search in google you can use that also, instead
  of developing vpc module, but for practice you need to know.

### Session-32
- Till now we used "Allow-all" method while creating SG, it is just for practice only, but now we need to
  follow strict SG rules according to the Roboshop-Documentation only.
- We have developed our own customized module for creating VPC right ? In this session also we are going
  to develop our own customized SG module, so refer "Roboshop-aws-SGmodule" in VS
- We have created Security groups and Security group rules for all the components according to the Roboshop
  Documentation, so go through the code in "02-sg" in "Roboshop-terraform" folder.
- Why we created different folders for every resources in "Roboshop-terraform" ? Refresh time
- Since they are in separate folders, consider they are like different projects.
- Go through the folders 01-vpc, 02-sg, 03-vpn, 04-ec2 code in "Roboshop-terraform" folder in VS.
- What is the main input required to create a SG ? VPC_ID
- For example in Big companies, 1 team is taking care for VPC, another team is taking care for SG etc.
  How do you get the information of resource which is in another team or another project ? SSM Parameter
- What is SSM Parameter store in "AWS systems manager" ? Its like a configuration storage.
- What does Configuration storage (or) Central storage do ?
- What is the Naming convention while storing the Configuration (or) Key-Value pair in SSM ?
- Generally Naming format will be in the linux structure like "/roboshop/dev/vpc_id"
- As we know Data-sources is used to query the data dynamically from the providers and also from the existing
  resources right ? but to query from the existing resource, we need to give some input like vpc_id, this
  vpc_id we cannot get from the data source, but we used data source only to query the default vpc_id, but to
  take the created vpc_id, again data-source is not an option, because we need to give vpc_id as input.
- Since VPC is in different folder, how do we get vpc_id in SG ? You need to store vpc_id in SSM Parameter
  store and read that saved Key-Value in SG using data-source option.
- Go through the "Terraform-aws-SGmodule" in VS, just module developing.
- Generally it is not mandatory to create ingress rules while creating SG and why ? but egress is static
  because this traffic creating from our server, mostly it will be constant.
- In real time, whenever you want few ports to open, you need to write a mail to firewall team then, they
  will open the port, if they are using terraform they will do changes in main.tf file
- In Security groups, we have two names "Name" and "Security group name" what is the difference ?
- As a module developer, you must output the resources in output.tf file like IDs etc. So that other teams
  will refer.
- Now create all Security groups according to the Roboshop Documentation "02-sg" in VS.
- For example according to the Roboshop Documentation, Mongodb ---> Should accept connections from
  "Catalogue" and "User" what should be the ingress (Security group rule) of mongodb now ? Source should
  be the CatalogueIP & Port 27017, Similarly for User also ? 
- Is CatalogueIP is constant everytime ? NO! then what should we do ? We need to take the ElasticIP which
  is very costly, because we have 12 Private servers that means we need to create 12 EIPs. If it is a Big
  project, we may need to create thousands of EIPs, this will generate huge bill to the company.
- So Security group has given one option, first create Mongodb and Catalogue Security groups.
- Then go to the Security groups in aws console and select created mongodb_SG/Edit_inbound_rules/Add rule
  Type --> Custom TCP, Port: 27017 and in source just type "sg" next to the custom, you will get the created
  Security groups, in that select already created Catalogue_SG. Same for the User also.
- Now write a terraform code for all the Security groups according to the Roboshop Documentation.
- Now creating EC2's for the roboshop "04-ec2" in VS using Open-source module from the internet.
- Here the only disadvantage is you cannot connect to this Private instances using SSH, because Private
  instances dont have PublicIP. We have two options and what are there ? "Jump_host" & "Installing VPN"
  in Default_VPC to connect to Private instances which are in Roboshop_VPC, but make sure you have Peering
  connection between Default_VPC and Roboshop_VPC.
- We used "CISCO" VPN in our company which is costly, but for practice we used "OpenVpn Connect"

### Session-33
- How to connect to Private Instances using VPN ?
- In which vpc should we install open-vpn ? default_vpc
- We must have a peering connection between default_vpc and roboshop_vpc.
- We have to create all our private instances in roboshop_vpc only.
- How the traffic is routing from home sever to aws network using open-vpn ?
- What is the SG rule when mongodb is accepting connections from open-vpn ?
- Make sure to enable vpn in all private instances and how can you do that ?
- Enabling vpn in all private servers is nothing but giving SG of VPN_instance to the mongodb.
- How to install open-vpn in server and connect to it ?
- How do you write whole process using terraform code ? 03-vpn in VS.
- Configuring VPN is not our responsibility, we have separate team for this.
- We use cisco_vpn in our company.

### Session-34
- Create resources in terraform like 
