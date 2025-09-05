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

### How do you manage credentials in terraform ?
We need to be careful while handling credentials. Best practices are setting the env variables before we plan and apply the infra. Once it is applied we can unset. We can store the credentials in jenkins credentials if we are following CICD.

### Explain the concept of workspace ?
Terraform workspace is used to create multiple envs using same code. Terraform will give us a special variable terraform.workspace. If you are in dev then the value of terraform.workspace will become dev, same for prod also. We can control envs using lookup function.

### How does terraform manages updates to existing resources ?
Terraform always try to match the desired infra with current infra which is in terraform.tfstate, if current state is equal to desired state, it will not take any action, if not equal then it will create the infra.

### Create an ec2 instance in aws ?
Use provider.tf, variables.tf, data.tf etc. Dont simple write resource block.

### How to store sensitive data in terraform ?
Previously we used ansible vault, recently we migrated to SSM Parameter store, since our whole infra is in SSM Parameter store. We integrate ansible with SSM instead of depending ansible and ansible vault commands.

### Does terraform supports multi provider deployments ?
Yes, we can define multiple providers.

### If i lose the state file how can i recover ?
First of all its a serious issue because terraform uses this file to track the infra. We have to follow some best practices to keep the file safely and in a position to recover. We must use remote state and locking mechanism like S3 bucket and Dynamodb table. We must use data replication, anytime a state file is changed in a bucket, it will make another copy of it in different bucket in different region. Implement proper IAM roles to access state file so that nobody will update or delete. Still if there is a loss, we have to restore it manually.

### What is null resource in terraform ?
It will not create any resources but we can use this to make use of provisioners like remote-exec and local-exec, file provisioners, triggers etc.

### What are modules in terraform ?
We can create terraform code as modules. It is like Dry concept dont repeat yourself, that can be used by others also instead of writing code for the infra from the scratch.

### What is the difference between ansible and terraform ?
Terraform is IaC tool and ansible is configuration management tool. Even though ansible can create infra but ansible dont have state mechanism while terraform does. So thats why terraform is best for creating infra and ansible is best for configuration. We can integrate ansible with terraform to get end-to-end automation. Terraform will create instance and handover to ansible for configuration of servers.

### Terraform vs cloudformation ?
Terraform can be used for multi cloud providers. CF is only used for AWS infra. Terraform has a state functionality while CF uses stacks.

### Once you create ec2 instance using terraform, after that you added one tag manually then what will terraform do ?
First terraform will do refresh operation. It can find the changes happened outside the terraform and alert us. If you apply now then terraform will remove those manuall changes and try to match the desired infra with the current infra.

### How do you deploy your infra code into different environments ?
Tfvars, Workspaces, Different repos for different env

### What are provisioners in terraform ?
We have local-exec and remote-exec and what will do these ?

### Terraform apply fails due to a state lock file issue. How would you resolve it ?
State locking occurs when previous executing is not releasing the lock, we can either use force unlock using LOCK_ID command or we can go to dynamodb table and manually delete entry with LOCK_ID

### Your terraform deployment has created infra but some resources are not deleting even after destroying ?
This majorly happens when there is a dependency on resources. For example we cant delete the SG when it is attached to EC2. So first we make sure to delete dependent resources are deleted and then delete the next resource. Another reason is access issues.
