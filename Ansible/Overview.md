### Session-18
- Another name of ansible is Configuration-server (or) Ansible-server (or) Main-server (or) Controller
  machine.
- What are the disadvantages in shellscript ? L, S, E, R, E, S, R, E
- What are the advantages of ansible over shellscript ? O, C, A, C, O
- Can ansible create instances on external systems like azure, aws, gitlab etc ? YES! But it is not
  recommended, because ansible is only intended for configuration management & application deployment.
- If so why dont we use ansible to create instances ? Because it doesnt have a state file to create instances
  as terraform does. So thats why terraform is best for creation of infrastructure.
- What is configuration management in general ?
- As a DevOps engineer we need to do this effectively (Basically CRUD over the server)
- What are the application deployment basic steps ?
- What is Idempotence Behaviour in ansible ?
- Create two servers Ansible & Node ?
- Connect to Node server from Ansible server ? "sshpass -p DevOps321 ssh centos@NodeIP"
- Create a file in Node from the Ansible server ? "sshpass -p DevOps321 ssh centos@NodeIP -C "echo Hello
  saikiran how are you > /tmp/sai.txt"
- Install any github session into Node from ansible server ? "sshpass -p DevOps321 ssh centos@NodeIP -C "curl
  <paste_the_RAW_URL> | sudo bash" (or) For example if you want to just see all the content of your session in
  the terminal only, then use "curl <paste_the_RAW_URL>" just enter without double qotes. Curl command will
  not download the file, instead it will show the content on the terminal.
- But to download the file use "wget <paste_the_RAW_URL>"
- What is PUSH architecture in ansible ?
- What is PULL architecture in ansible ?
- Install ansible in ansible-server and connect to Node ? make sure connection is success ? "ansible -i
  NodeIP, all -e ansible_user=centos -e ansible_password=DevOps321 -m ping"
- Install nginx in Node from Ansible ? ansible -i 34.203.214.64, all -e ansible_user=centos -e
  ansible_password=DevOps321 --become -m yum/service -a "name=nginx state=present/started/stopped"
- What is the difference between Commands and Modules ?
- What is the difference between Shellscript and Ansible-playbook ?
- YAML is the markup language used in ansible. Identation is mandatory in yaml format.
- What is Inventory in ansible ? Nothing but a list of hosts (servers) where Ansible will run its automation
  tasks on these servers. It’s basically your address book for servers — telling Ansible what machines exist,
  how to connect to them, and how they’re grouped.
- Go through the all files in "Ansible" folder in VS.
- https://github.com/daws-76s/concepts/blob/master/ansible.MD

### Session-19
- Go through the all files in Ansible folder in VS
- Make sure to install ansible in ansible server by "sudo yum install ansible -y" then only it becomes
  ansible server.
- ansible-playbook -i inventory.ini -e ansible_user=centos -e ansible_password=DevOps321 <playbook>
- ansible.builtin.ping ---> Its a ping module.
- ansible.builtin.package ---> Its a package module.
- ansible.builtin.service ---> Its a service module.
- ansible.builtin.debug ---> This module is used to print whatever you give.
- ansible.builtin.command ---> Used to run command on a remote machine directly without using shell.
- We have variables in ansible play-level, task-level, var_files, vars_prompt, inventory.ini, args
- Variable preference in ansible ? CMD, Task, File, Prompt, Play, Inventory.ini, Ansible roles.
- What are data-types in ansible ?
- What are conditions in ansible ? write a condition for roboshop user exist or not ?
- Similar to "$?" in shell, we have "rc" in ansible to check exit status of the previous command.
- Write ansible-playbook to loop Ramesh, Suresh, Saikiran, Mahesh.
- Write ansible-playbook to install nginx, mysql, postfix, net-tools using loop.
- Write ansible-playbook to install nginx, mysql, postfix, net-tools and also loop "name and state"
- What are tags in ansible ? In the server, if you want a particular task then you can use tags below.
- ansible-playbook -t devops 16-tags.yaml ; ansible-playbook -t aws 16-tags.yaml
- When we can use tags ? For example take a catalogue component, if there is any new version of catalogue,
  what will you do basically ? we do new deployment/new release right ? by using basic deployment steps.
  Command will be ---> ansible-playbook -e component=catalogue -t deployment main.yaml

