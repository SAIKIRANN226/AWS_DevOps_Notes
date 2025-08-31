### Session-18
- Ansible-server (or) Configuration-server (or) Main-server (or) Controller machine.
- What are the disadvantages in shellscript ? L, S, E, R, E, S
- What are the advantages of ansible over shellscript ? O, C, A, C, O, R, P
- Can ansible create instances on external systems like azure, aws, gitlab etc ? YES! But it is not recommended, because ansible is only intended for configuration management & application deployment.
- If so why dont we use ansible to create instances ? Because it does not have a state file to create instances as terraform does. So thats why terraform is best for creation of infrastructure only.
- What is configuration management in general and in ansible ?
- As a DevOps engineer we need to do CRUD over the server effectively.
- What are the application deployment basic steps ?
- What is Idempotence Behaviour in ansible ?
- Create two servers Ansible & Node ?
- Connect to Node server from Ansible server ? "sshpass -p DevOps321 ssh centos@NodeIP"
- Create a file in Node from the Ansible server ? "sshpass -p DevOps321 ssh centos@NodeIP -C "echo Hello saikiran how are you > /tmp/sai.txt"
- Install any github session into Node from ansible server ? "sshpass -p DevOps321 ssh centos@NodeIP -C "curl <paste_the_RAW_URL> | sudo bash"
- To show the file content in the terminal just use "curl <paste_the_RAW_URL> or <normal_url>"
- Curl command will not download the file, instead it will show the content on the terminal.
- To download the file just use "wget <paste_the_RAW_URL> or <normal_url>"
- What is PUSH (Ansible) architecture in ansible ? Agent less
- What is PULL (Chef) architecture in ansible, how do you configure PULL ? Install Agents
- Install ansible in ansible-server & connect to Node ? "ansible -i NodeIP, all -e ansible_user=centos -e ansible_password=DevOps321 -m ping" Hence connection is success between Ansible and Node.
- Install nginx in Node from Ansible ? "ansible -i NodeIP, all -e ansible_user=centos -e ansible_password=DevOps321 --become -m yum/service -a "name=nginx state=present/started/stopped"
- What is the difference between Shell commands and Ansible modules ?
- What is the difference between Shellscript and Ansible-playbook ?
- YAML is the markup language used in ansible. Identation is mandatory in yaml format.
- What is Inventory in ansible ? Nothing but a list of hosts (Servers) where Ansible will run its automation tasks on these servers. It’s basically your address book for servers — telling Ansible what machines exist, how to connect to them and how they’re grouped.
- Go through all the files in "Ansible" folder in VS.
- https://github.com/daws-76s/concepts/blob/master/ansible.MD

### Session-19
- Ansible-Server ---> "sudo yum install ansible -y" then only it becomes ansible server.
- ansible-playbook -i inventory.ini -e ansible_user=centos -e ansible_password=DevOps321 <playbook>
- ansible.builtin.ping ---> Its a ping module.
- ansible.builtin.package ---> Its a package module.
- ansible.builtin.service ---> Its a service module.
- ansible.builtin.debug ---> This module prints whatever you give.
- ansible.builtin.command ---> Used to run command on a remote machine directly without using shell.
- We have variables in ansible play-level, task-level, var_files, vars_prompt, inventory.ini, args.
- Variable preference in ansible ? CMD, Task, File, Prompt, Play, Inventory.ini, Ansible roles.
- What are Data-types in ansible ? We have Skills (List type) and Experience (Map type)
- What are conditions in ansible ? Write a condition for roboshop user exist or not ?
- Similar to $? in shell, we have "rc" in ansible to check the exit status of the previous command.
- Write ansible-playbook to loop Ramesh, Suresh, Saikiran, Mahesh.
- Write ansible-playbook to install nginx, mysql, postfix, net-tools using loop.
- Write ansible-playbook to install nginx, mysql, postfix, net-tools & also loop "name & state"
- What are tags in ansible ? Tags are used in server, if you want a particular task to run.
- ansible-playbook -t devops 16-tags.yaml ; ansible-playbook -t aws 16-tags.yaml
- When we can use tags ? For example take catalogue component, if there is any new version of catalogue, what will you do basically ? We do new deployment (or) new release right ? By using basic deployment steps. Command will be ---> ansible-playbook -e component=catalogue -t deployment main.yaml

