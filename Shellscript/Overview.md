### Session-12
- Why we use SSH based authentication to connect to github accounts ? and ~ ---> This indicate that you are directly landing in users directory "/c/Users/saikiran" in gitbash.
- What is the Port number of SSH ? 22 its a secure connection.
- What is the Algorithm for connecting to github accounts ?
- Command to generate a Key-Pair ? "ssh-keygen -f saikiran"
- We can add multiple github accounts in config file.
- You can keep your private key in any location but make sure to give correct location of your Private key in config file.
- Here the location of private key is created in /c/Users/saikiran and i have given ~ / saikiran.pem, how come the location is same ? because when you enter command "pwd" it will show your current directory when you are in "~" location.
- Which one should we prefer while cloning the repo HTTPS (or) SSH ?
- HTTPS is for Username & Password, while SSH is used for Private key based authentication. But prefer HTTPS while cloning any repository from github.
- Github is nothing but just a folder in internet with tracking capabilities.
- What is Shibang in Shellscript (or) Bashscript ? #!/bin/bash
- If you want git in Visual Studio only, then go to view ---> Terminal ---> Select gitbash.
- If you enter wrong URL while pushing to github "git remote set-url origin <url_of_the_repository>"
- If git is not configured in the github account yet, still developers can start writing their code in VS until git is ready and later they can push it to the git.
- A normal folder will become git, when you initialize "git init"
- How do you capture the output of any linux command into a variable ? using command substitution like this DATE=$(date) ; ID=$(id -u) etc.
- What is the use of arguments in the shellscript ? $1, $2, $3... $N, $@, $#
- While connecting to external systems like DB, how to hide password while entering in terminal ?
- Is really Data-types are important in shellscript ? NO!
- What is arrays in shellscript ? Array index will start from 0,1,2,3.... We have notation for "ALL" that is "@" and how many args are passed is "#"
- Write a shellscript of array using FRUITS example ?

### Session-13
- Write a shellscript using condition, if given number is greater than 100, given number is lessthan 100.
- Install mysql, git, postfix, net-tools first using conditions, functions & store logs in tmp.
- Write a loop script to print numbers from 1 to 1000 ?
- Write a shellscript to install multiple packages using loops ?
- What is root user and exit status ? id=0, (id -u), $?
- What is function in shellscript ? We generally keep our functions under variables.
- There will be NO logs in "less /var/log/messages" we need to store that logs, otherwise we cannot troubleshoot, but the best practice is to keep a separate log file for applications and only push critical events to /var/log/messages. Make sure you should not log in the current folder of server come outside and then do.
- What is the purpose of redirection ? Nothing but storing the output in our required folder.
- How to redirect the output ? "yum install nginx -y > output.text" you can keep any name in place of output like saikiran.text etc.
- What are special variables in shellscript and they should be in double qotes and how do you use the colour coding in shellscript ?
- You should not do any changes (or) adding new files in server terminal, come one step back like after going to home folder (cd) like ~ ---> Here you can store the logs for practicing as siva showed in the terminal, here in terminal, if you get any errors (or) not working properly you can delete that folder and clone again from the github (NO problem).
- Sudo dnf remove <package_name> -y (or) sudo yum remove <package_name> -y 
- How do you handle the errors in shellscript ? Using a special variable called exit-status "$?"
- What is the disadvantage in shellscript ? Even if shellscript faces any error, it wont stop, it will continue to run the script. It is our responsibility to check the errors by writing conditions & exit status.
  
### Session-14 
- Write a shellscript to install multiple packages using loop, like giving args outside the script ?
- Configure the Roboshop project using shellscript ?
- What is SED in shellscript ? If i want permanent change (sed -i) & temperory change (sed -e) ?
- Where this SED is used in shellscript ? It is used to search, find, replace, insert or delete text in a file without opening the file in a text editor.
- Command to check for remote connections ? "netstat -lntp"
- Shellscript is like keeping all individual linux commands in one file, instead of running one by one commands, which was done while configuring the project manually.
- yum list installed git (or) yum list installed | grep <package_name>
- Can we set $? (Exit status) to automatically exit in shellscript ? "set -e" but it wont work.
- Instead of giving &>> $LOGFILE everywhere, we can give "exec &>$LOGFILE" under logfile name.
- What is the use of logs ? In shell scripting, logs are used to record what the script did, when it did it, and whether it succeeded or failed. They act like a black box recorder for your script — if something goes wrong, you can look back and see why.
- To see full log file ---> sudo cat /var/log/messages
- To see page by page ---> sudo less /var/log/messages
- To follow logs in real time (or) to see running logs ---> tail -f /var/log/messages

### Session-15
- How do we set to exit automatically when shellscript faces any errors ? Does really "set -e" useful in exiting the shellscript when it faces error ? NO! why ?
- How do you store logs in shellscript ? Instead of giving &>> $LOGFILE everywhere, we can give like below "exec &>$LOGFILE" under logfile name. See in redis.sh
- unzip -o /tmp/web.zip ---> Here "o" is to overwrite, if you run the script multiple times.
- mkdir -p /app ---> Here -p means if folder exists, it will not create.
- Dont forget to restart nginx server after doing any changes in configuration file.
- Make sure to add all private servers in the web cofiguration.
  
