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
Ansible roles is a proper directory structure to create and manage ansible playbooks. It contains 
