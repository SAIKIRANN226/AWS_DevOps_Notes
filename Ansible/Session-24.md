### Ansible vault
Till now we have given passwords in the terminal or in the ansible.cfg file right ? but it is not secure, so we now use ansible vault, nothing but storage of secrets, for example below.
- Encoding ---> A proper pattern to encode the text, in this everybody can guess the secret.
- Encryption ---> Generating a random text with mathematic algorithm, so we encrypt ansible vault, so those
  who know the password they can only Dycrypt the code.

### How to create ansible vault in ansible-server ?
- Create one folder for "vault" and a sample playbook (01-playbook.yaml) inside the vault in VS.
- Create group_vars folder inside the vault in server and then 
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

### Points to remember
- We use ansible.cfg to minimize the commands while running the script in server.
- If esc button is not working while saving the file you can use "ctrl+esc" or "ctrl+c" button
- Use "ansible-vault encrypt group_vars/<some-name>.yaml" if already has existing vault.
- If you want to edit then "ansible-vault edit web.yaml"
- If you want to know wether it is encrypted or not ? then "cat group_vars/<some-name>.yaml"
- If you want to see then "ansible-vault view group_vars/<some-name>.yaml"
- You can use ansible-vault anywhere in the roboshop project for any components you want.
- Earlier we used Ansible-vault and we migrated to AWS SSM Parameter store since our entire infra is in AWS.
- 
