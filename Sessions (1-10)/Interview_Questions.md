### What you know about Git and Linux ?
- Git commands and Linux commands.
- Permissions in linux.
- User management
- Process management
- Package management
- Service management
- Giving admin access or limited access to the users

### How do you check the size of a folder in linux ?
du -sh <folder-path>

### How to check if a port is open ?
netstat -lntp

### How do you check running logs ?
tail -f /path/to/logs

### What is swap memory in linux ?
Swap memory is extra space in your computer hard drive that works like a backup RAM, when your computer runs out of RAM, it temporarily moves less used data to this space, so your system doesnt slow down or crash.

### How to check IP address of a linux server ?
ifconfig

### What is the purpose of a chmod ?
Is used to change the permissions of a file or folder. We can set permissions to RWX permissions to owner, group and others

### How to reboot the server when reboot command is not responding ?
We can use the shutdown command with the reboot option ---> "sudo shutdown -r -f now"

### What is the difference between Git and Github ?
Git is a distributed version control used to track code changes in local and manage the versions. Github is a cloud based platform we can hosts our Git repositories, Providing collaboration features like PR, issue tracking etc.

### Explain the difference between git merge and git rebase ?
git merge combines two branches and creating a new merge commit-id and also preserving the history, so that we can track who did what changes. It is used for better collaboration. rebase moves on top of another branch which creates a linear history.

### How do you resolve a merge conflict in Git ?
- Identify the conflicted files "git status"
- Open files and manually resolve conflicts (Look for <<<<<< markers).
- Mark as resolved "git add <file>"
- Commit "git commit -m "Resolved merge conflict"

### What is the difference between fork and clone in GitHub ?
- Fork: Creates a personal copy of someone else’s repository on GitHub (Used for contribution).
- Clone: Downloads a repository to your local machine to start development.

### How can you revert a commit that has already been pushed to a shared branch ?
git revert <commit_hash>

### What are GitHub Actions, and how have you used them ?
- GitHub Actions is a CI/CD tool that automates workflows on GitHub (Build, Test, Deploy).
- Example: Automating code build and deployment to AWS S3 or EC2 on push or pull request events.

### How do you check disk usage on a Linux server ?
df -hT

### How do you check the currently running processes and resource usage ?
top ; ps -ef ; free -h

### Explain the difference between cron and at ?
- cron: Schedules recurring jobs (Daily backups)
- at: Schedules a one-time job (Run a script tomorrow at 2 PM)

### How do you find which process is using a particular port ?
netstat -lntp

### What is the difference between Symlink and Hardlink ?
- Hard link: Points directly to file inode (Memory location, its a number) in hard disk. File data exists even if original is deleted.
- Symlink: Points to file path. Becomes broken if original is deleted.

### How would you monitor logs on a Linux server in real-time ?
tail -f /var/log/syslog  

### How do you manage services in Linux (Start, Stop, Restart) ?
- systemctl start <service>
- systemctl stop <service>
- systemctl restart <service>
- systemctl status <service>

### Explain file permission notation in Linux ?
- r → read, w → write, x → execute.
- Example: -rwxr-xr--
- Owner: read, write, execute
- Group: read, execute
- Others: read

### How do you check if a process is consuming high CPU or memory ?
- top → Sort by %CPU or %MEM.
- ps aux --sort=-%cpu | head -n 10 → Top 10 CPU-consuming processes.
- ps aux --sort=-%mem | head -n 10 → Top 10 memory-consuming processes.

### How to kill a process ?
- kill -9 PID ---> Force kill
- kill PID
