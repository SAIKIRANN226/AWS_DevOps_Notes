### Why we use SSH authentication ?
We want to connect to the github account to push the code right ? and we used SSH based auth, Because we work with multiple github accounts, so for every account logging with username and password is not a good practice, so we prefer to use "ssh based authentication".
- Generate a new key-pair (or) use existing key-pair, "ssh-keygen -f <file-name>" press enter two times,
  Public-key will be with .pub extension, you need to give .pem extension manually for Private-key, To enable
  extension go to "file explorer options" in control panel/view/unhide extensions for known file types.
- Cat Public-key, copy the code and go to the github settings /SSH and GPG Keys/New SSH key/give any name and
  paste without any gaps.
- Keep your Private-key in ".ssh" folder, if it is not created you have to create it in user directory like
  "C:\Users\saikiran\.ssh"
- Create a config file with no extension in .ssh folder, in this config file keep the config syntax and give
  the correct location of your Private-key and also we can add multiple github accounts here. Below is the
  config syntax i have given for my created Private-key.
  
                Host github.com
                  HostName github.com
                  User git
                  PreferredAuthentications publickey
                  IdentityFile ~/saikiran.pem
  
- We have HTTPS and SSH to the repository, we use ssh authentication for pushing to the github.
  1. HTTPS ---> Username and Password, clone https URL when you have read only access.
  2. SSH ---> Just Private-key, you can clone if you are the owner of the respository. Prefer HTTPS while
     cloning the repository.
- Github is nothing but a folder in internet with tracking capabilities.
- git branch -M main ---> To change from master to main (or) main to master
- Learn Dzone git commands from the below URL's
   https://dzone.com/articles/top-20-git-commands-with-examples
   https://dzone.com/articles/top-35-git-commands-with-examples-and-bonus
- git add . ; git commit -m "proper message" ; git push -u origin master

### Shellscript is also known as Bashscript
- #!/bin/bash ----> This we call it as "shibang" it is the first line to check the syntax of the shellscript,
  we need to give the location of bash which is in "/bin/bash" but we write first line as "#!/bin/bash" apart
  from the first line, If you see "#" anywhere it is commentout.
- If you want git in visual studio only then go to view ---> Terminal ---> Select gitbash
- If you enter wrong URL while pushing to github then we can set using below command
  "git remote set-url origin <url_of_the_repository>"
- If git is not configured in the github account yet, still developers can start writing their code in the VS
  until git is ready and later they can push it to the git.
- A normal folder will become git when you initialize by using command "git init"
- We develop code (or) script in VisualStudio.
- Using gitbash client we push the code (or) script to the github repository.
- Create a t2.micro server in AWS.
- git clone <URL> in the server ---> Because we are cloning for the first time and go to your script location
  then "sh <script-name>" , git pull ---> If you want only changes.
- echo is only used for printing purpose

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
  folder, If it is not there you need to create .ssh folder, It will be hidden so to check this, enter the
  following command "ls -la".
