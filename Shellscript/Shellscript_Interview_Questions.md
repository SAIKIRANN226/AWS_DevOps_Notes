- Have you worked on any automation scripts recently ?
Yes we have few applications running on Instance, i was asked to write the resources monitoring scripts, so i wrote CPU,Memory,Disk Utilization. I developed the scripts to scheduled through crontab every 15min, i configured it to send emails to the team channels. script like "user-05-06-2025.log"
- Can you write a simple shellscript to list all S3 buckets ?

            #!/bin/bash
            echo "Fetching list of s3 buckets..."
            aws sts get-caller-identity >/dev/null 2>$1
            if [ $? -ne 0 ]
            then
              echo "AWS CLI not configured properly, run 'aws configure' first"
              exit 1
            fi

            aws s3 ls
            echo "done"
- How do you write a shellscript to backup a directory everyday ?
  #!/bin/bash
  SOURCE_DIR="/path/to/your/data"
  BACKUP_DIR="/path/to/your/backup"
  DATE=$(date)
  BACKUP_NAME="backup-$DATE.tar.gz"
  echo "backing up $SOURCE_DIR..."
  
