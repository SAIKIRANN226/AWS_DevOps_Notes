### Deleting old log files more than 14 days old
- Delete old log files, Check disk usage and Send email alerts.
- For example we have a folder, where we are storing log files.
- Delete log files more than 14 days, only with ".log" extensions not any other files.

### Algorithm for deleting old log files (or) simple algorithm
- First decide, what is your Source-Directory (or) Folder where we are storing log files.
- Search more than 14 days old, only with ".log" extension not any other files.
- Then Delete "rm -rf". Below is the simple script to delete old log files.

### 15-delete-old-log.sh
- Create a folder for logs "mkdir /tmp/saikiran-logs" in cd location in linux server.
- Create few files with old date in the folder, so that we can delete the old log files.
- Command to create files with old date "touch -d 20231201 <anyname.log>"
- find . -type f -mtime +14 ---> f(files), .(means current directory)
- find . -type f -mtime +14 -name "*.log" ---> We want only with .log extension files.
- Now we can delete using "rm -rf" but we use while loop to read "command-output" line by line.
- You can search in chatgpt like write a shell script to delete old log files in a folder morethan 14 days
  old, you will get the script then copy and adjust according to your requirement and it worked for me.

### 16-ifs.sh
Generally we have "cat /etc/passwd" in this we have all the users information like user_id, group_id, user_name and many more other information, so how to read this whole information properly ? or in a structured way, then we can use IFS (Internal field separator).

### 17-disk-usage.sh
Command is "df -hT", if the disk usage goes above 70% we need to triggger a mail, so create another disk of 12gb for practice because in real time there will be more disks, so go to aws console and then navigate to Elastic Block Store ---> Volumes ---> Create volume ---> Action ---> Attach to the instance, so while creating disk there is one condition like for example disk should always near to the laptop. Similarly here also disk should create in the same availability zone where the server is created, when you check in the server "df -hT" still created disk is not showing, so you need to explicitly mount it by using a command "lsblk" and to make into usage, create a file system using "sudo file -s /dev/xvdf" ---> dev means devices that means we are creating xvdf folder inside the devices folder, then check wether it is created or not "sudo lsblk -f" and then run this command "sudo mkfs -t xfs /dev/xvdf" and then create a folder in root folder "cd /" by using this command "sudo mkdir /data" then mount it by "sudo mount /dev/xvdf /data".

### Overview steps of the above disk creation
- Create a disk in Elastic Block Store and attach to the instance then "df -hT"
- lsblk ----> To make available (or) disk is added
- sudo file -s /dev/xvdf ----> To create a file system
- sudo lsblk -f ----> To check wether the disk is functional (or) not ?
- sudo mkfs -t xfs /dev/xvdf ----> It is xfs type
- sudo mkdir /data ----> To create a data folder in "cd /"
- sudo mount /dev/xvdf /data ----> Mounting

### Finding different types of disks using grep command
- df -hT | grep xfs
- df -hT | grep tmp
- df -hT | grep -v tmp ---> -v means i dont want lines with tmp words; 
- df -hT | grep -vE 'tmp|File' ---> | ---> or ; & ---> and

### mail.sh
- Mailing the above disk usage to send alerts, sending mails from linux we have to configure email, so install
  the packages from gmail.MD document in concepts folder in linux server in home folder CD, but in real time
  company will give you mail server details to configure and in this, we need to configure gmail. Postfix will
  hit gmail API ; cyrus-sasl-plain will set authentication ; mailx is a command to send mail,so thats why we
  need to install these packages from gmail.MD; shift+G ---> godown in the config file and append the given
  small config and save :wq!
- We need "From" address and "To" address
- So open gmail in chrome go to Profile/manage your google account/security/2-step verification/turn-on/app
  passwords/app-name(any)/copy the generated password this password is only for linux wont work for gmail. 
- Remove spaces in password and put "from" address in the place of xyz: your gmail without "@gmail" and put
  in the "vim /etc/postfix/sasl_passwd"
- We can do mail formatting for better looking with color coding
- Converting text to html format from google websites
- Just write what ever you want from the compose message with required colors and copy that and paste in the
  converting text to html format from google websites and put the converted text to html lines in a template
  and we can call whenever required using mail.sh,to call mail.sh we need to use sh mail.sh "DevOps Team"
  "High Disk Usage" "$message" "info@joindevops.com" "ALERT High Disk Usage" in 17-disk-usage.sh

### Improved way of deleting old log files
- Instead of deleting only one particular folder,user has to enter source directory
- Action ---> We will ask user wether we should archive or delete instead of deleting log files of 14 days
  which is not a good practice.
- If he select archive ---> Where is the destination directory ?
- Time ---> Optional,if he gives take it otherwise,14 days default
- Memory ---> Optional,if he dint given then dont consider memory,if he gives then consider it

### Below is the usage of command
old-logs.sh -s <source_dir> -a <archive/delete> -d <destination_dir> -t <no-of-days> -m <memory-in-mb>

### Algorithm to check for the above command
- Wether the user has given proper command like -s, -a, -t, -m check all these inputs,if he dont give proper
  then tell him the correct usage.
- Source directory exists (or) not ?
- Destination directory exists (or) not ?
- If he dont give destination directory throw the error 
- Then archive (or) delete.

### Points to remember
- For any programming languages (or) for any scripting. It is all about variables/datatypes/conditions/loops
  and functions, but with a little different syntax, only we need to make sure wether we are following the
  correct algorithm or not ?
- Shift+G ---> To go down in the config_file.
- gg ---> To go top in the config_file.
