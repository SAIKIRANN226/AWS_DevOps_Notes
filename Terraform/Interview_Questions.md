### What is terraform and why we use it ?
It is an Open-Source tool, developed by hashicorp. Terraform is popular IaC. It is best in the market rightnow because of its advantages like V, C, A, I, C, A, M, H

### Ansible vs Terraform when to use ? What is the purpose ?
Ansible is a popular configuration management tool and Open-source tool. It is only intended for configuration management and application deployment using playbooks and these playbooks are version controlled in Git, since our source code is also Git. Ansible can also create infra but it is not recommended because ansible does not have a state file while terraform does. So thats why terraform is best for creating infra and ansible is best in configuration management. So we integrate terraform with ansible. Once terraform create servers, it can handover to ansible and ansible will takecare of the configuring servers.

### Explain terraform commands ?
We have commands like terraform init, plan, apply, destroy.

### What is the state in terraform ?
Terraform uses state file to compare desired infra with the existing infra which is in current state (terraform.tfstate) if desired state == current state then terraform will not take any action, if desired state is ==/== current state, then terraform will create the infra. So terraform responsibility is to match desired infra with actual infra.

### What is the remote state in terraform ?
Saving state in locally is not recommended because in a collaborative envionment if multiple persons are working on the same infra there is high chances of duplicates and errors like already exist, so we have to keep it safely in the remote storage like s3 bucket and locking this bucket with dynamodb, so that nobody will do any changes.

        backend "s3" {
          bucket = "saikiran"
          key = "msk"
          region = "us-east-1"
          dynamodb_table = "sai-table"
        }

### Explain variables in terraform ?
Variables are used to parameterize the infrastructure. We have types of variables like list, string, map, bool, number. However data-types are no that much important, because terraform will automatically consider which data-type is.

### What is Tfvars in terraform ?
It is a file which has key-value pair, these values will override the default values in variables.tf file. We can use different tfvars like dev.tfvars (or) prod.tfvars to provision the infra in multiple environments. We should use -var-file tag to pass tfvars file to the terraform command.

### What is count and count.index in terraform ?
We use count parameter to create multiple instances and route53 records based on a specific count. We use length function here so that it will calculate the length of the list automatically. Count.index is used to refer the index from 0

### What are outputs in terraform ?
When we create resources in terraform, it will give us attributes of the resource it created. These output values are useful in creating another resources. Module developers expose output values, module users will use it to create another resources

### What are data-sources in terraform ?
Terraform is connecting to providers like aws cloud and we have lot of information in it which are changing dynamically, so we query that data dynamically using data-source and use them to creat another resources.

### What are locals in terraform ?
Locals are also a type of variables. It is a key-value pair and we can use it anywhere we want. It has extra capabilities like keeping expressions, conditions, functions inside the local, variable values can be overridden but locals cannot be overidden.

### What are functions in terraform and name few of them ?
Basically when we give some input to the function, it will give us few ouputs like we have used length, lookup (To find the value of a key in a map), join, split, slice, file
