- What is Computer & what characterstics does computer hold ? What are the use cases of Server, TV, Phone
  etc. Linux is the servers world.
- What is Client-Server Architecture ? Transferring media from Phone to Laptop (Viceversa)
- What is Operating systems like Windows and what does it do ?
- What is the difference between Linux and Windows Operating systems ?
- How to connect to Linux servers and what is the another name of Server ?
- What are the Authentication mechanisms to connect to linux server ?
- Generate (or) create a link between "LOCK & KEY" ? ssh-keygen -f <file_name>
- Enable extensions in control panel ? File explorer, view, unhide extenions for known files.
- What is the syntax of Public-key ? ssh-rsa {code} Laptop-name
- What is the syntax of Private-key ? BEGIN OPENSSH PRIVATE KEY {code} END OPENSSH PRIVATE KEY
- Now create a server in aws and connect to that server using Public & Private keys.
- Import keypair in aws by going to --> Network & security options --> Keypairs --> Actions and Import
  key pair (Publickey) without any gaps.
- Create a Security group (Firewall) for inbound. All traffic 0.0.0.0/0 (Representation of internet)
- Launch instance with keypairs and take Amazon Linux 2AMI (HVM). Make sure the key pair name while you are
  creating server should match the key pair in Network & Security (Key Pairs).
- ssh -i saikiran.pem ec2-user@52.23.206.196 ---> In pwd location.
- Amazon Linux / Amazon Linux 2 ---> Default user name is "ec2-user"
- Ubuntu ---> Default user name is "ubuntu"
- Centos ---> Default user name is "centos"
- Debian ---> Default user name is "admin (or) debian"
- RHEL ---> Default user name is "ec2-user (or) root"
- Cheapest region is "us-east-1" ---> Latency is somewhat slow which is negligible.
- What is Absolute path and Relative path ? An absolute path is the complete path to a file or directory
  starting from the root. Relative path is relative to current directory.
- HTTP --> 80 Hypertext Transfer Protocol (Unencrypted web traffic)
- HTTPS --> 443 Hypertext Transfer Protocol Secure (Encrypted web traffic)
- SSH --> 22 Secure Shell (Secure remote login and file transfer)
- SMTP --> 25 Simple Mail Transfer Protocol (Sending email)
- DNS --> 53 Domain Name System (Resolving domain names to IP addresses)
- Gitbash ---> Is an ssh client and also a mini linux.
- Protocol ---> We have different protocols like https, http, ssh, smtp, dns etc.
- "$" ---> Normal user "#" ---> Root user (sudo su -) to exit from root just "exit"
- "pwd" ---> Present working directory you will be directly launched in /c/users/saikiran
- "command-name" --help ---> Get help from that particular command
- What are the basic linux commands ?
- What does CRUD do in software industry. Example of facebook
- Updating file with content commands and how to save or read the file ? Enter & ctrl+D
- Removing file and folder commands.
- Copy command in linux & how to copy the files ?
- Move command in linux & how to move the files ? If you use mv command with in the same folder, it
  works as a rename also.
- Grep command in Linux is a case sensitive. Linux will treat DevOps and DEVOPS as different. So to make this
  case insensitive (i) use "grep -i" ---> ps -ef | grep -i nginx
- Piping symbol ? | ---> One command output will become the input to the another command.
- What is wget and curl commands in linux and what is the difference ?
- What is cut & awk commands in linux ? We use cut to quickly extract what we require from the text using
  delimiters. We use awk when we need more advanced processing like filtering rows, formatting output.
- What are Head and Tail commands in linux ? Head is used to view the first few lines of a file, while tail
  is used to view the last few lines. Both are useful for quickly inspecting logs or large files & tail -f
  allows real-time monitoring.
- What is VIM in linux ? Is used for creating & editing files.
- Different types of search in a file in server ? :/, :?, shift+G, gg, n
- How to find & replace something in the server ? :%s/sbin/SBIN/g --> %s means all occurances.
- Permissions in Linux ? What is the file notation we have in server ? What are the permissions we have ?
  R(4), W(2), X(1) (Read, Write, Execution). Execution access is used to run the scripts & commands.