### Session-20 
- Configure Roboshop Project using ansible ? Go through the "Roboshop-ansible" in VS.
- Create all the instances & route53 records using shellscript (roboshop.sh) script.
- Dont forget to give role to the ansible instance, before creating instances & route53 records.
- Delete the old records if exists ---> Hosted zones --> Except NS and SOA.
- In ansible we have used file module, dnf module, user module, get url modules etc.
- How to check remote connections (or) running logs ? sudo tail -f /var/log/messages.
- Black Hole ---> &>> /dev/null (Output stored here will be discarded)
- All the Users informations will be there in "cat /etc/passwd" in server.

### Session-21
- What is "UPSERT" in roboshop.sh file in "Roboshop-shellscript" ? Previously it was "CREATE" now "UPSERT".
- What is the difference between Command and Shell ?
- Shell ---> It is like you login inside the server and run the command, Environment variables and redirections (Symbols) will work here.
- Command ---> It is like running the command outside the server, Environment variables and redirections (Symbols) will not work here.
- We used functions in shellscript to avoid the repetition of the code right ? So similarly in ansible also we have Ansible Roles.

### Session-22
- We have a special file in linux called a "Black Hole" located at /dev/null. Any data written to it is immediately discarded (Vanishes). "& >> /dev/null" Here & → runs in background, >> /dev/null → discards output.
- How to run a file (or) playbook in background ? "nohup ansible-playbook -i inventory.ini -e ansible_user=centos -e ansible_password=DevOps321 mongodb.yaml & >> /dev/null"
- Output will be in "nohup.out" it will not come in terminal. We cannot run every script in background because of memory consumption, you can only run few scripts (or) a small instance in background.
- How to see running logs in the background ? "tail -f nohup.out"
- What are ansible roles ? It is a dry principle, dont repeat yourself like we have used functions in shellscript to avoid the repetition of code. It is a proper directory structure to keep our configuration & we can share this with other users also.
- Ansible roles ---> Common is also a role, we have tasks, handlers, templates, files, vars, defaults, meta, library, lookup_plugins.
- How to debug, if you are facing any error in ansible playbook ? "ansible-playbook -vvv -i inventory.ini -e ansible_user=centos -e ansible_password=DevOps321 -e component=mongodb main.yaml" We will get the full information on terminal, what is happening in background, so that we can see where is the error.
- What are the supporting files in project ? Like mongodb.repo, catalogue.service, roboshop.conf etc.
- Creating every role is not mandatory, we create what we require.
- How to call common role (Any role) in another role ? "ansible.builtin.import_role"
- How can we ignore errors in ansible ? Using "ignore_errors: true"

### Session-23
- What is "ansible.cfg" file ? It is ansible main configuration file, we can control options from here.
- How to see from where the config file is loading in ansible server ? "ansible --version"
- What is the default location of config file ? "/etc/ansible/ansible.cfg"
- For example create a test folder in CD location "mkdir test"
- Then cd test/ and "cp /etc/ansible/ansible.cfg ." then pwd will be "/home/centos/test"
- Then "export ANSIBLE_CONFIG=/home/centos/test/ansible.cfg" nothing but i have given first preference.
- When you test "ansible --version" in any location, then you can see ansible config file is loading from the "/home/centos/test/ansible.cfg" location. Only if you set environment variable for "ANSIBLE_CONFIG" and incase if you "UNSET" this environment variable using "unset ANSIBLE_CONFIG" now it will be loading from the default location that is "/etc/ansible/ansible.cfg"
- There are many options in ansible.cfg file (Ansible configuration settings) we may not use all the options, we only use what is required like inventory_path, ask_vault, timeout, user_name, passwords etc.
- What are the preferences of loading ansible.cfg file ?
- Instead of giving "ansible-playbook -i inventory -e ansible_user=centos -e ansible_password=DevOps321 -e component=mongodb main.yaml" We can keep -i inventory as a separate file and keep your username and password in ansible.cfg, then command usage is "ansible-playbook -e component=mongodb main.yaml"
- Templates is nothing but a place holders, where we will submit our required values at the run time and it is a Jinja2 format and extension is .j2, go through the code in VS. Like we have used for catalogue.service files.
- What are Handlers in ansible roles and why we use ?
- What is the Usage of tags in ansible ? If you want to run a particular task, then we use Tags.
- How to create a full config file ? "ansible-config init --disabled > ansible.cfg" Here disabled means by default all options are commented, you can uncomment which ever options you want to use.
  
### Session-24
