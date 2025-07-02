- What is terraform and advantages of terraform ?
- Terraform installation and setup ?
- Syntax of terraform to create any resources ?
- Terraform commands and their functionality ?
- Variables syntax ?
- Importance of ".gitignore" in terraform.
- Terraform.tfvars and variable preferences ?
- We have used length_function.
- We used output block to print the output of the resources.
- Locals is terraform and why count.index will not have access in locals block.
- Data-sources in terraform.
- Types of loops and their use ? count_based, for_each and dynamic_loop.
- Terraform state (state and remote state)
- Create an S3 bucket and lock the bucket using dynamodb table.

### Below are the resources created using terraform code
- Create VPC
- Create Internet Gateway and attach to the VPC
- Create Public, Private and Database Subnets in minimum 2AZ for High availability
- And also create "Data-based" subnet group, since database subnet having different behaviour
- Create Elastic_IP 
- Create NAT Gateway
- Create Route_tables for Public, Private and Database subnets and associate it with their 
  respective subnets in two regions (1a and 1b)

- Add Internet Gateway route in the Public Route_table
- Enable Auto-asign Public_IP to the Public_subnet
- What is NAT Gateway and why it is useful in Private_subnets ?
- Create VPC peering connection
- Developed "VPC" module and tested simultaneously
- We used tagging strategy like "common_tags and resource_tags"
- 

