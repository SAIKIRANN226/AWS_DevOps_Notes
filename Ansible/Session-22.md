### To run the file or program in the background
"nohup ansible-playbook -i inventory.ini -e ansible_user=centos -e ansible_password=DevOps321 <file-name> mongodb.yaml & >> /dev/null" ---> Output will be in nohup.out, it will not come in the terminal, if it is a small instance, we cant run every script in the background, because memory consumption will be high, so you can run only few scripts in the background.

### Ansible roles
It is a dry principle, dont repeat yourself like we used functions in shellscript. It is a proper directory structure to keep our configuration and we can share this with other users also. Refer Roboshop-ansible-roles in VS. Command to run playbook for ansible role is "ansible-playbook -i inventory.ini -e ansible_user=centos -e ansible_password=DevOps321 -e component=mongodb main.yaml"

### How to debug if you are facing any error
"ansible-playbook -vvv -i inventory.ini -e ansible_user=centos -e ansible_password=DevOps321 -e component=mongodb main.yaml" we will get the full information in the terminal, which is happening in the background, so that we can see where is the error.

### Points to remember
- To see the logs running in the background use "tail -f nohup.out"
- To set the indentation in VS use "shift+tab and tab"
- mongodb.repo, catalogue.service, user.service etc. these files are called supporting files, this we can keep
  in the files roles.
- Creating every role is not mandatory, we can create only what we required.
- If you want to call a common role in any roles like catalogue,mongodb etc. Use "ansible.builtin.import_role"
- We can use "ignore_errors: true" in ansible also.
