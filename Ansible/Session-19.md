### Go through the below files
- 03.multi-play.yaml
- 04.variables.yaml 
- 05.variables-task.yaml
- 06.variables-from-files.yaml
- 07.variables-from promt.yaml
- 08.vars-from-inventory.yaml
- 09.vars-from-Args.yaml
- 10.var.preference.yaml
- 11.datatypes.yaml
- 12.conditions.yaml
- 13.loops.yaml
- 14.loops.yaml
- 15.loops.yaml
- 16.tags.yaml

### Points to remember
- Create 2 servers, for example below.
- Ansible server make sure to install ansible in the server by "sudo yum install ansible -y" then it becomes
  ansible server.
- Node server ---> Watch the 03.multi-play.yaml in VS.
- Then gitbash, pull in server and execute by following command.
- ansible-playbook -i inventory.ini -e ansible_user=centos -e ansible_password=DevOps321
  <playbook-name>
