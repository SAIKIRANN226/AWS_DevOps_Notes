### Session-18
- What are the disadvantages in shellscript ?
- Advantages of ansible over shellscript ?
- Can ansible create instances on external systems like azure, aws, gitlab etc ?
- If so why dont we use ansible to create instances ?
- Because it doesnt have a state file to create instances as terraform does.
- What is configuration management ?
- As a DevOps engineer we need to do this effectively (Basically CRUD over the server)
- What are the application deployment basic steps ?
- What is Idempotence Behaviour in ansible ?
- Create two servers Ansible & Node ?
- Connect to Node server from Ansible server ?
- Create a file in Node from the Ansible server ?
- Install any github session into Node from ansible server ?
- Configuration-server (or) Ansible-server (or) Main-server (or) Controller-machine
- What is PUSH architecture in ansible ?
- What is Pull architecture in ansible ?
- Install ansible in server and connect to Node ?
- Install nginx in Node from Ansible ?
- What is the difference between Commands and Modules ?
- What is the difference between shellscript and ansible playbook ?
- What is the syntax format of ansible playbook ?
- What is Data Transfer Object ?
- Identation is mandatory in yaml format.
- What is Inventory in ansible ?
- Go through the files 01-playbook.yaml & 02-nginx.yaml files in VS ?
- https://github.com/daws-76s/concepts/blob/master/ansible.MD

### Session-19
- Go through the all files in ansible folder in VS

### Session-20 
- Configure roboshop project using ansible ?
- Create all the instances and route53 records using shellscript (roboshop.sh)
- Dont forget to give role to the instance, before creating instances.
- Delete the old records. If exists ---> Hosted zones --> Except NS and SOA.
- In ansible i have used file module, dnf module, user module, get url modules etc.
- sudo tail -f /var/log/messages to check remote connections.

### Session-21
- What is the difference between command and shell ?
- What is UPSERT in shellscript ?
- We created functions in shell to avoid the repetition of the code right ?
- So similarly in ansible also we have Roles.

### Session-22
- How to run the file (or) playbook in the background ?
- You should not run every playbook in the background and why ?
- How to see running logs in the background use "tail -f nohup.out"
- What are ansible roles ?
- How to debug, if you are facing any error in ansible playbook ?
- What are supporting files in project ?
- Is creating every role is mandatory in ansible roles ?
- How to call common role (Any_role) in another role ? "ansible.builtin.import_role"
- How can we ignore errors in ansible ? "ignore_errors: true"

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
