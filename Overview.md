### Terraform
************************************************************************************************************
- What is terraform ? and what are the advantages of terraform ? V,C,A,I,C,A,M,H
- In how many ways we configured our project ?
- Why we prefer ansible over shellscript while configuring ?
- Why we dint preferred configuring project manually ?
- What is inventory management ?
- What is declarative ? and do we need to follow the sequence ?
- Terraform installation and setup ?
- How to push the terraform code from VS to aws ?
- How to configure aws ? aws configure
- How to create terraform user or administrator user in aws ?
- Where does the access key and secret keys will be stored ?
- Terraform syntax ?
- Keeping provider is important in terraform ?
- Create sample ec2 with SG using variables ?
- What are terraform commands and explain their functionality ?
- Where to run the terraform commands ?
- Variable syntax ? Do we really need to put "data type" in variables ?
- We can also keep access key and secret key in provider under region, but why we dont
  prefer to keep ?
- Do we need to push to the github before running terraform commands ?
- Importance of .gitignore in terraform ?
- What does terraform.tfvars file do ? we generally it as .tfvars, we can name anything
  before .tfvars
- What are the variable preferences ? command line/-var-file/terraform.tfvars/environment variable
- Write a sample condition syntax for an ec2 ?
- Create ec2 and route 53 records of few instances using count_based loop ?
- Create ec2 and route 53 records of few instances using for_each loop and also use output block ?
- What is the use of output block ?
- What is length function ? why it is used only in count based loop ?
- Syntax of output ?
- What are locals in terraform ? and what is the syntax of local ? how to use locals ?
- What is Data-sources ? Does data-sources is only used for querying the data dynamically from
  the providers ?
- What is the use of querying the data dynamically from the existing resources ?
- Types of loops ? count_based/for_each/dynamic_loop why this are useful ?
- Terraform state (state and remote state) ?
- What is terraform.tfstate (it is crucial should not be deleted by mistake also) and what
  is lock file ?
- Why central state file (remote state s3) is used ?
- What are the disadvantages in local state ?
- Create one s3 bucket and lock the s3 bucket using dynamodb table ?
- What are there otherthan "Terraform S3 remote state" ?
- Does S3 buckets are chargable in aws ?
- How to create multiple environments in 3 ways and what are they ? same code but with different
  configurations.
- First create using "terraform.tfvars" method.
- Do we need to create different buckets and dynamodb_tables for dev and prod ? or same bucket ?
- What function you have used to control different environments in tfvars method ?
- When you are switching from one env to another env, you need to reconfigure the backend.
- "terraform init -reconfigure -backend-config=prod/backend.tf"
- When you do terraform init ---> Backend will also be there, so here you have multiple environments,
  so use "terraform init -backend-config=dev/backend.tf"
- Now create using "workspace" method and there will be only one bucket default one "env:/"
- How to know workspace commands ?
- How to create new workspace ?
- Workspace has a default variable "terraform.workspace" what does it do ?
- What is "lookup" function ? we need to write in "instance_type" line like "lookup(var.instance_type,
  terraform.workspace)"
- Which approach is better ? tvfars (or) workspace (or) different repos for different envs ?
- How many types of provisioners are there ? and what are they ?
- What is local-exec provisioner and what is the syntax ?
- What is the use of key word ${self.id} in the local-exec provisioner block ?
- What is remote-exec provisioner and what is the syntax ?
- Where this provisioners are useful ?
- What is the difference between terraform and ansible ? how end to end automation will be done
  using ansible ? and why not creation of infra done with ansible ? and why only we use terraform
  to create infra ?
- What is creation time and destroy time ? and why we use this ?
- Using different key names for backend for different environments
- We can write multiple provisioners like "on_failure = continue"
- What is the use of Module development in terraform ? and what is the syntax of the module ?
- What are two types of modules and two types of roles ?
- Which type of modules you have used in your company ?
- What is VPC in aws ?
- What is the difference between public subnets and private subnets ?
- What is CIDR (Classless Inter-Domain Routing) ?
- Create roboshop VPC network in aws console in privateip range only which internet provides only
  3 bitblock ranges, we should select among them only.
