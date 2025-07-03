### Best practices to create security groups in roboshop
- Till now we used allow-all method while creating SG, it is just for practice only, but now we need to follow
  strict SG rules according to the roboshop-documentation.
- In last session we created VPC using our own module (customised module) in this session, we are going to
  create security group module using own module (customised module) and also create all security groups for
  all components according to the roboshop-documentation.
- We created a folder "Roboshop-terraform" in |VS| and inside this folder we have created separate folders 
  for every resources to reduce the refresh time because if our infrastructure becomes big, refreshing the 
  resources will take some time, so to reduce the refresh time we have created in separate folders. In simple
  words like if we keep all resources in a single folder, incase if we do any small change also, it will take
  time to reflect all the resources and maintenance will also very tough.
- So go through the 01-vpc, 02-sg, 03-vpn, 04-ec2 code in |VS|.
- What is the main input required to create a SG ? We want VPC_ID, in which vpc you are creating SG, here vpc
  and sg are in different folders, if it was in same folder we can easily get the vpc_id, but these are in
  different folders, For example if they are in separate folders then they are completely like different
  projects, for example like in big companies there will be a separate team for vpc, and for SG like that. How
  do you get vpc_id by going out from the SG folder, for that we have a service called "SSM Parameter" in "AWS
  systems manager" in this we need to create a key-value pair, and we can refer in the security group to get
  the vpc_id. SSM Parameter is like configuration storage, different applications can store the configuration
  in SSM Parameter and also different application can refer the stored configuration from the SSM Parameter.
  It is like central storage for the configuration.
- So first store the vpc_id in ssm parameter store in "parameter.tf" file in 01-vpc then write a code. Search
  in google "ssm parameter store in terraform"

### Creating SG Module
- Refer "Roboshop-aws-SGmodule" in VS.
- In this we created SG, but not inbound rules, so create rules using dynamic at the time of SG creation. Is it
  mandatory to write ingress rules to create SG ? NO, it is not mandatory to provide ingress or egress, but
  egress is important, generally egress rule will be same because traffic is creating from our server. What we
  do here is egress is always same for every SG, so keep egress static, so we want only ingress.

### Now create security groups for the roboshop 02-sg in VS
- Go through the roboshop documentation https://github.com/daws-76s/roboshop-documentation
- So what should be the ingress rule for mongodb ? mongodb should accept connections only from catalogue and
  user, then source ---> catalogue_IP and port ---> 27017, here catalogue_ip is constant every time ? NO, so
  to get the catalogue static_ip what is the option we have ? we need to take elastic_ip which is costly, if
  we take elastic_ip for every private modules we need 12 elastic_IPs which is very costly. If it is a big
  project we may need 1000's of elastic_IPs, then company may get bill of 5000 dollars. So better to give the
  security group_ids.
- Create a mongodb_SG and catalogue_SG in VS (main.tf)
- Then go to the security groups in aws console and select created mongodb_SG/Edit inbound rules/Add rule
  Type --> custom TCP, port: 27017, and in source just type "sg" next to the custom, you will get the created
  security groups, in that select already created catalogue_SG.
- So write a terraform code for the above line in VS.
- Similarly create for user also, and continue for redis,mysql,rabbitmq (refer documentation), here better
  to create all security groups for all instances first and then write rules.

### Now creating Ec2's for the roboshop 04-ec2 in VS
Till now we developed VPC and SG module and simultaneously we tested this modules while creating vpc and sg.
But here we are using modules directly from the internet developed by others to create ec2's. Nothing but from open-source. Here the only disadvantage is you cannot connect to this private instances using ssh, because private instances dont have public_IP addresses. For this we have below two options.
- Create one ec2 in public_subnet, and login to this ec2 first and from there connect to the mongodb. We call
  this as a "jump_host"
- Another one is using VPN, install it in your laptop and connect to the mongodb using VPN.

### Points to remember
- Data sources is used to query the data dynamically from the providers and from the existing resource also
  but to query from the existing resource, we need to give some input like vpc_id, this vpc_id we cant get 
  from the data source, but we used data source only to query the default vpc_id.
- Generally the path in ssm parameter should be like this "/roboshop/dev/vpc_id", Because there will many
  env's right, so to identify easily we use this linux structure. It is like key-value, here key is path and
  value is vpc_id.
- In security groups in aws console, we have two names 1.Name and 2.Security group name, we can change 1st one,
  not 2nd one, if you change the 2nd one then terraform will delete that SG and recreate new SG which you have
  updated (nothing but after terraform apply)
- In real time, whenever you want few ports to open, you need to write a mail to firewall team then they will
  open the port, if they are using terraform they will do changes in main.tf
- We used "cisco" VPN in our company.
