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
- We can also get authentication to AWS in provider section, under region
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
- Create instances and route53 records using count based loop ?
- Create instances and route53 records using for each loop ?
- Count_based is to iterate lists and For_each is to iterate maps.
- What is function in terraform and what is length function here ?
- We cannot create our own functions, as to use terraform inbuilt functions only.
- What is syntax of output in terraform ?
- Go through the output block in VS ? and why the output block is used ?

### Session-27 
- What is locals in terrafrom and what is the syntax of locals ?
- How to call a local in terraform code ?
- What is Data-sources in terrafrom and why it is used ?
- How do we search ? for example if you want AMI, then "terraform query ami" in google
- Can we query data from the existing resources also ? apart from the providers ?
- Types of loops ? count, for_each, dynamic_loop
- What is dynamic_loop and where it is useful ?
- What is Terraform State (State and Remote state) ?
- What is lock file in terraform state and why it is created ?
- What is central state file (or) remote state (or) S3 bucket ?
- Terraform.tfstate is a crucial file, should not delete.
- What are the disadvantages if there is not state file in terraform ?
- Create s3 bucket and dynamodb table to lock ?

### Session-28

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

### Session-30
- 
