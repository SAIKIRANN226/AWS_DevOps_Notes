### Have you worked on any automation scripts recently ?
- Yes we have few applications running on instances and i was asked to write a script to monitor the resources.
- I wrote a script to monitor the Disk Usage, CPU utilization and Memory Utilization.
- Configured it to send email alerts to the team
- And also i wrote a log cleanup script too, since our application create logs every day
### Can you write a simple shellscript to list all s3 buckets ?
      #!/bin/bash
      
      aws sts get-caller-identity &>> /tmp/somename.log
      if [ $? -ne 0 ]
      then 
          echo -e "AWS CLI not configured properly. Run aws configure first"
          exit 1
      else
          echo -e "$G "Fetching list of aws s3 buckets...$N"
      fi

      aws s3 ls
### How do you write a shellscript to backup a directory everyday ?
      #!/bin/bash

      SOURCE_DIR="path/to/your/data"
      BACKUP_DIR="path/to/your/backups"
      DATE=$(date +%F)
      BACKUP_NAME="backup-$DATE.tar.gz"

      echo "Backing up $SOURCE_DIR into $BACKUP_DIR"
      mkdir -p "$BACKUP_DIR"
      tar -czf "$BACKUP_DIR" "$SOURCE_DIR"

      if [ $? -ne 0 ]
      then 
          echo -e "$R Backup FAILED $N"
          exit 1
      else
          echo -e "$G Backup SUCCESSFUL $N"
      fi
### How do you pass the arguments to the shellscript ?
I will pass the arguments while executing the script like "sh greetings.sh morning", i receive the args inside the shellscript using special variables $1,$2 etc.
### What is the diff btw $@ and $* in bash script ?
- $@ ---> Expands each argument individually
- $* ---> Joins all arguments as one string

      #!/bin/bash
      echo "using $@"
      for arg in "$@"
      do
         echo "$arg"
      done

      echo "using $*"
      for arg in "$*"
      do
         echo "$arg"
      done
### How do you handle errors in shellscript ?
We have one disadvantage in shellscript is even if it is facing error i wont stop, so we use a special variable "$?" to exit, we can also use "set -e" but it will not work everywhere, like for example while configuring a project we may create new folders or users etc. So when you set -e in the script, if will exit in the first step without creating user or folder, because there is no folder for the first time right, so thats why better to use $? only.
### 
      

