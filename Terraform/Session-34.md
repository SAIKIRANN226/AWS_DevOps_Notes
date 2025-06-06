### Creating resources in "Robosho-terraform"
- 01-vpc
- 02-sg
- 03-vpn
- 04-ec2
Go through the above code in VS. We have created VPC and Peering, ALl SG's, VPN, EC2 and Records. So now we want all instances to automatically configured, for that we need to create a "ansible-server" this server will provision all instances using ansible-playbooks and also create security group of port SSH 22 to connect all instances securely, but we already created VPN SG with SSH 22 right ? So we can use that also. So create this ansible-server in default subnet in default VPC. So ansible server is created, after creating server ansible should provision all the servers automatically, for this we need to write a small shellscript, to provision the instances "ec2-provision.sh" in VS. There is one disadvantage in "user-data" if one time failed, it will not come again, so we are addressing this with provisioners, so delete the ansible-server and address with provisioners.












### Points to remember
- We know how to develop the module and how to use the module
- SSM Parameter is to store the configuration, for example one project exports config, another one refers.
- Mostly in the companies, errors are not because of coding, it is because of configuration change, even if we
  make small changes in configuration, we get errors, so thats why we need to keep config independently.
- SG is very important since we are connecting to every resources present in aws.
- Individually we can understand every concept, but when we configure the project using all concepts, it will
  create huge confusion, like for example if we give a request from client or from our laptop, the request
  should reach to the end service which is present in aws, request will cross many stages like client-side
  configuration should be clear,vpc,igw,subnets etc. have many resources to cross to reach the end service.
  So this visualization should there in us. Thats why SG is important to use in every resources.
- Delete NAT gateway after use, because it has charges.
- Keeping provider is good.
- Dont forget to connect VPN then only we can connect to the private instances.
- User-data logs will be in sudo su - , cd /var/log/ , ls -l , cloud-init.log , tail -f cloud-init.log
- To see the running logs in ansible-server of instances ? sudo su- , cd /var/log/ , tail -f cloud-init-
  output.log
- 