### Session-20 
- Configure roboshop project using ansible ? go through "Roboshop-ansible" in VS.
- Create all the instances and route53 records using shellscript (roboshop.sh)
- Dont forget to give role to the ansible instance, before creating instances and route53 records.
- Delete the old records if exists ---> Hosted zones --> Except NS and SOA.
- In ansible i have used file module, dnf module, user module, get url modules etc.
- How to check remote connections ? sudo tail -f /var/log/messages.
- &>> /dev/null ---> It is called black hole. Output stored here will be discarded.

### Session-21
- What is "UPSERT" in roboshop.sh file in "Roboshop-shellscript" ? previously it was "CREATE" now "UPSERT".
- What is the difference between Command and Shell ?
- Shell ---> It is like you login inside the server and run the command, Environment variables and
  redirections (Symbols) will work here.
- Command ---> It is like running the command outside the server, Environment variables and redirections
  (Symbols) will not work here.
- We used functions in shellscript to avoid the repetition of the code right ? So similarly in ansible also
  we have Ansible Roles.

### Session-22
- How to run the file (or) playbook in the background ? "nohup ansible-playbook -i inventory.ini -e
  ansible_user=centos -e ansible_password=DevOps321 mongodb.yaml & >> /dev/null"
- Output will be in nohup.out, it will not come in the terminal, if it is a small instance, we can't run
  every script in the background, because memory consumption will be high, so you can run only few scripts
  in the background.
- How to see running logs in the background use "tail -f nohup.out"
- What are ansible roles ? It is a dry principle, dont repeat yourself like we have used functions in
  shellscript to avoid the repetition of the code. It is a proper directory structure to keep our
  configuration and we can share this with other users also.
- Ansible roles ---> Again in common role, we have tasks, handlers, templates, files, vars, defaults, meta,
  library, lookup_plugins.
- How to debug, if you are facing any error in ansible playbook ? "ansible-playbook -vvv -i inventory.ini -e
  ansible_user=centos -e ansible_password=DevOps321 -e component=mongodb main.yaml" we will get the full
  information in the terminal, which is happening in the background, so that we can see where is the error.
- What are supporting files in project ? like mongodb.repo, catalogue.service, roboshop.conf etc.
- Is creating every role is mandatory in ansible roles ? NO! we create what we require.
- How to call common role (any role) in another role ? "ansible.builtin.import_role"
- How can we ignore errors in ansible ? using "ignore_errors: true"

### Session-23
- What is "ansible.cfg" file ? It is ansible main configuration file, we can control options from here.
- How to see from where config file is loading in server ? "ansible --version"
- What is the default location of config file ? "/etc/ansible/ansible.cfg"
- For example create a folder "mkdir test" in CD location.
- Then cd test/ and "cp /etc/ansible/ansible.cfg ." then pwd will be "/home/centos/test"
- Then "export ANSIBLE_CONFIG=/home/centos/test/ansible.cfg" nothing but i have given first preference.
- When you do "ansible --version" in any location, then you can see ansible_config file is loading from the
  "/home/centos/test/ansible.cfg" location. Only if you set environment variable for "ANSIBLE_CONFIG" and
  incase if you "UNSET" this environment variable using "unset ANSIBLE_CONFIG", now it will be loading from
  the default location that is "/etc/ansible/ansible.cfg"
- We have many options in "ansible configuration settings" file nothing but "ansible.cfg". We may not use all
  the options, we only use what we require like inventory_path, ask_vault, timeout, user_name, passwords etc.
- What are the preferences of loading ansible.cfg file ?
- So instead of giving -i inventory -e ansible_user=centos -e ansible_password=DevOps321 to the command, we
  can put this is in ansible.cfg & command usage is "ansible-playbook -e component=mongodb main.yaml"
- Templates is nothing but a place holders, where we will submit our required values at the run time and it
  is a Jinja2 format and extension is .j2, go through the code in VS. Like we have used for catalogue.service
  files.
- What are Handlers in ansible roles ?
- What is the Usage of tags in ansible ? If you want to run a particular task, then we use Tags.
- How to create a full config file ? "ansible-config init --disabled > ansible.cfg"
  
### Session-24
- Till now where we have given our usernames and passwords ? Command line (or) ansible.cfg file
- What is ansible-vault and what is the purpose ? Storing secrets like keys and passwords etc.
- Difference between encoding and encryption ?
- Ansible uses mathematic algorithm (AES256) to encrypt the vault.
- How to create ansible-vault in ansible-server ? Below are the steps.
- Practice folder (Your working directory)
- Create "vault" folder inside the Practice folder, if we create vault folder in VS (Windows), it will not
  reflect in the server, so you need to create in linux server only. Same for "group_vars" folder.
