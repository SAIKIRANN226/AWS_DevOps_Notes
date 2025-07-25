### Why we use SSH based authentication to connect to Github account ?
To push our developed code from VS to Github account using gitbash client, we use SSH based authentication. Because we work with multiple github accounts, so for every account logging with username and password is not a good practice, so we prefer to use "SSH based authentication" since SSH(22) is more secure.

- First generate a new key-pair (or) use existing key-pair, "ssh-keygen -f <file_name>" press enter two times,   Public-Key will be with .pub extension, you need to give .pem extension manually for Private-Key. To enable
  extension go to the "File Explorer Options" in control_panel/view/unhide_extensions for known file types.
- Cat Public-Key, copy the code and go to the github_settings/SSH_and_GPG_Keys/New_SSH_key/give_any_name and
  paste without any gaps.
- Keep your Private-Key in ".ssh" folder, if it is not there you have to manually create the .ssh folder in
  user directory "C:/Users/saikiran/.ssh"
- Create a config_file with NO extension in .ssh folder, in this config file keep the config_syntax and give
  the correct location of your Private-Key and also we can add multiple github accounts here. Below is the
  config syntax i have given for my created Private-Key.
  
                    Host github.com
                      HostName github.com
                      User git
                      PreferredAuthentications publickey
                      IdentityFile ~/saikiran.pem
  
- We have HTTPS and SSH to the repository.
- HTTPS ---> Username and Password, clone https URL when you have read only access.
- SSH ---> Just Private-Key, you can clone if you are the owner of the respository. Prefer HTTPS while cloning
  the repository.
- Github is nothing but a folder in internet with tracking capabilities.
- git branch -M main ---> To change from master to main (or) main to master
- Learn Dzone git commands from the below URL's
- https://dzone.com/articles/top-20-git-commands-with-examples
- https://dzone.com/articles/top-35-git-commands-with-examples-and-bonus
- git add . ; git commit -m "proper message" ; git push -u origin master

### Shellscript is also known as Bashscript
- #!/bin/bash ----> This we call it as "shibang" it is the first line to check the syntax of the shellscript,
  we need to give the location of bash, which is in "/bin/bash" but we write first line as "#!/bin/bash" apart
  from the first line, if you see "#" anywhere, it is commentout.
- If you want git in visual studio only then go to view ---> Terminal ---> Select gitbash
- If you enter wrong URL while pushing to github then we can set using the below command.
  "git remote set-url origin <url_of_the_repository>"
- If git is not configured in the github account yet, still developers can start writing their code in the VS
  until git is ready and later they can push it to the git.
- A normal folder will become git, when you initialize by using command "git init"
- We develop code (or) script in VisualStudio.
- Using gitbash client, we push the code (or) script to the github repository.
- Create a t2.micro server in AWS.
- Git clone <URL> in the server. Because we are cloning for the first time and go to your script location
  then "sh <script_name>" , git pull ---> If you want only changes.
- Echo is only used for printing purpose.

### Go through the below scripts in VS
- 01-hello-world.sh
- 02-variables.sh
- 03-variables.sh
- 04-variables.sh
- 05-variables.sh
- 06-data-types.sh
- 07-arrays.sh

### Points to remember
- If you make any changes in the code in VS and if you save that changes by pressing ctrl+S, then colour will
  change to yellow. So to make normal then you must push the code to the github account.
- In linux when you open gitbash we are automatically landing in the home directory to know that just type
  "pwd" then you can see your landed location "/c/users/user(saikiran), Here definitely you will have ".ssh"
  folder, if it is not there you need to create .ssh folder, It will be hidden, so to check this, enter this
  command "ls -la"
- How to shift from main-master (or) master-main branch ? "git branch -M main"
- If you want to create a folder in github with .md extension, just use '/' after naming your folder and after
  '/' just create a file with .md extension. Example 'AWS_DevOps_Notes(Repo)/Shellscript/Session-01.md'
