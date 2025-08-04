### Session-25
- What is terraform and why it is used ? and In how many ways we configured our project ?
- Why we prefer ansible while configuring big project ?
- Another name of ansible ?
- Why we din't prefer manual configuration ?
- What are the advantages of terraform ? V,C,A,I,C,A,M,H
- What is declarative in terraform ?
- How to install terraform and setup ?
- Install "hashicorp terraform extension" to get colors.
- How to get authentication to AWS to push the created infra ? aws CLI install
- How to test wether the aws CLI is installed or not in cmd & gitbash ? aws --version
- If credentials are not found then use "aws configure"
- Before "aws configure" you need to create terraform administrator user in IAM ?
- Where the credentials like secret key and access key will be saved ?
- What is the syntax of terrafrom to create any resources ?
- What we call this syntax of terraform ?
- What is the importance of provider in terraform & what is the extension of terrafrom to save ?
- Where to run the terraform commands ?
- What are the terraform commands and what is their functionality ?
- Terraform commands should be run in gitbash.
- What is variable syntax ?
- Is really data-type in variable syntax is important ?
- Go through this https://github.com/daws-76s/terraform
- We can also get authentication to AWS in provider section, under region.
- By giving access_key and secret_keys under region also, but why we dint prefer this ?
- Why we only use aws CLI to authenticate ?
- So Dont push the access_key and secret_key to the github (or) internet for safety reasons.
- Go through the all files in Terraform folder in VS.

### Session-26
- What is the importance of .gitignore in terraform ?
- What is the use of terraform.tfvars ?
- How to give terraform.tfvars file from the command prompt ? for plan and apply
- Here terraform.tfvars name is not mandatory we can use any name like "saikiran.tfvars"
- Write a terraform code using terraform.tfvars example ?
- What are the variable preferences in terraform ?
- Write a terraform code, if mongodb then t3.small and remaining t2.micro using condition ?
- Create instances and route53 records using count_based loop ?
- Create instances and route53 records using for_each loop ?
- Count_based is to iterate lists and For_each is to iterate maps.
- What is function in terraform and what is length function here ?
- We cannot create our own functions, we have to use terraform inbuilt functions only.
- What is the syntax of output in terraform ?
- Go through the output block in VS ? and why the output block is used ?

### Session-27 
- What is locals in terraform and what is the syntax of locals ?
- How to call a local in terraform code ?
- What is Data-sources in terrafrom and why it is used ?
- How do we search ? for example if you want AMI, then "terraform query ami" in google
- Can we query data from the existing resources also ? apart from the providers ?
- Types of loops ? count_based, for_each, dynamic_loop
- What is dynamic_loop and where it is useful ?
- What is Terraform State (State and Remote state) ?
- What is Declarative state and Desired state ?
- What is Current state in terraform ? and where it will be stored ? terraform.tfstate
- When Desired state == Current state, then terraform will not take any action.
- When Desired state =//= Current state, then terraform will create.
- Why the terraform will create lock file ?
- What is Remote state and explain the concept using 2 developers are working on same repo ?
- What errors these developers will face, if they are working on same repo ?
- Terraform.tfstate is a crucial file, should not delete.
- What are the two disadvantages in local state ?
- So create s3 bucket and lock that bucket using dynamodb table ?
- What are the different remote states we have ? and why we use only "terraform s3 remote state"
- Where to keep this remote state in terraform code ?
- Another name of remote state is backend.
- If we write more lines of script we say configuration is increasing.
- S3 buckets are chargeable in aws, so delete after practice.

### Session-28
- How to create multiple environments with terraform in 3 ways ?
- Using same code but with different configuration ?
- How do you control different environments in tfvars method ? using startswith function ?
- We create different buckets and dynamodb tables for dev & prod in tfvars method
- Can we use one bucket for both dev and prod in tfvars method ?
- Create 2 buckets & 2 dynamodb tables in aws console in tfvars method ?
- You need to initiate dev backend while "terraform init" and same for prod also.
- When you are switching from one env to another env, must reinitialize it.
- Then you can terraform plan, apply (or) destroy using -var-file
- What will happen when you forget to give -var-file ?
- Only 1 bucket is created for workspace, inside that, it will organize into different folders.
- If you want to know workspace commands just "terraform workspace"
- How to create workspace ? "terraform workspace new dev" do it in gitbash
- When you are using terraform it has default variable that is "terraform.workspace"
- So we use lookup function in workspace method to control different environments.
- So which approach is better ? tfvars, workspace, different repos for different envs ?
- What are provisioners in terraform ?
- What is local-exec provisioner in terraform ?
- What is remote-exec provisioner in terraform ?
- 

### Session-29
- What is module development in terraform ?
- What is module syntax ?
- Go through the EC2 module in "Terraform-modules" in VS.
- Provider will be not there in module developing.
- How many types of Modules are there ?
- How many types of Roles are there ?
- DevOps engineer writes a README.md file to let others know how to use the module.
- Develop yourself a terraform EC2 module and use it ?
- Create a VPC in aws console ? CIDR ---> 10.0.0.0/16
- Create Public subnet in aws console ? CIDR ---> 10.0.1.0/24
- Create Private subnet in aws console ? CIDR ---> 10.0.2.0/24
- Create Database subnet in aws console ? CIDR ---> 10.0.3.0/24
- Create Public, Private & Database route tables in aws console ?
- And associate Public, Private & Database route tables ?
- Add Internet in the Public route table ?
- Enable auto-asign public IPv4 address only to the public subnet.
- Create Internet gateway and attach to your created VPC in aws console ?
- Watch from 26:11 to 1:14:21 to understand how VPC works.

### Session-30
- What is NAT Gateway and why it is used ?
- In which subnet (1a or 1b) this NAT Gateway should be create and why ?
- Creating NAT Gateway is not enough we need to add routes between private subnets and to
  Internet gateway (NAT) which is in public subnet.
- Which ever private subnets like database subnet or any other private subnets wants to connect
  to internet, they should add route to the NAT gateway which is in public subnet.
- Select any of the private_subnet/routes/edit_routes/add_route (Destination= 0.0.0.0/0,
  Target= NAT gateway, select default one in dropdown under Target section only)
- When you create a NAT gateway, aws will create instance in the background, We dont have
  access to that instance, this instance IP is dynamic, whenever you off and on.
- So create ElasticIP for this instance and then create NAT Gateway.
- NAT and ElasticIP is chargeable, so delete after practice.
- Can we get StaticIP for this instance ?
- Even your home publicIP is dynamic, if you want staticIP, you need to pay money to ISP provider.
- What is VPC peering ? and what is the condition to create VPC peering connection ?
- Create a VPC peering connection between "Roboshop_VPC & Default_VPC"
- Try to add routes in main route table, if not reflecting, then add explicitly ?
- If you want only one or two private subnets wants to connect to the vpc peering main road
  then you can add in those two route tables only.
- You need to add from the other side also not just one side. This is nothing but routes in VPC.
- Develop aws-vpc Module and test it ? or go through the code in VS.
- What is tagging strategy and why we use it ?
- We have Common_tags and Resource_tags ? what is the difference between them ?
- Why we use merg function in tagging strategy ?
- Now create all resources using terraform like vpc, igw, subnets, route tables etc. 
- Go through the code of "Terraform-aws-vpc-module" in VS.

### Session-31
- In VPC peering, when you are adding routes in VPC, if acceptor vpc is not in our control what you
  will do ?  we should inform them to add the acceptor route in their terraform code.
- Is really Peering connection is required ?
- So how do we connect to other VPC which is in other company ?
- We install VPN in default VPC and then connect.

### Session-32
- 