- Next create "group_vars" folder inside the vault folder then.
- Create "vault-file" inside the group_vars folder using below command.
- ansible-vault create Practice/vault/group_vars/some_name.yaml, keep your username and password in this
  file using "ansible-vault edit group_vars/saikiran.yaml" ansible_user: centos ; ansible_password: DevOps321
  and save it :wq!
- Also create ansible.cfg, inventory.ini & your playbook files (Inside the Practice folder not in vault or
  group_vars folders)
- Put "ask_vault_pass=True" in ansible.cfg (or) "ansible-playbook saikiran.yaml --ask-vault-pass"
- How to connect to the instance ? "ansible-playbook saikiran.yaml" since we have inventory in separate
  file and username/password are kept in vault.
- Since our whole infra is in SSM Parameter in AWS systems manager, this is also a vault from AWS, but we
  integrate ansible-vault with the SSM Parameter and we fetch the values from AWS instead of depending on
  ansible-vault and ansible-vault commands and all those things etc.
- What is Dynamic Inventory in ansible ? What is auto-scaling of servers ?
- For example we have 10 servers now because of traffic and i need to run (or) manage these servers using
  ansible-playbooks. Till now we targeted only single server using ansible, but we never targeted multiple
  servers at a time.
- When auto-scaling is created, ansible will connect to AWS to fetch the IP_addresses of the newly created
  servers (Using auto-scaling). How ansible will fetch IP_addresses dynamically ? we have a plugin called
  "aws ec2 inventory"
- For example, If you want to run update to the all the web instances then "ansible-instance" should connect
  to AWS and fetch instances with the Name "web" which are present in us-east-1 region. We use "aws ec2
  inventory" plugin. Go through the "web.aws_ec2.yaml" file in the VS. 
- You can keep any name like "saikiran.aws_ec2.yaml" but file must end with ".aws_ec2.yaml"
- Syntax of the above plugin is below, you can search in google.
  
        plugin: amazon.aws.aws_ec2
        regions:
        - us-east-1
        filters:
        tag:Name:         
        - web
  
- Here tag:Name ---> Is same as what we see Instances section in aws, there we have Name, Instance ID,
  Instance state, Instance type etc. So first is we want Name.
- Paste the above syntax in "web.aws_ec2.yaml" in server in CD location using "vim web.aws_ec2.yaml"
- Make sure to install "botocore and boto3" then only plugins will work.
- To install botocore and boto3 using python, we use "pip"
- First know which version of python is using in ansible ? "ansible --version" pip should also be the same
  version of python.
- So "sudo yum list | grep pip"
- "sudo yum install python3.11-pip.noarch -y" (Select from the above list)
- Now install "pip3.11 install boto3 botocore"
- "ansible-inventory -i web.aws_ec2.yaml --list" now it will fetch the instances with name "web"
- Ansible fetched all the web-instances right ? Now if you want to connect to this web instances.
  "ansible aws_ec2 -i web.aws_ec2.yaml -e ansible_user=centos -e ansible_password=DevOps321 -m ping" then web
  instances will give us replay "pong"
- What is Plug and Play ? If your ansible-server wants to connect to the external systems like aws, azure, gcp
  or alibaba etc. Then we need to add some plug (Of aws, azure, gcp or alibaba) thats what we call plug,
  similarly if ansible have aws plugin to connect to aws ec2, then we can fetch IP_addresses. That is nothing
  but "AWS Dynamic inventory plugin"
- We use ansible.cfg file to minimize the commands (or) arguments to the script in server.
- Use "ansible-vault encrypt group_vars/<some_name>.yaml" If already has existing vault.
- If you want to edit the existing vault ---> "ansible-vault edit web.yaml"
- If you want to know wether it is encrypted or not ? then "cat group_vars/<some_name>.yaml"
- If you want to see your credentials, then "ansible-vault view group_vars/<some_name>.yaml"
- You can use ansible-vault anywhere in the roboshop project for any components you want.
- Earlier we used Ansible-vault & recently we migrated to AWS SSM Parameter, since our entire infra is in
  AWS. We integrated ansible-vault with SSM Parameter to fetch the values directly from the AWS. Which
  is a seamless integration instead of depending ansible-vault and ansible-vault commands.
