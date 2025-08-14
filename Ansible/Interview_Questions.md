### What is configuration management in ansible ?
Configuration management is the way of configuring the servers for consistency, scalability, reliability. This is master-node architecture. For example we have ansible server and ansible is installed in it. Then ansible will connect to servers (or) nodes using SSH connection. We write ansible playbooks that are version control in Git. Ansible can run these playbooks against nodes and also it connects to multiple servers at a time to achieve scalability. Since it is configuration as code, same code will work in multiple environments for consistency. Any changes in the configuration, it will immediately run the playbooks and it will reflect in the nodes.

### What are the ansible advantages over shell ?
Linux distributions, Scalability, Error handling, Readability, External systems, Sensitive information, Rich in modules, Easy to understand through YAML format.

### What are handlers in ansible ?
When there is a change in task, we can run another task through handlers. For example if there is a change in nginx configuration, then it will notify another task called restarting nginx.

### What is the significance of become keyword in ansible playbook ?
Become provide the sudo access to the playbook, so that it can install any thing in the server.

### How does ansible handle Idempotence and why it is important in ansible configuration ?
Providing same results irrespective of the number of executions is called idempotence. For example if user exist, it will not create, if not exist then it will create.

### How do you handle errors and exceptions in ansible playbooks ?
When there is an error in ansible playbook, bydefault it will exit the program. But we can manage errors in ansible through Ignore_errors: true, this option allows the playbook to continue even it faces any errors.

### Describe the structure of ansible playbook ?
Just write ansible playbook to install nginx and run the nginx.

### How do you configure inventory files in ansible ?
Inventory file is where we manage the hosts, group of hosts, group of groups that ansible can manage. We can also mention group level variables, host level variables inside the inventory.ini

### How can you store sensitive information such as passwords in ansible ?
We use ansible-vault feature to encrypt the sensitive information like passwords and usernames. Command to create ansible vault is "ansible-vault create secrets.yaml" while executing the playbook, we use the command like "ansible-playbook saikiran.yaml --ask-vault-pass" (or) we can keep "ask_vault_pass = True" in inventory.ini

### You need to manage a dynamic inventory where servers are frequently added or removed. How would you configure ansible to work with such a dynamic inventory ?
We have a plugin called "aws_ec3" it can pull the hosts based on region and filters.

### What are roles in ansible ?
Ansible roles is a proper directory structure to create and manage ansible playbooks. It contains vars, tasks, templates, handlers etc.

### How do you run a specific tasks in ansible ?
We can make use of tags in ansible. We can tag each task with tag value and include them while executing the playbook.

### What modules you have used in ansible ?
We have used many modules in our project like package, service, unarchive, get_url, copy, template, file, command, shell, systemd, import_role etc.

### How is Ansible different from other automation tools like Puppet or Chef ?
Ansible is agentless and uses SSH to connect to nodes and it is a PUSH based model.

### What is an Ansible Inventory ?
An inventory is a file (INI, YAML, or dynamic) that defines the list of hosts and groups where Ansible will run tasks. For example ini format is [webservers] web1.example.com web2.example.com

### What are Ansible Playbooks ?
Playbooks are YAML files containing plays. Each play maps a group of hosts to tasks.

### How do you run an Ansible playbook on a specific host from an inventory group ?
ansible-playbook -i inventory.ini playbook.yml --limit web1.example.com

### What is the difference between command and shell module in Ansible ?
Shell ---> It is like you login inside the server and run the command, Environment variables and redirections (Symbols) will work here. Command ---> It is like running the command outside the server, Environment variables and redirections (Symbols) will not work here.

### What is Idempotency in Ansible ?
If you run program multiple times, that can create samething multiple times, where as in ansible, if the user does not exist then it will create, if exist it will ignore, that means even if you run the program infinite times also, it will not create any damage. Providing same results irrespective of the number of executions is called idempotence.

### How do you debug Ansible playbooks ?
Use debug module -v, -vv or -vvv

### How do you connect Ansible with AWS ?
Install boto3 and AWS CLI. Use dynamic inventory scripts (aws_ec2 plugin). Create playbooks using AWS modules like ec2_instance, s3_bucket.

### You need to run a playbook on only those hosts where a service is down. How would you handle it ?
Use the when condition with service_facts:

### A production deployment failed midway due to a network issue. How do you ensure Ansible resumes from where it left off ?
Use --start-at-task option, like ansible-playbook deploy.yml --start-at-task="Install dependencies"

### You need to dynamically add newly launched AWS EC2 instances to your Ansible runs.
Use the aws_ec2 dynamic inventory plugin --> plugin: aws_ec2

### Default Ansible inventory file location ?
/etc/ansible/hosts

### Which file sets Ansible’s default configurations ?
ansible.cfg

### How do you repeat a task for multiple items ?
Using loops 
