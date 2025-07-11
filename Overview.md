### Terraform
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
- What is terraform.tfstate (it is crucial should not be deleted by mistake also) and what is lock file ?
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




- Provisioners are of two types "local-exec" and "remote-exec"
- What is local-exec provisioner and what is the syntax ?
- What is the use of key word ${self.id} in the local-exec provisioner block ?
- What is remote-exec provisioner and what is the syntax ?
- 













