- Even ISP providers will configure our home privateip in this range only.
- Generally we give "10.0.0.0/16" so that we can get maximum IPs like 65k, it will not cost.
- Create public and private and database subnets ranging 10.0.1.0/24 ; 10.0.2.0/24 ; 10.0.3.0/24
  in atleast 2-AZ for High Availability.
- Create Public and Private route_tables in this VPC only
- Now associate route_tables to the respective subnets.
- Give internet access to the public_subnets, not to the private
- Enable auto-asign public Ipv4 address to public subnet, not to the private
- Create Internet gateway (router) and attach to the roboshop VPC
- How do you check if internet is working or not ?
- Router (Internet Gateway) has two sides PublicIP and PrivateIP, how do you check this ?
- If anybody wants to connect to my laptop or hack, how they will connect ? using publicip or privateip ?
- We can create as many private subnets we want, but for functionality purpose we have only two those
  are public and private subnets.
- Explain the the NAT Gateway in VPC ? in which subnet should we create this ? and why ?
- Adding NAT Gateway is enough ? or should we add routes (connection) from private subnets
  to the NAT Gateway ?
- An Instance will be created in the background when you create NAT Gateway, we dont have access
  to that instance and moreover that instance IP is dynamic, if you want staticIP that is more costly,
  so create an elasticIP first and then create NAT Gateway, even our home publicIP is dynamic, if
  we want staticIP we need to pay money to the ISP provider.
- Note that ElasticIP and NAT Gateway is chargable and why ? because NAT is creating an instance in
  the background, creation of server is chargeable.
- Create VPC peering between "default_VPC and roboshop_VPC" and also "routes in VPC"
- A default route_table will be created in aws, if you can add VPC routes in default it is best,
  or which ever subnet wants route then we can add explicitly, make sure you need to add both sides.
- Go through the VPC-Module development in VS.
- Now create all the above using terraform code
- We have a tagging strategy in terraform those are common_tags and resource_tags and their syntax ?
- What will hapenn if we merge common_tags and resource_tags ?
- Is really peering connection is required ?
- How do we connect to VPC (resources) which is in another company ? installing VPN in default VPC.
- If acceptor VPC is not in our control, can we get the access to add route ?
- We can use module which is in github "source = "git"::<https_URL>ref=main"
- How to use Security groups effectively ? according to the roboshop documentation ?
- How the naming convention is followed in your company ? ${project_name}.${component}.${resource}
- For downloading the artifacts we followed "semantic" version
- For how many resources you have developed "modules"
- How to connect to the private instances ? you need to install VPN in default VPC.
- We only developed modules for VPC and SG, and later we used open source from the internet github
  for creation of ec2 instances.
- Why slice function is used ? write a code to list availability zones which are available ?
- We can write a condition in variables also using validation block with in the variable syntax using
  length function, we wrote for public, private & database subents.
- Develop ec2 module and how to use that ec2 module ?
- Develop SG module and how to use that SG module ?
- Best practices to create security groups using roboshop documentation.
- You have developed modules for VPC, SG, EC2 right ? what are those types ?
- Why we created separate folders in VS for every resources ?
- What is the main input required to create a SG ? nothing but VPC
- When you are creating SG, we want VPC right ? how to get vpc_id which is another folder,
  that means treats as a complete different project ? Example of a big company who dont depend on
  just one company ?
- What is the use of SSM Parameters in "aws systems manager" and it is key-value pair, it is like a
  central storage for configuration and what is the path type to store a key-value ?
- For example how to store a vpc_id in SSM Parameter in aws console ?
- How to create a SG module ? Go through "Roboshop-aws-SGmodule" in VS.
- Now create all SG's for roboshop, refer in 02-sg.tf
- For example mongodb should accept connections only from catalogue and user, then what is the source
  for mongodb ? catalogue and user IP's
- Is catalogue and user IP's are static ? NO! then what should we do ?
- Now creating all EC2 servers for roboshop, but this time, we are using open-source module
- But we cannot connect to private servers, since they dont have PublicIP right ? then we have two
  options anad what are they ?
