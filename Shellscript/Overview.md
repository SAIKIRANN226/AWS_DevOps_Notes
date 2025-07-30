### Session-12
- Why we use SSH based authentication to connect to github accounts ?
- What is the port number of SSH ?
- Algorithm for connecting to github account ?
- Command to generate a Key-Pair ?
- Which one should we prefer while cloning the repo HTTPS (or) SSH ?
- HTTPS is for username and password
- What is shibang in shellscript (or) bashscript ?
- How do you capture the output of any linux command in a variable ?
- What is the use of arguments in the shellscript ?
- While connecting to external systems like DB, how to hide password while entering in terminal ?
- Is really data-types are important in shellscript ?
- What are arrays in shellscript ?

### Session-13
- Install mysql, git, postfix, net-tools using conditions, functions & store logs in tmp.
- Write a shellscript to install multiple packages using loops ?
- Write a loop to print 1 to 1000 in shellscript ?
- What is root user and exit status ?
- What is function is shellscript ?
- What is the purpose of redirection ?
- How to redirect the output ? "yum install nginx -y > output.text"
- You can keep any name in place of output like saikiran.text etc.
- What are special variables in shellscript and it should be in the double qotes ?
- Colour coding in shellscript ?
- How to remove package in shellscript ?
- How do you handle the errors in shellscript ?
- What is the disadvantage in shellscript ?
  
### Session-14 
- Write a shellscript to install multiple packages using loop ?
- Configure the Roboshop project using shellscript ?
- What is SED in shellscript ? what to keep if i want permanent change and temperory change ?
- Where this SED is used in shellscript ?
- How to check logs in shellscript ?
- Command to check remote connections ? netstat -lntp
- Shellscript is keeping all individual Linux commands in one file, instead of one by one commands.
- Which was done while manual configuration.
- yum list installed git (or) yum list installed | grep <package_name>
- Can we set $? (Exit status) to automatically exit in shellscript and why we dont prefer this ?
- Instead of giving &>> $LOGFILE everywhere, we can give "exec &>$LOGFILE" under logfile name.
- What is the use of logs ? why we check logs ?

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
