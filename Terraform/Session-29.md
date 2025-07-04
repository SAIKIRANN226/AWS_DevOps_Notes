### Module development
Dry concept, dont repeat yourself. For example we created infrastructure for a project, nothing but we wrote a terraform code for this infra right ? If we got another new project, do we write the terraform code from the scratch ? NO! we dont write the code from the scratch instead we reuse the code, so no need to write the infra for every project from the scratch, go through the code of "Terraform-Modules" in the VS. Provider will not be there in module developing. Module syntax is below.

              module "name-of-module" {
	                source = "../ec2"
              }
	      
### Two types of modules and Two types of roles
1. Customised modules for our organisation, this will be developed by central team in cloud.
2. Open-source modules. "Module Developer" Who develops the module and "Module User" Who consumes the module.
Note:- Put one README.md file to provide the documentation on the module how to use it by others, purely its DevOps responsibility.

### VPC - Virtual Private Cloud
Amazon VPC is a virtual network that you create in AWS. It’s your own isolated section of the AWS cloud where you can launch AWS resources (like EC2 instances, databases, etc.) in a secure and controlled environment. Think of it like your own private data center in aws cloud. Breaking main building block of VPC as below.
- Subnets ----> Divides your VPC into smaller networks. Can be public or private.
- Route tables ---> Controls how traffic is routed within the VPC and outside (like to the internet).
- Internet Gateway(IGW) ---> Allows public to access internet to resources in public subnets.
- NAT Gateway Instance ---> Lets private subnets access the internet without being exposed.
- Security Groups ---> Act as firewalls for instances (e.g., EC2).
- Network ACLs ---> Act as firewalls for subnets.
- Elastic IP ---> A public static IP you can assign to an instance.

### How VPC works is the below diagram

                   "Internet" is nothing but a service provider (airtel,jio,actfiber etc.)
                       |
              +------------------+
              | Internet Gateway | router in home which is connected to public_subnets
              +------------------+
                       |
                [ Public Subnet ]
                  /     |       \
                 /      |        \
             EC2-1    EC2-2      ...
                       |
               [ Private Subnet ]
                   (e.g., DB)

Public subnet: Resources (like EC2) that need internet access. So that public can access their websites. Private subnet: Resources (like databases) that shouldn’t be exposed to the internet. Use NAT to allow internet outbound traffic from private subnet without allowing inbound traffic.

### Why we use VPC in aws ?
- Isolation & Security ---> Fully control traffic in/out of your resources.
- Custom IP Addressing ---> Use your own IP ranges (CIDR blocks).
- Control Access ---> With security groups, NACLs, and route tables.
- Hybrid Connectivity ---> Connect on-premises data centers using VPN or AWS Direct Connect.

### Example of a use case if you want to host a web app
- Frontend (EC2 or Load Balancer) in a public subnet
- Backend (database) in a private subnet
- Use security groups to allow only the frontend to talk to the backend
- Use a NAT Gateway so the backend can update packages via the internet, but isn’t reachable from the outside

### Summary of the VPC
- VPC ---> A private network in AWS, or a private data center
- Subnet ---> A segment within a VPC (can be public or private)
- IGW ---> Provides internet access to public subnets
- NAT Gateway ---> Allows outbound internet from private subnet
- Security Group ---> Instance-level firewall
- Route Table ---> Controls network traffic routes

### Difference between Public_subnet and Private_subnet ?
Subnets who have access (route) to the internet gateway are public_subnets, subnets who dont have access (route) to the internet gateway are private_subnets or subnets are attached to internet gateway are called public_subnets, which are not attached to the internet gateway are called private_subnets, here Internet gateway is nothing but arch in village example and router in home example.

### CIDR (Classless Inter-Domain Routing)
It is used to allocate IP addresses efficiently, like dividing the large CIDR block (VPC) into a small networks. Nothing but assigning individual IP addresses from VPC CIDR block (e.g., 10.0.1.0/24) efficiently to the resources like ec2, containers in dockers, VMs, load balancers, or databases and also to the other subnets in VPC. Practical Example in DevOps. For suppose you’re setting up an AWS VPC as below.

