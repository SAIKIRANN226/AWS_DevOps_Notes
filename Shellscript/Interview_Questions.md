### Have you worked on any automation scripts recently ?
Yes we have few applications running on VM, i was asked to write resources monitoring scripts, so i wrote for CPU Utilization, Memory Utilization, Disk Utilization. I developed this script and scheduled through crontab for every 15 min and i configured it to send alerts in email and team channels and also i wrote log cleanup script, since our application creates logs every day in our servers, for example "user-05-06-2024.log" My script archives logs older than 7 days, I moved this archives to S3 bucket, I delete zip files older than 30 days from the server.

### Can you write a simple shellscript to list all S3 buckets ?
    #!/bin/bash
    echo "Fetching the list of S3 buckets...."
    aws sts get-caller-identity >/dev/null 2>&1
    if [ $? -ne 0 ]
    then 
        echo -e "$R AWS_CLI is not configured properly. Run aws configure first $N"
        exit 1
    fi 
    aws s3 ls 
    echo "Done"
    
### How do you write a shellscript to backup a directory everyday ?
    #!/bin/bash
    SOURCE_DIR="/path/to/your/data"
    BACKIP_DIR="/path/to/your/backups"
    DATE=$(date)
    BACKUP_NAME="backup-$DATE.tar.gz"

    echo "Backing up $SOURCE_DIR to $BACKUP_DIR/$BACKUP_NAME...."
    mkdir -p "$BACKUP_DIR"
    tar -czf "$BACKUP_DIR/$BACKUP_NAME" "$SOURCE_DIR"

    if [ $? -eq 0 ]
    then 
      echo -e "$G Backup is successful $N"
    else 
      echo -e "$R Backup is failed $N"
    fi 
Here .tar means It’s a single file that contains many files/folders bundled together — kind of like putting everything into one big box, but without compression and .gz means After making the .tar archive, it is compressed with the gzip algorithm to make it smaller. This results in a .tar.gz file — a compressed archive. Think of it like putting all your files in a box (.tar) and then shrinking the box (.gz) so it takes less space.

### How do you pass arguments to the shellscript ?
I will pass arguments to the shellscript while executing the script, for example "sh greetings.sh morning" i receive the args inside the sript through special variables like $1,$2,$3...$N. Number of args "$#" All args special variable is like "$@"

### What is the difference between $@ and $* in bash scripts ?
$@ and $* both are used to access all the arguments passed to the bash script. $@ expand each argument individually. $* Joins all arguments as one string.

    #!/bin/bash
    echo "Using $@"
    for arg in "$@";
    do 
        echo "$arg"
    done

    echo "Using $*"
    for arg in "$*";
    do 
        echo "$arg"
    done 

    sh saikiran.sh "arg one" "arg two" 
    Using $@: 
    arg one
    arge two

    Using $*:
    arge one arg two

### How do you handle errors in shellscript (or) How do you debug a shellscript ?
Shellscript will not exit when it faces errors, it will continue to run, we need to check every command using exit-status "$?" and exit if faces any error, we can also "set -e" also after shibang, but it will not work most of the times.

### What’s the difference between > and >> in shell scripting ?
Greaterthan symbol > means overwrites the file and >> appends the file.

### How do you read a file line-by-line in bash ?
        while IFS= read -r line; do
          echo "$line"
        done < file.txt
### Explain the difference between soft link and hard link ?
Soft link (symbolic link): Points to the file path, can link across file systems, breaks if the original is deleted. Hard link: Points directly to the inode, must be on the same file system, remains valid even if the original is deleted.

### How do you check if a process is running in a shell script ?
        if pgrep -x "nginx" > /dev/null; then
          echo "Running"
        else
          echo "Not running"
        fi

### How do you replace all occurrences of a string in a file using shell commands ?
sed -i 's/old_text/new_text/g' file.txt

### How do you find the number of lines, words, and characters in a file ?
wc file.txt

### Write a script that reads usernames from a file and checks if they exist in the system ?
        #!/bin/bash
        while read -r user; do
          if id "$user" &>/dev/null; then
            echo "$user exists"
          else
            echo "$user not found"
          fi
        done < users.txt
### Write a script to read a file and print only lines that contain the word "ERROR" ?
        #!/bin/bash
        LOG_FILE="/var/log/messages"
        grep "ERROR" "$LOG_FILE"

### Write a script to check if a service is running; if not, start it ?
        #!/bin/bash
        SERVICE="nginx"
        
        if ! pgrep -x "$SERVICE" > /dev/null; then
          echo "$SERVICE is not running. Starting..."
          systemctl start "$SERVICE"
        else
          echo "$SERVICE is running."
        fi

### 






