### Creating below resources using terraform code
- VPC 
- Internet Gateway
- Public, Private and Database subnets
- Database subnet group, since database has different behaviour
- Elastic_ip
- NAT Gateway
- Public, Private, and Database route tables
- Added Public, Private, and Database routes
- Public, Private, and Database route table associations
- Peering connection (you can see this explanation in points to remember)
- Adding the routes, nothing but we call it as routes in VPC.

Now successfully we developed the module, and we now push it to the internet (github), so now my written module is in internet, if someone wants to use this, then you should refer it through the github, by using "source = "git"::<https URL>ref=main", so when you do "terraform init" the module will be downloaded in the testing code and terraform will create a folder called "module" automatically.

### How to use security groups effectively ?
For example according to the diagram mongodb should accept connections only from catalogue and user module, so we need to create a special security group to the mongodb and naming convention like roboshop-dev-mongodb, and ingress rules like accept connections only from catalogue and user module etc. Similarly we need to create for other modules also. We also need VPN, we cannot connect directly to the instances which are present in the private subnets, so create a VPN in default VPC, then connect to VPN in your laptop then only you can access instances.

### Points to remember
- We need terraform to create 100 % of the project infrastructure, not just by creating few resources like VPC
  or SG etc.
- In this class we continue from creating database subnet.
- First create Elastic IP and then create NAT gateway.
- We also have open source modules, search in google "terraform aws vpc module", terraform only provides us.
- We can create a folder (example) and keep all the testing code in it, so that it will be easy for everyone
  to use the module.
- Till now we used allow-all while creating SG, it is just for practice only, from next session we follow
  correct practice.
- It may not require for everyone, when this peering is useful ? bydefault peering connection between two
  VPC's is not possible, if we want to connect with the resources which are in another VPC, then you require
  peering, for example big projects like banking they dont depend on one company, they tie up with multiple
  companies and these companies deals different module like one company is dealing web module, another is
  dealing cart module, another is dealing shipping module etc. That means these companies have different
  accounts, so to collaborate with other VPC's which are present in different companies, then we need VPC
  peering connection. So users can decide if peering is required or not ? if required they have to give
  VPC peering_id, if they are not giving we should consider default VPC. For example consider Requestor is
  "Roboshop" and "Acceptor" is User provided VPC or Default VPC. If acceptor VPC is not in our control, can we
  get the access to add route ? NO, so we need to inform them to write an acceptor code in their terraform.
