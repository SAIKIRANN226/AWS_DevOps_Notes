### Creating resources in "Robosho-terraform"
- 01-vpc
- 02-sg
- 03-vpn
- 04-ec2
We have created VPC and Peering connection between Default_VPC & Roboshop_VPC, all SG's, VPN, EC2 and Records. So now we want all instances to automatically configured, for that we need to create a "ansible-server" this server will provision all instances using ansible-playbooks and also create security group on port SSH 22 to connect all instances securely, but we already created VPN SG with SSH 22 right ? So we can use that also. So create this ansible-server in default subnet in Default_VPC. So now ansible server is created, after creating server, ansible should provision all the servers automatically, for this we need to write a small shellscript, to provision the instances "ec2-provision.sh" in VS. There is one disadvantage in "user-data" if user-data fails one time, it will not come again, so we will address this issue with provisioners but siva dint explained this, so delete the ansible-server and do again terraform init,plan and apply.

### LB (Target_groups & rules) and Launch templates (Auto-scaling & auto-scaling policy)
Because of these application will become fully stable and auto-scaling will be enabled automatically.
- First create 2 nginx servers, while creating add "user-data" like #!/bin/bash ; yum install nginx -y ;
  mkdir -p /usr/share/nginx/html/ui ; echo "<h1>Hi we are from UI team<h1>" >
  /usr/share/nginx/html/ui/index.html ; systemctl restart nginx
- Create LB security group, here from the tarffic is coming to this LB ? from the internet, therefore ingress
  rule should be type = http ; cidr = 0.0.0.0/0
- Create SG for these two nginx servers, these servers will get request from LB, therefore ingress rule should
  be a SG which is attached to LB.











### Points to remember
- We know how to develop the module and how to use the module
- Mostly in the companies, errors are not because of coding, it is because of configuration change, even if we
  make small changes in configuration, we get errors, so thats why we need to keep config independently.
- SG is very important, since we are connecting to every resources present in aws.
- Individually we can understand every concept, but when we configure the project using all concepts, it will
  create huge confusion, like for example if we give a request from client (or) from our laptop, the request
  should reach to the end service which is present in aws, request will cross many stages like client-side
  configuration should be clear, vpc, igw, subnets etc. have many resources to cross to reach the end service.
  So this visualization should there in us. Thats why SG is important to use in every resources.
- Keeping provider is good in your actual code not in module developing.
- User-data logs will be in sudo su - , cd /var/log/ , ls -l , cloud-init.log , tail -f cloud-init.log
- To see the running logs in ansible-server of instances ? sudo su- , cd /var/log/ , tail -f cloud-init-
  output.log
- yaml file was mentioned in the 02-sg folder, it is just to refer how the sg connections are given
- No Problem if you delete ".terraform" folder and lock file.
