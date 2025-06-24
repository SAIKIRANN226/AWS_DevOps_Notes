### Ansible vault
Till now we have given passwords (or) usernames in the terminal (or) in the ansible.cfg file right ? but it is not secure, so we now use ansible-vault, nothing but storage of secrets like keys,passwords etc.
- Encoding ---> A proper pattern to encode the text, in this format everybody can guess the secret.
- Encryption ---> Generating a random text using mathematic algorithm (AES256) tough to guess, so we encrypt
  ansible-vault, those who know the password they can only decrypt the code. Below are the examples.
- asaiaavaa ----> sai (encoding)
- hsdh234sk456jdksd ----> sai (encryption)

### How to create ansible vault in ansible-server ?
- Practice folder (Your working directory)
- vault folder (Create inside the Practice folder)
- group_vars folder (Create inside the vault folder)
- Create vault file inside the group_vars folder using below command.
- "ansible-vault create Practice/vault/group_vars/some_name.yaml"
- Create ansible.cfg, inventory.ini and your playbook files (Inside the Practice folder not in vault or
  group_vars folders)
- Put "ask_vault_pass=True" in ansible.cfg (or) "ansible-playbook 01-playbook.yaml --ask-vault-pass"
- How to connect to the instance ? "ansible-playbook 01-playbook.yaml" since we have inventory in
  separate file and username/passwords are kept in vault.
- Since our infra is in SSM Parameter in AWS systems manager, this is also a vault from AWS, but we integrate
  ansible-vault with the SSM Parameter and we fetch the values from AWS instead of depending on ansible-vault
  and ansible-vault commands.

### Dynamic Inventory
- Till now we dint used aws cloud services completely, its like a on-premise for us, like we have only servers
  and domain thats it.
- For example we have 10 servers now, because of traffic and i need to run ansible-playbook against these
  servers, then ansible will connect to AWS ---> It will fetch IP_addresses of the servers dynamically, how
  will ansible will fetch ?
- If you want to run update to the all web instances then "ansible-instance" should connect to AWS and fetch
  instances with name "web" which are present in us-east-1 region. We use "ansible ec2 inventory"

### What is Plug and Play
- If your ansible-server wants to connect to the external systems like azure,gcp or alibaba etc. Then we need
  to add some plug (of azure,gcp or alibaba), thats what we call plug, similarly if ansible have plugin
  to connect to aws ec2, we can fetch IP_addresses. That is nothing but "AWS Dynamic inventory plugin"

### Points to remember
- We use ansible.cfg to minimize the commands (or) arguments to the script in server.
- If esc button is not working while saving the file you can use "ctrl+esc" or "ctrl+c" button.
- Use "ansible-vault encrypt group_vars/<some_name>.yaml" if already has existing vault.
- If you want to edit then "ansible-vault edit web.yaml"
- If you want to know wether it is encrypted or not ? then "cat group_vars/<some_name>.yaml"
- If you want to see then "ansible-vault view group_vars/<some-name>.yaml"
- You can use ansible-vault anywhere in the roboshop project for any components you want.
- Earlier we used Ansible-vault and we migrated to AWS SSM Parameter store since our entire infra is in AWS.
- Boto and botocore are aws python modules, we need to install latest, "sudo yum list | grep pip", then install
  sudo yum install python3.11-pip.noarch -y
- Then "pip3.11 install boto3 botocore"
- We can't create ansible-vault in windows (VS), so thats why we used linux server to create the vault folder
  and group_vars folders and inside the group_vars folder we create vault using command.