- In linux when you create a user a group with same name will be created.
- To give execution permission to user then "chmod u+x"
- Only for owner then "chmod g-rw " removing read, write to group
- To give read access to all users to all groups then "chmod ugo+r"
- To remove write access to a group & inside folder also then "chmod g-w -R"
- User management like creating users and giving access to the servers in two methods.
- Password authentication mechanism & SSH access authentication mechanism.
- Create a user & password ---> "sudo useradd saikiran" & "passwd saikiran" and all user entries will be in
  "cat /etc/passwd" location. "sudo userdel <username>" ---> To delete user
- "id ramesh" ---> 1st (uid) ; 2nd (gid) ; 3rd (other groups id). To get groups --> getent group
- If this ramesh wants to connect to the server using IPaddress, we need to change a configuration by going
  to "vim /etc/ssh/sshd_config" in gitbash only. Here by default linux is disabled for login through password
  authentication no, So make this yes, then "systemctl restart sshd".
- sshd -t ---> Will know any mistakes have done in the previous command, checks syntax of file.
- So now how will ramesh login (Connect) to the server ? ---> "ssh ramesh@IP"
- Now raheem joined and how to give SSH authentication (or) using Private key ? sudo useradd raheem
- I will ask the raheem to give his Public key through mail.
- sudo cd /home/raheem/ enter this command in gitbash after connecting to the server, here we will create
  folder "mkdir .ssh" and then "chmod -R 700 .ssh" also make the .ssh folder to raheem ownership by
  "chown -R raheem:raheem(group) .ssh" now create a file inside .ssh folder "vim authorized_key" paste the
  raheem public key here, ask him to create keypair for this. Then change modification to "chmod 400
  authorized_key" so that raheem can only read, he cant write because it is better to put read only to
  protect the file.
- 7 --> user (RWX) , 0 --> group , 0 --> others ===> "chmod -R 700 .ssh"
- Now we will tell raheem that your username is configured and we will give him the IPaddress then raheem will
  login using this command "ssh -i raheem raheem@IP" Here first raheem is his Privatekey and second reheem is
  Username.
- The process of creating users and groups is done by linux admin team but just know how to create users
  and groups, adding users into groups etc.
- What is Process management in linux ? "ps -ef | grep jenkins"
- When process stuck kill the process ---> "kill PID" do not kill parent process id 1st is PID second one
  is parent id. If even kill cannot kill, then forcefull terminate "kill -9 PID"
- What is Package management in linux ? yum install ; yum list installed ; yum remove -y
- What is Service management in linux ?
- systemctl start nginx ---> This is how to make a package into service.
- systemctl status nginx ---> To know if it is running or not (or) we can also check with process "ps -ef |
  grep -i nginx"
- systemctl stop nginx ---> To stop the service.
- systemctl enable nginx ---> Automatically services will run.
- systemctl disable nginx ---> Will disable nginx.
- What is Network managment in linux ? How do you check port & process running ? netstat -lntp
- What are the general trouble shooting process you do ?
- How to give admin access (or) any other access to linux users ? Example two types of users. Linux admin
  team ---> Full admin access ; DevOps team ---> Limited sudo access
- Generally to give sudo access we have one file "/etc/sudoers" So "vim /etc/sudoers" It is not recommended
  to open this file because it is crucial so linux has given one command to open then file safely that is
  "visudo"