### Session-16
- Write a shellscript to delete old logfiles which are morethan 14 days old ?
- Check Disk Usage and Send email for alerts ?
- Generally we have "cat /etc/passwd" in this, we have all the users information like user_id, group_id,
  user_name etc. So how to read this whole information properly ? or in a structured way ? for that we can
  use IFS (Internal field separator).
- What is the algorithm for deleting old log files ? decide source_dir/search for files/delete.
- How do you create files with old date in server ? "touch -d 20231201 <anyname.log>"
- Command to find old logfiles morethan 14 days old with .log extensions only ?
- Instead of direct "rm -rf" we used while loop to read "command output" line by line & then delete.
- Command to check the information about total space and available space on a file system ?
- How to create a new volume (or) disk in aws console and what is the condition for that ?
- What are the commands to make the disk into usage ? go through the overview steps of the disk creation.
- Creating disk is the work of "Storage team" not DevOps. But just know how it works.
- How do we find different types of file systems ? using reverse search.
- How do you mail the above disk usage from linux server ? we will configure the company mail server details
  to send email alerts.
- So we call mail.sh whenever we want to monitor on disk_usage, not only on disk_usage, we can also call for
  CPU_Utilization, Memory_Utilization etc for monitoring purpose using shellscript, because sometimes
  mailing is not in our control, linux team will give a script like "mail.sh" we can simply call that instead
  of writing this whole command "echo "$message" | mail -s "High Disk Usage" info@joindevops.com"
- Then how to call mail.sh ? "sh mail.sh" "DevOps Team" "High Disk Usage" "$message" "info@joindevops.com"
  "ALERT High Disk Usage", whatever you write after sh mail.sh is arguments we are passing.
- How to go all the way to down in config file ? "shift+G"
- How to go all the way to top in config file ? "gg"
- Basically no need to follow the color coding or formatting, we can just use as it is in mail configuration
  gmail.MD document (or) if your company provide the email configuration document just simply follow that.
- So configuring gmail.MD document for sending mails is morethan enough.
- Monitoring team responsibility is, if websites are down, then monitoring team will send alerts to
  Developers team. If servers are down, then monitoring team will send alerts to DevOps team.

### Session-17
- What is Crontab & why it is useful ? Usage of crontab & giving the script location in "crontab -e"
- How to see the running logs of a Crontab ? "tail -f /var/log/cron"
- What is Optargs in shellscript ? we can control the script behaviour by giving extra inputs to the script
  using a tool called Optargs.
- How to set any shellscript as Native Linux Command ? echo $PATH
- If you install any softwares in these PATHS then, automatically windows (or) linux will pick up from
  this PATHS only.
- Generally if you keep your script in "/usr/local/bin" location, then you NO need to give ".sh" while
  executing the shellscript.
- So "sudo cp 18-greetings.sh /usr/local/bin/greeting (Copied as a greeting name)
- Give executive access "sudo chmod +x /usr/local/bin/greeting" now if you are in any folder otherthan the
  script folder also, just run by using name "greeting" (or) greeting -n sai -w good evening.
- Till now we have created ec2 instances and route53 records manually by logging into aws console.
- Like if web then PublicIP, if not web then PrivateIP right ? and also if mongodb, mysql, shipping then
  t3.small & remaining t2.micro.
- We can now create using aws CLI "aws command line" to automate. In every server we have aws command line,
  you can check using "aws help" in server.
- So we need to write a script to automate using "aws command line" for creating instances & records.
- What are Roles to Resources ? Not only for persons, resources should also have access to access another
  resource, for that we have Roles to Resources like for example if you have created one EC2 and this EC2
  instance should go and create another new instances (or) route53 records.
- How to create a role for ec2 in aws console ? IAM/roles/create role/select EC2 as use case/next/admin
  access (or) amazonEc2fullaccess/route53 full access/give any name to the role.
- How will you asign above role to the ec2 in aws console ? select the already created instance & go to
  Actions/Security/Modify IAM role/Select your created role.
- Remove old credentials which was created for aws console in .aws/ folder by using rm -rf, if you got
  any errors in cd location using "ls -la" command because that was hidden folder.
- Command to create instances with tags ?
- Command to list instances and find the one with your specific name tag ?
- Command to terminate the instances ?
- How do you create administrator user in aws console ? By going to IAM, Users, Create user, Attach
  policies directly, Administrator access, Click on the created user, Security credentials, Create
  accesskey, select CLI.
- Then "aws configure" after creating administrator user in aws console.
- Why we created roles in IAM ? Here if it is a person, he can keep Access_key & Secret_keys safely, will
  EC2 keep these credentials secretly ? If anybody has access to this EC2, he can able to see these
  credentials using "ls -la" command in cd .aws/ because these keys are saved in .aws/ folder only. Thats
  why we have created roles to resources in IAM.
- Write a shellscript to create all instances & records using aws CLI ? Go through the "roboshop.sh" file
  in Roboshop-Shellscript.
- What is UPSERT in shellscript ? if the record exists, update (or) edit it, if it doesn’t exist, it will
  create the records.
- Important point, So overall create any one instance and give a role to it, so that it will create multiple
  instances from this instance only, you need to clone the "roboshop-shellscript" in the server and run the
  "roboshop.sh" script.
- We used --query is to get the PrivateIP of the instances nothing but query from the existing resource.
