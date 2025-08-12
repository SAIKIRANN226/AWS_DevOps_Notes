### Session-12
- Why we use SSH based authentication to connect to github accounts ? and ~ ---> This indicate that you
  are directly landing in users directory "/c/Users/saikiran" in gitbash.
- What is the Port number of SSH ? 22 its a secure connection.
- What is the Algorithm for connecting to github accounts ?
- Command to generate a Key-Pair ? ssh-keygen -f saikiran
- We can add multiple github accounts in config file.
- You can keep your private key in any location, but make sure to give correct location in config file.
- Here the location of private key is created in /c/Users/saikiran and i have given ~ / saikiran.pem, how
  come the location is same ? because when you enter command pwd it will show your current directory when
  you are in "~" location.
- Which one should we prefer while cloning the repo HTTPS (or) SSH ?
- HTTPS is for username and password, SSH is for private key based authentication.
- But prefer HTTPS while clonning the repo.
- Github is nothing but a folder in internet with tracking capabilities.
- What is Shibang in Shellscript (or) Bashscript ?
- If you want git in Visual Studio only, then go to view ---> Terminal ---> Select gitbash
- If you enter wrong URL while pushing to github then we can set using the below command
  "git remote set-url origin <url_of_the_repository>"
- If git is not configured in the github account yet, still developers can start writing their code
  in the VS until git is ready and later they can push it to the git.
- A normal folder will become git, when you initialize by using command "git init"
- How do you capture the output of any linux command in a variable ? using command substitution like this
  DATE=$(date)
- What is the use of arguments in the shellscript ?
- While connecting to external systems like DB, how to hide password while entering in terminal ?
- Is really data-types are important in shellscript ?
- What are arrays in shellscript ? Array index will start from 0,1,2,3.... We have notation for
  "ALL" that is "@" and how many args are passed is "$#"

### Session-13
- Write a condition, if given number is greater than 100 (or) given number is lessthan 100.
- Install mysql, git, postfix, net-tools first using conditions, functions & store logs in tmp.
- Write a loop script to print numbers from 1 to 1000.
- Write a shellscript to install multiple packages using loops ?
- What is root user and exit status ?
- What is function in shellscript ? where we generally keep our functions ? under variables
- There will be NO logs in "less /var/log/messages" we need to store that logs, otherwise we cannot
  troubleshoot, make sure you should not log in the current folder of server come outside and then do.
- What is the purpose of redirection ?
- How to redirect the output ? "yum install nginx -y > output.text" you can keep any name in place of
  output like saikiran.text etc.
- What are special variables in shellscript and it should be in the double qotes ? and what are colour
  coding in shellscript ?
- You should not do any changes (or) adding new files in server terminal, come one step back like after
  going to home folder (cd) like ~ ---> Here you can store the logs for practicing as siva showed in the
  terminal, here in terminal, if you get any errors (or) not working properly you can delete that folder
  and clone again from the github (NO problem)
- How to remove package in shellscript ? "sudo dnf remove <package_name> -y" (or)
- sudo yum remove <package_name> -y 
- How do you handle the errors in shellscript ? using a special variable called exit-status "$?"
- What is the disadvantage in shellscript ? Even if shellscript faces error, it wont stop, it is our
  responsibility to check the errors by writing conditions and exit-status a special variable "$?"
  
### Session-14 
- Write a shellscript to install multiple packages using loop, like giving args outside the script ?
- Configure the Roboshop project using shellscript ?
- What is SED in shellscript ? If i want permanent change (sed -i) and temperory change (sed -e) ?
- Where this SED is used in shellscript ? to change the configuration (or) like giving remote access to
  other servers in shellscript.
- How to check logs in shellscript ? "sudo less /var/log/messages"
- Command to check remote connections ? netstat -lntp
- Shellscript is keeping all individual Linux commands in one file, instead of one by one commands, which
  was done while configuring the project manually.
- yum list installed git (or) yum list installed | grep <package_name>
- Can we set $? (Exit status) to automatically exit in shellscript ?
- Instead of giving &>> $LOGFILE everywhere, we can give "exec &>$LOGFILE" under logfile name and and why
  we dont prefer this.
- What is the use of logs ? why we check logs ? trouble shooting will be easy and we can check wether the
  remote connections are successful or not.

### Session-15
- How do we set to exit automatically when shellscript faces errors ?
- Does really "set -e" helpful in exiting the shellscript when it faces error ?
- How do you store logs in shellscript ?
- Where to check the logs wether the remote connections are successfully connected (or) not ?
- Command to check logs ---> "sudo less /var/log/messages"
- unzip -o /tmp/web.zip ---> Here "o" is to overwrite, if you run the script multiple times.
- mkdir -p /app ---> Here -p means if folder exists, it will not create.
- Dont forget to restart nginx after changing in configuration file.
- Make sure to add all private servers in the web cofiguration
  
### Session-16
- Write a shellscript to delete old logfiles which are morethan 14 days old ?
- What is the use of IFS (Internal field separator) ?
- Write a shellscript to read a file which is in /etc/passwd using IFS ?
- What is the algorithm for deleting old log files ?
- Check Disk Usage and Send email for alerts ?
- How do you create files with old date in server ?
- Command to find old logfiles morethan 14 days old with .log extensions only ?
- Command to check information about total space and available space on a file system ?
- How to create a new volume (or) disk in aws console and what is the condition for that ?
- What are the commands to make disk into usage ?
- How do we find different types of file systems ? using reverse search.
- How do you mail the above disk usage from linux server ?
- We will configure the company mail server details to send email alerts.
- Sometimes mailing is not in our control, linux admin team will configure in mail.sh to use.
- How to go all the way to down in config file ?
- How to go all the way to top in config file ?
- Creating disk is the work of "Storage team" not DevOps. But just know how it works.
- If websites are down, then monitoring team will send alerts to Developers team.
- If servers are down, then monitoring team will send alerts to DevOps team.

### Session-17
- What is crontab and why it is useful ?
- Usage of crontab and giving the script location ?
- How to see logs of a crontab ? tail -f /var/log/cron
- What is Optargs in shellscript ?
- How to set any shellscript as Native Linux Command ?
- Automating the creation of aws instances and route53 records using aws CLI ?
- What are Roles to Resources ?
- How to create a role for ec2 in aws console ?
- How will you asign above role to the ec2 in aws console ?
- Remove old credentials which was created for aws console in .aws folder by using rm -rf
- Command to create instances with tags ?
- Command to list instances and find the one with your specific Name tag ?
- Command to terminate the instances ?
- How do you create administrator user in aws console ?
- How do you configure aws ?
- Why we created roles in IAM ?
- Write a shellscript to create all instances and route53 records using aws CLI ?
- What is UPSERT in shellscript ?