- Ramesh ---> Give Admin full access, under wheelgroup and enter %admin ALL=(ALL) ALL
- Suresh limited access ---> %devops ALL=(ALL) /usr/bin/yum,/usr/bin/systemctl
- For ramesh we have given full admin access but for suresh we can give only few limited access like "yum"
  command (To know where this command is installed "which yum" (or) "which systemctl"
- Everytime opening "visudo" is also a risky. Linux has given one location "vim /etc/sudoers.d"
- vim /etc/sudoers.d/DevOps (Created folder) --> %devops ALL=(ALL) /usr/bin/yum,/usr/bin/systemctl
- vim /etc/sudoers.d/Admin (Created folder) --> %admin ALL=(ALL) ALL
- What is 3Tier architecture ?
- In previous session how do we connected to servers in gitbash ? Then how putty will connect ?
- In gitbash we call Privatekey as ".pem" but in putty we call it as ".ppk" (Putty privatekey)
- How to create this putty private key (.ppk) ? Load .pem file in puttygen save with .ppk extension
- Open putty --> connection --> ssh --> auth --> credentials --> load your saved .ppk file
- Connection --> data --> username (ec2-user) --> then go to session and save (Important)
- Create a server in aws and take the IP and paste it in putty (Hostname) click on load to connect.
- To change the font open putty --> appearence --> change and then save to make effect in superputty.
- From where the html files will load in nginx ? "/usr/share/nginx/html"
- How to keep sample html website from the internet ? First remove html folder then keep yours.
- What is the Linux file system structure ?
- When putty stucks (or) unable to enter any command then open putty first load your session then go to
  connection ---> Give 30 in seconds then go to session & save, generally we have value 0 you need to give
  any value like 30, that means every 30 seconds connection will be alive, you can give max 300.
- What is Symlink and Hardlink and what is Inode ?
- How to create a symlink for a file ? "ln -s /home/ec2-user/hello /tmp/hello-soft"
- How to create a hardlink for a file ? "ln /home/ec2-user/hello hello-hard" if you dont give "s" it will
  become hardlink.
- We use nginx as front-end servers because it can handle high traffic, it is often used as a reverse proxy,
  we used nginx only in all sessions.
- IIS is only used for windows based infrastructure.
- We have "winscp" for file transfer, it is a mini windows for linux server.
- Generally frontend servers called as http servers port 80. Hosts html, java based applications.
- Backend is also http servers but port 8080. Hosts like tomcat, jboss, .net, python etc.
- These frontend and back will connect through API's
- What is the difference between PublicIP vs PrivateIP ? How the Modem will provide PrivateIPs to the
  internal systems (or) to laptops ?
- What is ipconfig, what is my ip, what is your private ip
- What is NAT (Network address translation) ?
- What is Fibre exchange points ?
- What is Enterprise archive file ? Servlets (DB) ; JSPS (UI)
- What Monolithic vs Microservices ?
- Frontend (80)---> HTML, JS, AngularJS, Java applications.
- Backend (8080) ---> Databases like mysql, postgre etc.
- To connect from one server to another server we use "telnet port" Usage is "telnet 3.34.345.0 8080"
- If telnet is not installed ---> sudo yum install telnet -y ; If connection is refused, check wether any
  process or application is working on that particular port by using "netstat -lntp" then change inbound.
- If you type "ipconfig" you will get all details, IPv4 is my PrivateIP, IP under default gateway is modem.
  IPv4 are exhausting and we are upgrading to IPv6 till then we can use IPv4. We have 2power32 IPaddresses,
  If we allocate all these, we get problems. So they brought "NAT" Network Address Translation, However
  latency will become slow is nothing but time to respond.
- What does Security groups (Firewalls) do ?
- Frontend (Web) and Backend (Api) are Stateless ; DB is Statefull.
- Web and Api will work only when DB is in existence. Example of a CRUD over facebook.
- We are using webservers as nginx on http protocol only, it can also use https.
- Installing packages using yum and dnf. But dnf is preferred while configuring project manually because it
  consumes less memory.
- In the server where does the nginx configuration is saved ? "cd /etc/nginx/" vim nginx.conf
- Where does the default content of the nginx will be saved ? "cd usr/share/nginx/html/"
- What is Forward proxy and Reverse proxy ?
- Reverse proxy is mainly used for loadbalancers and server anonymous.
- Where will be the reverse proxy configuration ? "vim /etc/nginx/default.d/roboshop.conf"
- What are the famous HTTP status codes ?
- Configure the Roboshop project manually ?
- What is cache server ? Example of downloaded movie by 1 user. Redis is the cache server.
- What is Domain name system (DNS) and how do you register your domain ?
- Steps to install any application in linux ?
- What is Synchronous vs Asynchronous in networking ?
