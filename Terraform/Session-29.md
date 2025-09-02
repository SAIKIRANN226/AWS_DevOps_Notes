### Module development
Dry concept, dont repeat yourself. For example we created infrastructure for a project, nothing but we wrote a terraform code for this whole infra right ? If we got another new project, do we write the terraform code from the scratch ? NO! we dont write the code from the scratch instead we reuse the code, so no need to write the infra for every project from the scratch if we developed modules. So go through the code of "Terraform Modules" in the VS, where we developed EC2 module. Provider will not be there in module developing.

	  module "name-of-module" {
			source = "../ec2"
	  }
	      
### Two types of Modules
1. Customized modules for our organisation, this will be developed by central team in cloud.
2. Open-source modules, this can be used from the internet.

### Two types of Roles
1. "Module Developer" ---> Who develops the module
2. "Module User" ---> Who consumes the module.
   
Put one README.md file to provide the documentation on the module how to use it by others, purely its DevOps responsibility to write documentation.

### VPC (Virtual Private Cloud)
Amazon VPC is a virtual network that you create in AWS. It’s your own isolated section of the AWS cloud where you can launch AWS resources (Like EC2 instances, Databases, etc.) in a secure and controlled environment. Think of it like your own Private Data-center in aws cloud. Breaking main building block of VPC as below.
- Subnets ----> Divides your VPC into smaller networks. Can be Public or Private.
- Route tables ---> Controls how traffic is routed within the VPC and outside (Like to the internet).
- Internet Gateway(IGW) ---> Allows Public to access internet to resources in Public subnets.
- NAT Gateway Instance ---> Let Private subnets access the internet without being exposed.
- Security Groups ---> Act as firewalls for instances (e.g., EC2).
- Network ACLs ---> Act as firewalls for subnets.
- Elastic IP ---> A Public static IP you can assign to an instance.

### How VPC works is the below diagram

                   "Internet" is nothing but Service Provider (Airtel,jio,actfiber etc.)
                       |
              +------------------+
              | Internet Gateway | Router in home which is connected to Public_subnets
              +------------------+
                       |
                [ Public Subnet ]
                  /     |       \
                 /      |        \
             EC2-1    EC2-2      ...
                       |
               [ Private Subnet ]
                   (e.g., DB)

### Why we use VPC in aws ?
- Isolation & Security ---> Fully control traffic in/out of your resources.
- Custom IP Addressing ---> Use your own IP ranges (CIDR blocks).
- Control Access ---> With security groups, NACLs, and route tables.
- Hybrid Connectivity ---> Connect on-premises data centers using VPN or AWS Direct Connect.

### Difference between Public_subnet and Private_subnet ?
Subnets who have access (Route) to the internet gateway are Public_subnets, subnets who dont have access (route) to the internet gateway are Private_subnets (or) subnets are attached to internet gateway are called Public_subnets, which are not attached to the internet gateway are called Private_subnets, here Internet gateway is nothing but arch in village example and router in home example. Use NAT to allow internet outbound traffic from Private subnet without allowing inbound traffic.

### CIDR (Classless Inter-Domain Routing)
It is used to allocate IP addresses efficiently, like dividing the large CIDR block (VPC) into a smaller networks. Nothing but assigning individual IP addresses from VPC CIDR block (e.g., 10.0.1.0/24) efficiently to the resources like ec2, containers in dockers, VMs, load balancers, or databases and also to the other subnets in VPC. Practical Example in DevOps. For suppose you’re setting up an AWS VPC as below.

1. VPC CIDR: 10.0.0.0/16 (65,536 IPs).
2. Subnets:
   Public subnet: 10.0.1.0/24 (256 IPs for web servers).
   Private subnet: 10.0.2.0/24 (256 IPs for databases). etc like that
3. Security group rule: Allow HTTP traffic from 0.0.0.0/0 (any IP) to the public subnet.

### Create Roboshop Network - VPC
Create VPC network for Roboshop Project. You need to give CIDR while creating VPC, nothing but like pin code of a village, here siva has given 10.0.0.0/16, so this IP is Public (or) Private ? Internet has given some "Private_ip address range" you can search in google there you find three ranges and those only allocated to Private_ip not for Public_ip, there you can see 24,20,16 bit-blocks, these are only for Private_ip not for Public_ip, even ISP people will configure your Private_ip address in any range among these 3 bit-blocks, as of now you can select any one for your VPC, so from this siva selected starting from 10. Atleast you need to create 16 servers to use VPC, 10.0.0.0/28 ---> 16 servers, 10.0.0.0/16 ---> 65k servers, generally we give VPC_CIDR 10.0.0.0/16 only, because it does not cost anything, so we can go for maximum.

### Create Roboshop Public_subnets and Private_subnets
Here in "IPV4 subnet CIDR block" section you can give 10.0.1.0/24 ---> Public
Here in "IPV4 subnet CIDR block" section you can give 10.0.2.0/24 ---> Private

### Create Public and Private route_tables
Make sure you select your created VPC, not default for all the above subnets and tables

### Now associate route_tables to the respective subnets
Click on the created Public_subnet ---> Select Route table ---> Edit route table association ---> Then associate with Public route_table which you have already created & do same for the Private_subnet also. 

### Giving internet access to the Public_subnets
Select Public route_table which you have created, click on Routes/edit_routes/add_route ---> In destination section give internet notation (0.0.0.0/0) ---> and Internet gateway in the Target section and select default from the drop down under the internet gateway only ---> Then save changes. That means public subnets got the internet access and we dint given internet access to Private subnets that is the difference.

### Create Internet gateway (Router)
Make sure attach this Internet gateway to your VPC, you can see the option on top as soon as you created.

### Enable auto-asign public Ipv4 address
This must be enable to only Public_subnet, not for the Private_subnet. You can do this by clicking on the Public_subnet ---> Actions ---> Edit subnet settings, just check the box. Note that create web server in the Public_subnet and remaining severs like cart, shipping etc. can be created in the Private_subnets.

### Create a subnet for Database
10.0.3.0/24 and create Database route table and attach it to the Database subnet.

So what ever we have created all these by manually in the aws, we should create this by using terraform and you need to create resources in minimum two availability zones, so that you can save yourself from the natural disasters, that means you need to keep Public and Private subnets aswel as remaining subnets in two availability zones, if the company is having budget then we can create servers in both zones (or) create one and transfer (Move or create in another zone in case of any natural disasters alert).

### Points to remember
- Terraform best practices like naming the resources in terraform search in google. Because terraform
  has state file and it will track all the resources using names only.
- We used Open source modules sometimes, we have dedicated cloud team who develops module and we use them.
- How do you check internet is working or not ? "ping google.com"
- Ipv4 is 32bit and Ipv6 is 64 bit 
- Router (Internet Gateway) ---> It has Public_IP & Private_IP. Public_IP is nothing but just type what is      my ip in google, there you can see Ipv4 address that is your Public_IP, not ipv6. What is your Private_IP
  just "ipconfig" in cmd there you can see IPv4 address under Under wireless LAN adapter Wifi.
- What is your actual IPaddress ? Just type in google "what is my IP", if anybody wants to connect
  to my laptop you can connect using this IP address only. You cannot connect with private_ip address.
- Your created VPC is Isolated, even aws dont have access to it.
- AWS wont charge for VPC's, subnets, route tables, it only charges when you are creating server.
- We can create as many private subnets we want, however for functionality purpose we have only two subnets
  which is Public and Private subnets.
- Watch from 26:11 to 1:14:21 to understand how VPC works.
