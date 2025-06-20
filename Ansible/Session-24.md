### Ansible vault
Till now we have given passwords (or) usernames in the terminal (or) in the ansible.cfg file right ? but it is not secure, so we now use ansible-vault, nothing but storage of secrets like keys,passwords etc.
- Encoding ---> A proper pattern to encode the text, in this format everybody can guess the secret.
- Encryption ---> Generating a random text using mathematic algorithm (AES256) tough to guess, so we encrypt
  ansible-vault, those who know the password, they can only decrypt the code.
- asaiaavaa ----> sai (encoding)
- hsdh234sk456jdksd ----> sai (encryption)

### How to create ansible vault in ansible-server ?
- "ansible-vault create /path/<some_name>.yaml"
- Create one folder for "vault" and a sample playbook (01-playbook.yaml) inside the vault in VS.
- Create "group_vars" folder inside the vault in server.
- For example create a vault inside the group_vars folder using "ansible-vault create group_vars/web.yaml"
- Set vault password and then enter your values like ansible_user: centos ; ansible_password: DevOps321
- So now we have web component username and password is in group_vars/web.yaml
- How to connect to the web instance ? "ansible-playbook 01-playbook.yaml" since we have inventory in
  separate file and username and passwords are in vault and you need to keep "ansible.cfg" file give
  ask_vault_pass=True then only it will ask to enter the vault password
- If you dont give "ask_vault_pass=True" then you need to give from the command prompt only like below
  "ansible-playbook 01-playbook.yaml --ask-vault-pass"
- SSM Parameter, since our infra is in SSM Parameter in AWS systems manager, this is also a vault from AWS,
  we integrate Ansible-vault with the SSM Parameter and we fetch the values from AWS instead of depending on
  ansible-vault and ansible-vault commands.

### Dynamic Inventory
- Till now we dint used aws cloud services perfectly, its like a on-premise, like we have servers and domain
  thats it.
- For example we have 10 servers now because of traffic, and i need to run ansible-playbook against these
  servers, then ansible will connect to AWS ---> Fetch IP_addresses of the servers dynamically, how will
  ansible will fetch ?
- If you want to run update to the all web instances then "ansible-instance" should connect to AWS and fetch
  instances with name "web" in us-east-1

### What is Plug and Play
- If your ansible-server wants to connect to the external systems like azure,gcp or alibaba etc. Then we need
  to add some plug (regarding azure,gcp or alibaba), thats what we call plug, similarly if ansible have plugin
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
- We can't create ansible-vault in windows (VS), so thats why we used linux server to create the vault.
