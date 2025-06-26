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