- Data-sources is only to query the data dynamically from the providers ?
- When you see sg in aws console, there you will see two names for a sg, what is the use ?
- In real time, when you want to open a port, you need send a mail to the firewall team, and we
  used cisco vpn in our company.
- How to connect to private server using VPN ?
- You need to install VPN in default_VPC, and make sure to have peering connection between default_VPC
  and roboshop_VPC
- Make sure to enable VPN in all private servers, how ?
- How to install OpenVPN in ec2 server ?
- Now go through the 02-sg.tf, which we have created all those using terraform code
- Configuring VPN is not our responsibility, we have separate team for this
- We have created VPC and Peering connection between Default_VPC & Roboshop_VPC, all SG's, VPN, EC2
  and Records, so how do we configure all those instances automatically by integrating ansible ?
- What is LB (Target_groups & rules) and Launch templates (Auto-scaling & auto-scaling policy)
- Any project starts with vpc, go through the "Roboshop-Infra-Dev" this is Dev environment, how did
  you create this workspace ? using which method ? terraform.tfvars, workspaces or different repos
  for different environments ? and do we need to create separate bucket ?
- Load balancer is running on which protocol ? HTTPS, why we keep "Web_ALB" in HTTPS ?
  and why we keep "App_ALB" in HTTP ?
- Which is more secure HTTPS or HTTP ?
- Listeners of HTTP(80) and HTTPS(443)
- Why we create sg.yaml file in "Roboshop-Infra-Dev" ?
- For creating databases, we implemented ansible PULL strategy and why ?
- What is the disadvantage in PUSH approach compared to PULL ?
- We dont know the status of user-date wether it is success or not, so we use Provisioners
- Passwords are stored in ssm only through manuall not automated, mainly database passwords
- Why we are moved from ansible vault to SSM parameter ?

### Git (Global Information Tracker)
************************************************************************************************************
- How git will track files like for example "git echo hello world" ?
- How to generate a commit-id for your content in git ?
- Git will calculate commit-id based on the content
- What is SHA code ? for every file (or) folder (or) repo storing in github will have SHA code.
- What is "git log" ? to see the commit-ids
- What is the command to print all commid-ids in oneline ? git log --oneline
- Git is a Key-Value pair ? here what is Key and Value ?
- What is the command used to get the information of the commit-id ?
- What is protection rule in github for main (or) master branch ?
- What are the minimum protection rules we can give to the main branch among the different rules ?
- Command to create a new feature branch in github ? when you create this branch, do you think commit-ids
  of main branch and feature branch will be same ? when you cloned from the main branch
- When will the commit-id of feature branch will change ?
- What is PULL request ? when they should raise this PR ?
- Who are the reviewers (or) approvers ? what they do ? how many minimum reviewers should be there ?
- When developer got the approvals, what are the merging options (or) strategies they have ?
- After merging also you will get merge commit-id, that means main branch is forwarded 
- When you "git log" and "git cat-file <merge_commit_id> -p" then you will get few information like tree,
  parent-ids, author etc.
- What are Merge commit, Rebase and merge, Squash and merge ?
- Which one should prefer among these merging strategies ?
- When to use Merge and when to use Rebase ?
- What is Long-live branch and Short-live branch ? we can delete Short-live branch after merging
- Where the CICD should takeplace in this branching strategy ? in Dev in Feature branch only and why ?
- Code is same across all environments, but configuration is different.
- Configuration should be dettached from the code, since we are storing config in SSM Parameter.
- Once we got succeeded in merging code into the main branch, we can deploy into higher environments
  like QA, SIT, UAT, and PROD
- What if we success in DEV and failed in QA ?
- We are following feature branching strategy, we have main branch as long live branch, anything otherthan
  main branch we call it as feature branch, developers will work in feature branches, they will do CICD in
  feature branch itself, once it is successful they will raise PR, based on the discussions PR will be
  approved and from the main branch, we do deployment into the higher environments QA, SIT, UAT, PROD.
- If we got emergency, we can just test in "DEV" and then directly go for the "PROD"
- You will have ".git" folder in every repo, it stores all the information of git like tracking, metadata,
  objects etc. Everything will be stored in this folder only.





































