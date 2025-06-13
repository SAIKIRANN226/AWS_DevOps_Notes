### Continuation of the roboshop configuration through ansible
In roboshop.sh ---> There is a "UPSERT" previously it was "Create" now upsert that means if record exist it will edit, if not exist it will create and while running "roboshop.sh" file if you get the error "unable to locate credentials you need to configure credentials by running "aws configure" that means you dint add the role for Ansible-Server instance ---> Actions/Secuirty/ModifyIAM-role/Add your already created role to the ansible-server.

### Command vs shell
- Shell ---> It is like you login inside the server and running the command, env variables and redirections
  symbols will work here.
- Command ---> It is like running command outside the server, env variables and redirections symbols will not
  work here, in command redirections will not work, it will work in shell.

### Points to remember
- First create ansible-server and install ansible in it.
- Run roboshop.sh script to create instances from the ansible-server only.
- Clone the "roboshop-shell" to create the instances from the roboshop.sh script.
- Run the roboshop.sh script.
- Now clone roboshop-ansible project in the ansible-server only.
- Run every module with the ansible command.
- We created functions in the shell to avoid the repetition of the code, so similarly in ansible we have roles.