1. VPC CIDR: 10.0.0.0/16 (65,536 IPs).
2. Subnets:
   Public subnet: 10.0.1.0/24 (256 IPs for web servers).
   Private subnet: 10.0.2.0/24 (256 IPs for databases). etc like that
3. Security group rule: Allow HTTP traffic from 0.0.0.0/0 (any IP) to the public subnet.

### Create Roboshop Network - VPC
Create VPC network for Roboshop Project. You need to give CIDR while creating VPC, nothing but like pin code of a village, here siva has given 10.0.0.0/16, so this IP is public or private ? so internet has given some "private ip_address range" you can search in google there you find three ranges and those only allocated to private_ip not for public_ip, there you can see 24,20,16 bit-blocks, these are only for private_ip not for public_ip, even ISP people will configure your private_ip address in any range among these 3 bit-blocks, as of now you can select any one for your VPC, so from this siva selected starting from 10. Atleast you need to create 16 servers to use VPC, 10.0.0.0/28 ---> 16 servers, 10.0.0.0/16 ---> 65k servers, generally we give 10.0.0.0/16 only, because it does not cost anything, so we can go for maximum. You can take VPC CIDR as 10.0.0.0/16 while creating VPC in aws.

### Create Roboshop Public_subnet and Private_subnet
Here in "IPV4 subnet CIDR block" section you can give 10.0.1.0/24 ---> Public
Here in "IPV4 subnet CIDR block" section you can give 10.0.2.0/24 ---> Private

### Create Public and Private route_tables
Make sure you select your created VPC, not default for all the above subnets and tables

### Now associate route_tables to the respective subnets
Click on the created public_subnet ---> select Route table ---> edit route table association ---> then associate with public route_table which you have already created and do same for the private_subnet also. 

### Giving internet access to the public_subnets
Select public route_table which you have created, then click on Routes/edit_routes/add_route ---> In destination section give internet notation (0.0.0.0/0) ---> and Internet gateway in the Target section and select default from the drop down under the internet gateway only ---> then save changes. That means public subnets got the internet access and we dint given internet access to private subnets that is the difference.

### Create Internet gateway (router)
Make sure attach this Internet gateway to your VPC, you can see the option on top as soon as you created.

### Enable auto-asign public Ipv4 address
This must be enable to only public_subnet, not for the private_subnet because it is not required for private_subnet, you can do this by click on the public_subnet ---> actions ---> edit subnet settings, just check the box. Note:- We need to create web server in the public_subnet and remaining severs like cart,shipping etc. can be created in the private_subnets.

### Create a subnet for database
10.0.3.0/24 and create database route table and attach it to the database subnet.

So what ever we have created all these by manually in the aws, we should create this by using terraform and you need to create resources in minimum two availability zones, so that you can save yourself from the natural disasters, that means you need to keep public and private subnets aswel as remaining subnets in two availability zones, if the company is having budget then we can create servers in both zones (or) create one and transfer (move or create in another zone in case of any natural disasters alert).

### Points to remember
- Terraform best practices like naming the resources in the terraform search in google.
- We used open source modules sometimes and we have dedicated cloud team who develops module and we use them.
- How do you check internet is working or not ? "ping google.com"
- Ipv4 is 32bit and Ipv6 is 64 bit 
- Router (Internet Gateway) ---> It has Public_IP and Private_IP, Public_IP is nothing but just type what is    my ip in google there you can see Ipv4 address that is your Public_IP, not ipv6. What is your Private_IP
  just "ipconfig" in cmd there you can see IPv4 address under Under wireless LAN adapter Wifi.
- What is your actual IPaddress ? Just type in google "what is my IP", if anybody wants to connect
  to my laptop you can connect using this IP address only. You cannot connect with private_ip address.
- Your created VPC is Isolated, even aws dont have access to it.
- AWS wont charge for VPC's, subnets, route tables, it only charges when you are creating server.
- We can create as many private subnets we want, however for functionality purpose we have only two subnets
  which is Public and Private subnets.
- Watch from 26:11 to 1:14:21 to understand how VPC works.
