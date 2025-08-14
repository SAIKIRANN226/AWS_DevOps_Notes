### Session-18
- Another name of ansible is Configuration-server (or) Ansible-server (or) Main-server (or) Controller machine.
- What are the disadvantages in shellscript ? L, S, E, R, E, S
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
  tasks. It’s basically your address book for servers — telling Ansible what machines exist, how to connect to
  them, and how they’re grouped.
- Go through the all files in "Ansible" folder in VS.
- https://github.com/daws-76s/concepts/blob/master/ansible.MD

### Session-19
- Go through the all files in ansible folder in VS
- Make sure to install ansible in the Ansible-Server by "sudo yum install ansible -y" then it becomes
  ansible server.
- ansible-playbook -i inventory.ini -e ansible_user=centos -e ansible_password=DevOps321 <playbook_name>

### Session-20 
- Configure roboshop project using ansible ?
- Create all the instances and route53 records using shellscript (roboshop.sh)
- Dont forget to give role to the ansible instance, before creating instances.
- Delete the old records. If exists ---> Hosted zones --> Except NS and SOA.
- In ansible i have used file module, dnf module, user module, get url modules etc.
- sudo tail -f /var/log/messages to check remote connections.

### Session-21
- What is UPSERT in shellscript ? previously it was "CREATE" now UPSERT.
- What is the difference between command and shell ?
- Shell ---> It is like you login inside the server and running the command, env variables and redirections
  symbols will work here.
- Command ---> It is like running the command outside the server, env variables and redirections symbols
  will not work here.
- We created functions in shell to avoid the repetition of the code right ? So similarly in ansible also
  we have Roles.

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
- How to debug, if you are facing any error in ansible playbook ? "ansible-playbook -vvv -i inventory.ini -e
  ansible_user=centos -e ansible_password=DevOps321 -e component=mongodb main.yaml" we will get the full
  information in the terminal, which is happening in the background, so that we can see where is the error.
- What are supporting files in project ? like mongo.repo, catalogue.service, roboshop.conf etc.
- Is creating every role is mandatory in ansible roles ? NO! we create what we require.
- How to call common role (any role) in another role ? "ansible.builtin.import_role"
- How can we ignore errors in ansible ? using "ignore_errors: true"

### Session-23
- What is "ansible.cfg" file ? it is main configuration file.
- How to see from where config file is loading in server ? ansible --version
- What is the default location of config file ? "/etc/ansible/ansible.cfg"
- What are the preferences of loading ansible.cfg file ?
- How to set config file and how to UNSET config file ?

### Session-24
- Till now where we have given our Usernames and Passwords ?
- What is ansible vault ? what does it do ?
- Difference between Encoding and Encryption ?
- How to create ansible vault in ansible-server ?
