### Terraform is a popular Infrastructure as code - IaC
Terraform is an open-source tool developed by HashiCorp. Instead of going into AWS console and manually creating an EC2 instance or any other resources, we can create by writing terraform code. Till now we configured our project manually, also using shellscript, ansible, but we prefer ansible as a configuration management if it is large project. Because ansible can connect to more number of servers easily from one single ansible server, we can also call controller machine. Why we din't prefer manual configuration ? Because manually logging in every servers is a timetaking process and also we get more human errors.

### Advantages of terraform
- Version Control
- Consistent Infra
- Automated Infra CRUD
- Inventory Management
- Cost Optimisation
- Automatic Dependency Management
- Modular Infra
- Hybrid Cloud

### Version Control
Since it is code, we can maintain in Git to control version. We can completely maintain the history of infra and collaboration is easy. We can also rollback to the previous version incase of any production failure.

### Consistent Infrastructure
Often we face the problem of different configurations in different environments like DEV, QA, PROD, etc. Using terraform we can create similar infra in multiple environments with more reliability (or) Same code will work in all environments like dev,sit,uat,prod. Real time scenario like code is working in dev or uat 
or pre-prod but not working in prod, to solve this issue we use terraform.

### Automated Infrastructure - CRUD
Basically CRUD over the infrastructure. Using terraform we can create entire infra in minutes reducing the human errors and deleting infra in minutes if not required and updating infra using terraform is also easy. Create the infra, Read the infra, Update the infra, Delete the infra.

### Inventory Management
Inventory Management in Terraform is nothing but tracking and managing the various infrastructure resources that Terraform provisions and maintains. Terraform doesn't have a built-in inventory management system, but it provides several features and practices that help in managing and keeping track of infrastructure resources. If we create infra manually it is very tough to maintain the inventory of resources in different regions. But by seeing terraform you can easily tell the resources you are using in which regions. For example if the project is going big. When you login to aws we can see more resources like multiple VPC, multiple route 53, multiple EC2, multiple load balancers, CDN's, s3 buckets etc. If the client ask for the full details of the project we cannot show one by one in the aws console and giving the report is very tough and that is also not a good practice, instead of showing in the aws console we can maintain from the above points, which can be seen in |VS| in the form of folders of above resources.

### Cost Optimization
- When you need infra you can create in minutes. When you don't need you can delete in minutes, so you can 
  save the cost.
- Automatic Dependency Management, for example if we need to create route53 records, ec2 servers should be in   the running state, and take those IP and paste in the route53, that means route53 is depending on ec2
  servers, so we can create resources and terraform will takecare of dependencies.
- Terraform Modules ---> You can create terraform code as modules, so that other projects can also use it
  without writing from the scratch.
- Terraform is also a Hybrid Cloud that means you can create infra in aws, azure, GCP not only cloud,
  it can also work with any other popular tools available in the market, you can see in the terraform
  providers website, it can work with many other providers (or) you can write your own module and connect
  with the terrform also. Not only resources we can also create repos, branches etc. in github by writing
  terraform code.

The above all are the terraform understanding (Interview Question). It is a declarative way of creating infrastructure, what is declarative ---> whatever you write you get it, if you write correct syntax, and it is easy syntax and no need to follow the sequence in the code. If anybody edit manually in the aws console, and we find it is very difficult to trace who did it, but in terraform if anybody did changes and we can restore infrastructure immediately by just one command, then we can discuss who did it later.

### Terraform installation and setup
- Download terraform from google mostly AMD64 windows and if you extract you will get .exe file
- Move that .exe file in your desired location, downloading is not enough, still it will show terraform
  command not found.
- Take this downloaded path and give it in the "system environment variable"
- Search in the laptop ---> Edit the system environment variables --> environment variables --> select or
  click on the path in the system variables --> edit --> new --> paste it here.
- If you give the terraform command, it will check all the paths you have given in the env variables, if it
  is available then terraform command will work.
- Install "hashicorp terraform extension" to get colors.

We write code in VS ---> then we push to github ---> then we push to the aws, but in order to push to the 
aws we need authentication for that, we have "awsCLI" so search in google "aws cli install" just run shown commands in "cmd" then test "aws --version" in cmd aswel as in gitbash, wether it is installed or not, select windows to install, not linux or macos. Then to connect to aws, we need to create a terraform user or administrator user by going to IAM/Users/Create(next)/Attach policies directly and select administrator access --> click on your created_user/security_credentials/create access_key/click on command line interface (CLI)/copy the access_key and secret_key then -----> configure user in your laptop by using this command "aws configure" in gitbash --> these credentials will be saved in --> windowsC/users/user/.aws folder

### Syntax of terraform to create resources

      resource "what resource" "name of your resource" {
      
      }

- This syntax we call HCL (Hashicorp Configuration Language) 
- Here also we have variables/conditions/loops/functions/datatypes
- So rightnow we are using terraform for aws, so search terraform providers --> Select aws provider, if you
  dont give the provider, terraform will not know to work with which provider ? and .tf is the extension of
  terraform file.
- Just go through session-01/ec2.tf, provider.tf, varibles.tf in the |VS|, where ec2 with SG is created 
  using terraform, Just type "terraform ec2 in the google"
- Where to run the terraform commands ? ---> Where ever .tf files exists, like for example go the directory
  session01/ec2/ec2.tf and provider.tf ---> Here you should run the commands.

### Terraform commands
- terraform init --> Initialize the provider, it will download the provider in ".terraform" folder is
  automatically created when you do terraform init.
- terraform plan --> Terraform will calculate the full details and show it (or) it is just a plan it will not
  create, it will show the preview of the changes (or) Terraform compares the infra between declared and
  existing.
- terraform apply --> Now it will create
- terraform apply -auto-approve --> Not ask for the prompt
- terraform destroy -auto-approve --> Not ask for the prompt
- All the above commands should be run in the gitbash.

### Variables syntax

        variable "name-of-variable" {
             type = datatype
             default = "default value"
        }

Terraform will automatically consider which datatype is, so no need to give the data-type but for practice we need to give data-type.

### Points to remember
- https://registry.terraform.io/providers/hashicorp/aws/3.34.0/docs/resources/security_group
  terraform registry website to see all examples.
- Just go through the "README" file in the sivagithub terraform "https://github.com/daws-76s/terraform"
- In provider also we can give access_key and secret_key under region to authenticate to aws, but when you
  push to github then github will send emails to notify, but it is not recommended because anyone can use
  your aws account and they can create anything in aws. So thats why we downloaded awsCLI to authenticate to
  aws account which is a secure way.
- Important point to remember, you "NO" need to push to the github, you can directly save the terraform file
  and run the terraform commands in gitbash and later you can push to the github to save the files. Later
  green colour will change to the normal colour. But saving the file is mandatory.
- Dont push the access_key and secret_key to the github (or) internet for safety reasons.
