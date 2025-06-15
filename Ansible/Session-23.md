### Ansible.cfg
- It is a configuration file, we can control everything from here, if we enter "ansible --version" in the
  server terminal, we can see from where the configuration file is loading.
- Generally config file will be in "/etc/ansible/ansible.cfg"
- For example create a folder "mkdir test" in CD location.
- Then cd test/ and "cp /etc/ansible/ansible.cfg", then pwd "/home/centos/test"
- Then "export ANSIBLE_CONFIG=/home/centos/anyfolder/ansible.cfg"
- When you do "ansible --version" in any location then you can ansible config file will load from the below
  "/home/centos/test/ansible.cfg" location. Only if you set in "ANSIBLE_CONFIG" and incase you "UNSET" this
  environment variable using "unset ANSIBLE_CONFIG" again it will be loading from the default location that is
  "/etc/ansible/ansible.cfg"
  
Changes can be made and used in a configuration file which will be searched for in the following order
- ANSIBLE_CONFIG (environment variable if set)
- ansible.cfg (in the current directory)
- ~/.ansible.cfg (in the home directory)
- /etc/ansible/ansible.cfg
So instead of giving -i inventory -e user_name -e password to the command, we can put this is ansible.cfg and command usage is "ansible-playbook -e component=mongodb main.yaml"

### Templates in roles
Is a jinja2 format, it is like ansible variable you can submit variable in catalogue.service file moved to the template and given {{MONGODB_HOST}}, so now this has become template, it is same as copy module.

### Handlers in roles
Handlers, for example if a configuration file is changed then we need to restart the nginx,
but what handlers will do is sometimes you want a task to run only when any changes are done in the machine(config_file), for example you may want to restart a service if a task updates the configuration
of that service, but not if the configuration is unchanged, for this we use "notify", why we use this
handlers because some servers will take 2-3 min other servers like nginx will restart in seconds

Tags.yaml is to run a tag ---> ansible-playbook -t devops 16.tags.yaml ---> dint not given hosts because 
it will test from the local host, if you dint mention the tags in the command it will run all tags, so 
where this tags are useful ? for example a new version is going to release for catalogue, so for that we
need to deploy new version, for that we need to stop the service/remove old code/download latest code/
and then restart, here we no need to run all the catalogue script, so create a deployment.yaml file in 
common in tasks folder. Usage: "ansible-playbook -e component=catalogue -t deployment main.yaml"

Points to remember
*******************
1. After all successful components deployments but still you may get erros like categories are not 
   displaying so in this case first "sudo less /var/log/messages" in this session catalogue is unable 
   to connect mongodb so do this "cat /etc/systemd/system/catalogue.service"
