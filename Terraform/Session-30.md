### Overview of Previous Session
1. Created VPC.
2. Created Internet gateway and attach to the VPC.
3. Created Public, Private & Database subnets in atleast 2-AZ for High Availability.
4. Created route tables (Public,Private,Database) and associate it with their respective subnets in two 
   regions 1a and 1b.
5. Added Internet Gateway route in the Public_route table because internet should be enabled in public.
6. Enable auto-asign public_Ipv4 address only to the public_subnet not in the private_subnet.Note:- When you
   create VPC, aws will automatically create default route table (10.0.0.0/16) to communicate between subnets.

### High Availability
az-1 = one public_subnet     = 10.0.1.0/24 ---> us-east-1a

az-2 = another public_subnet = 10.0.2.0/24 ---> us-east-1b

az-1 = one private_subnet     = 10.0.11.0/24 ---> us-east-1a

az-2 = another private_subnet = 10.0.12.0/24 ---> us-east-1b

az-1 = one database_subnet     = 10.0.21.0/24 ---> us-east-1a

az-2 = another database_subnet = 10.0.22.0/24 ---> us-east-1b

### "NAT Gateway" is used to enable outgoing internet
If we need to update any package or download something in the private subnets, for this we need to connect to internet. But what traffic is this ? is it OUTGOING? or INCOMING?. If server wants to download something then it is OUTGOING traffic, INCOMING traffic is already disabled in the private_subnets. So if we want to go outside and download safely we have something called "NAT Gateway" --> This should be created in the public subnet (1a or 1b) because we have given internet access to the public_subnets, creating NAT Gateway is not enough we need to add routes between private_subnets and to Internet gateway (NAT) which is in public_subnet. Then only private_subnets can access internet and download anything. Like for example if only one of the private_subnets wants to connect to internet then this private_subnet should have a road (route) to internet gateway (NAT) which is in public_subnet. So like that which ever private_subnets like data base subnet or any other private_subnets wants to connect to internet, they should add route to the NAT gateway which is in public_subnet. So you need to add in the route tables (Private and Database) then only you will get access to the Internet. So select any of the private_subnet/routes/edit_routes/add route (Destination= 0.0.0.0/0,Target= NAT gateway,Select default one in dropdown under Target section only). [Note:- Here when you create a NAT gateway, aws will create instance in the background (we dont have access to that) that means NAT and elasticIP is chargeable, Before creating NAT gateway we have one rule because created instance in the background has IP_address which is dynamic whenever you off and on, it will change the IP address, for that we need to create elastic_IP, so create elastic_IP address first --> Then create NAT Gateway. [Note:- If you want static IPaddress we need to pay money, like for example even your home public_ip is dynamic it is changing everytime, so if you want static home public_IPaddress you need to pay to the ISP provider in your area.

### VPC peering in aws cloud
Example of the two villages, for every village we have pincode, so similarly in the VPC what is pincode ? 
That is "CIDR". Bydefault we cannot connect two VPCs, it is possible through VPC peering, only when both 
VPC's should have different CIDR. Then only VPC peering is possible. Below is the example.
Requestor VPC = I want to connect with you please accept my request.
Acceptor VPC  = Ok i will accept your request.

### Possibilities of VPC peering
- VPC in same region and same account
- VPC in another region and same account
- VPC in same region and another account
- VPC in different region and another account

### Below is the example of VPC peering
So let us take "Requestor VPC = Roboshop VPC ; Acceptor VPC = Default VPC". Now try to create VPC peering connection, after creating in the same account you need to accept request in the "Actions" option. Take example of villages now you have created a main road (Peering Connection) between two villages, but if you want streets (every subnets or only which ever subnet you want) to connect to main road, so connect all streets roads to the VPC peering main road, nothing but routes right ? so try to add routes in the main route table, go to the VPC main route table there edit routes in destination give the other VPC_CIDR to connect and target should be peering connection and under the peering connection select the dropdown option and save it. If it is not reflecting then you need to add routes in all route tables explicitly. If you want only one or two private subnets wants to connect to the vpc peering main road then you can only add in those two route tables only. This is nothing but routes in VPC, generally when you are connecting to 2 villages we need to get pin codes of 2 villages in the destination and give peering connection in the target, add in all public and private and main route table explicitly if you want all subnets to connect to the vpc main road.

### Terraform-aws-vpc Module development in VS
- Terraform-aws-vpc ---> Is a module we are developing.
- Terraform-vpc-test ---> Is we are testing wether the module is working or not.

### Now create below all these with terraform code
1. Create VPC
2. Create Internet gateway and attach
3. Create all subnets
4. Create route tables
5. Create routes
6. Associate with subnets
7. Create elastic_IP
8. Create NAT
9. Add NAT gateway route in public and database subnets
10. Peering connection
11. Routes

### "Common tags" this is a map & below is the example
We have tagging strategy, like we have more resources in roboshop project like vpc subnet,routes tables,NAT gateway and many more, so for all these resources we have common tags to use like below.

      Project = "Roboshop"
      Terraform = "true"
      Environment = "dev" 
      Name = "Saikiran"

This tags are applicable to all resources. We can overwrite this common tags any time and resource tags are specific tags.

### "Resource tags" this is also a map
Similarly we have different tags like vpc tags,subnet tags,nat tags etc. But we want both tags,for example we have Name = "Mothkur" in resource tags compared to Name = "Saikiran" in common tags, what will happen if we merge common tags and resource tags ? then resource tags only applicable, that means Name = "Mothkur" in resource tags will be considered. So for this we have function in terraform that is "terraform merge","tags = merge(var.common_tags, var.vpc_tags)", we can merge as many maps we want. So now we are developing VPC module thats why we use vpc_tags in code.

### Points to remember
- To go directly in to your working folder in gitbash by "cd /d/repos/terraform-vpc-test"
- When you create a NAT Gateway automatically a instance will be created in the background, we cannot access
  this instance, this instance IP_address will be changing dynamically whenever you off and on, so we need to
  create elastic IP_address, and then create NAT gateway.
- Tagging strategy is important in terraform.
