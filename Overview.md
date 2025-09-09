### Sessions (1-11)
- What is Computer & what characterstics does computer hold ? What are the use cases of Server, TV, Phone.
- What is Client-Server Architecture ? Transferring media from Phone to Laptop (Viceversa)
- What is Operating systems like Windows & what does it do ?
- What is the difference between Linux (Servers world) & Windows Operating systems ?
- How to connect to Linux server (Node) ?
- What are the Authentication mechanisms to connect to linux server ?
- Generate (or) create a link between LOCK & KEY ? ssh-keygen -f <file_name>
- You can directly generate keys in .ssh folder using "ssh-keygen -f <file_name>"
- Enable extensions in control panel ? File explorer, view, unhide extenions for known files.
- What is the syntax of Public-key ? ssh-rsa {code} Laptop-name
- What is the syntax of Private-key ? BEGIN OPENSSH PRIVATE KEY {code} END OPENSSH PRIVATE KEY
- Now create a server in aws & connect to that server using Public & Private keys.
- Import keypair in aws by going to --> Network & security options --> Keypairs --> Actions & Import key pair
  (Publickey) without any gaps.
- Create a SG (Firewall) for inbound. All traffic 0.0.0.0/0 (Representation of internet)
- Launch instance with keypairs & take Amazon Linux 2AMI (HVM). Make sure the key pair name while you are
  creating server should match the key pair in Network & Security (Key Pairs).
- ssh -i saikiran.pem ec2-user@IP ---> In pwd location (User directory).
- Amazon Linux / Amazon Linux 2 ---> Default user name is "ec2-user"
- Ubuntu ---> Default user name is "ubuntu"
- Centos ---> Default user name is "centos"
- Debian ---> Default user name is "admin (or) debian"
- RHEL ---> Default user name is "ec2-user (or) root"
- Cheapest region is us-east-1 ---> Latency is somewhat slow which is negligible.
- What is Absolute path & Relative path ? An absolute path is the complete path to a file or directory
  starting from the root. Relative path is relative to current directory.
- HTTP --> 80 Hypertext Transfer Protocol (Unencrypted web traffic)
- HTTPS --> 443 Hypertext Transfer Protocol Secure (Encrypted web traffic)
- SSH --> 22 Secure Shell (Secure remote login & file transfer)
- SMTP --> 25 Simple Mail Transfer Protocol (Sending email)
- DNS --> 53 Domain Name System (Resolving domain names to IP addresses)
- Gitbash ---> Is an ssh client & also a mini linux.
- Protocol ---> We have different protocols like https, http, ssh, smtp, dns etc.
- $ ---> Normal user ; # ---> Root user (sudo su -) to exit from root just type exit
- pwd ---> Present working directory you will be directly launched in /c/users/saikiran
- <command_name> --help ---> Get help from that particular command.
- What are the basic linux commands ?
- https://dzone.com/articles/top-35-git-commands-with-examples-and-bonus
- What does CRUD do in software industry (Example of facebook)
- Updating file with content commands & how to save or read the file ? Enter & ctrl+D
- Removing file & folder commands ? rm, rmdir, rm -r <folder_name>
- Copy command in linux & how to copy the files ?
- Move command in linux & how to move the files ? If you use mv command with in the same folder, it works as
  a rename also.
- Grep command in Linux is a case sensitive. Linux will treat DevOps & DEVOPS as different. So to make this
  case insensitive (i) use grep -i ---> ps -ef | grep -i nginx
- Piping symbol ? | ---> One command output will become the input to the another command.
- Difference between wget and curl commands ?
- What is cut & awk commands in linux ? We use cut to quickly extract what we require from the text using
  delimiters. We use awk when we need more advanced processing like filtering rows, formatting output.
- What are Head & Tail commands in linux ? Head is used to view the first few lines of a file, while tail is
  used to view the last few lines. Both are useful for quickly inspecting logs or large files while "tail -f"
  allows real-time monitoring.
- What is VIM in linux ? Is used for creating & editing files.
- Different types of search in a file in server ? :/, :?, shift+G, gg, n
- What Permissions we have in Linux ? What is the file notation ? R(4), W(2), X(1) (Read, Write, Execution).
  Execution access is used to run the scripts & commands.
- In linux when you create a user a group with same name will be created.
- To give execution permission to user then "chmod u+x"
- Removing read, write access to group "chmod g-rw" 
- To give read access to all users to all groups then "chmod ugo+r"
- To remove write access to a group & inside folder also then "chmod g-w -R"
- User management like creating users & giving access to the servers in two methods.
- Password authentication mechanism & SSH access authentication mechanism.
- Create a User & Password for saikiran in server ---> "sudo useradd saikiran" & "passwd saikiran" and all
  user entries will be in "cat /etc/passwd" location. "sudo userdel <username>" ---> To delete user
- id ramesh ---> 1st (uid) ; 2nd (gid) ; 3rd (other groups id). To get groups --> getent group
- If this saikiran wants to connect to the server using IPaddress, we need to change a configuration in
  vim /etc/ssh/sshd_config in gitbash. Here by default linux is disabled for login through password
  authentication as no, So make this yes, then systemctl restart sshd
- So now how will saikiran login (Connect) to the server ? ---> ssh saikiran@IP
- Now raheem joined & how to give SSH authentication (or) using Private key ? "sudo useradd raheem" No need
  to create password for raheem because we are giving access to him using private key.
- I will ask the raheem to give his Public key through mail.
- sudo cd /home/raheem/ enter this command in gitbash after connecting to the server, here we will create
  folder mkdir .ssh and then chmod -R 700 .ssh also make the .ssh folder to raheem ownership by "chown -R
  raheem:raheem(group) .ssh" now create a file inside .ssh folder "vim authorized_key" paste the raheem
  public key here, ask him to create keypair for this. Then change modification to "chmod 400 authorized_key"
  so that raheem can only read, he cant write because it is better to put read only to protect the file.
- 7 --> user (RWX) , 0 --> group , 0 --> others ===> "chmod -R 700 .ssh"
- Now we will tell raheem that your username is configured & we will give him the IPaddress then raheem will
  login using this command "ssh -i raheem raheem@IP" Here first raheem is his Privatekey & second reheem is
  Username.
- The process of creating users & groups is done by linux admin team but just know how to create users and
  groups, adding users into groups etc.
- What is Process management in linux ? Nothing but how the OS creates, schedules, monitor and terminate
  processes. Each process has unique id. We can monitor processes using ps, top commands & control them with
  kill <pid> or kill -9 <pid> commands.
- When process stuck kill the process ---> "kill PID" do not kill parent process id 1st is PID second one is
  parent id. If even kill cannot kill, then forcefull terminate "kill -9 PID"
- What is Package management in linux ? How the software is installed, updated or removed on the system. We
  use yum command ; yum list installed ; yum remove -y ; yum install <package>
- What is Service management in linux ? Is about starting, stopping, monitoring, and configuring background
  services like web servers or databases. Tools like systemctl (systemd) or service commands are used to
  control them.
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
- Ramesh ---> Give Admin full access, under wheelgroup & enter %admin ALL=(ALL) ALL
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
- Connection --> data --> username (ec2-user) --> then go to session & save (Important)
- Create a server in aws & take the IP and paste it in putty (Hostname) click on load to connect.
- To change the font open putty --> appearence --> change & then save to make effect in superputty.
- What is the Linux file system structure ?
- When putty stucks (or) unable to enter any command then open putty first load your session then go to
  connection ---> Give 30 in seconds then go to session & save, generally we have value 0 you need to give
  any value like 30, that means every 30 seconds connection will be alive, you can give max 300.
- What is Inode ? Inode is the representation of file & folder inside the memory, it is a number. How to
  get that number ? ls -li
- What is Symlink & Hardlink ? Symlink will point to the file not to the inode while Hardlink will point
  directly to the inode not to the file.
- How to create a Symlink for a file ? First create a file hello & add content in it using cat command, then
  create symlinnk "ln -s /home/ec2-user/hello /tmp/hello-soft" We can give obsolute path or relative path.
- How to create a Hardlink for a file ? "ln /home/ec2-user/hello /tmp/hello-hard"
- We use nginx as front-end servers because it can handle high traffic, it is used as reverse proxy.
- IIS is only used for windows based applications.
- We have "winscp" for file transfer, it is a mini windows in linux server.
- Generally frontend servers called as HTTP servers on port 80. Hosts html, java based applications.
- Backend is also HTTP servers but on port 8080. Hosts like tomcat, jboss, .net, python etc.
- What is the difference between PublicIP vs PrivateIP ? How the Modem will provide PrivateIPs to the
  internal systems (or) to laptops ? Using NAT
- What is NAT (Network address translation) ?
- What is Fibre exchange points ?
- What is Enterprise archive file ? Servlets (DB) ; JSPS (UI) ---> Monolithic
- What is Monolithic vs Microservices ? Monolithic means Single unified application, easy to start, hard to
  scale. Microservices will Split into independent services, scalable & flexible, but more complex.
- Frontend (80) ---> HTML, JS, AngularJS, Java applications.
- Backend (8080) ---> Databases like mysql, postgre etc.
- To connect from one server to another server "telnet <IP> <port_number>"
- If telnet is not installed ---> sudo yum install telnet -y ; netstat -lntp shows all TCP ports currently
  being listened on, along with the process using each port. I use it in DevOps to check whether services
  like Nginx, MySQL, or application servers are actually listening on the expected ports.
- To check if a command is installed or not ? Use "which" usage is "which telnet" "which yum" etc.
- If you type "ipconfig" in cmd you will get all details, IPv4 is my PrivateIP, IP under default gateway is
  modem. IPv4 are exhausting and we are upgrading to IPv6 till then we can use IPv4. We have 2power32
  IPaddresses. If we allocate all these, we get problems. So they brought "NAT" Network Address Translation.
  However latency will be slow that is nothing but time to respond will be somewhat slow.
- Frontend (WEB) & Backend (API) are Stateless ; DB is Statefull.
- WEB & API will work only when DB is in existence. Example of CRUD over facebook.
- We are using web servers as nginx on HTTP protocol only, it can also use HTTPS.
- Installing packages using yum & dnf. But dnf is preferred while configuring project manually because it
  consumes less memory when compared to yum. Yum is used in automation like shellscripting.
- Location of nginx configuration "cd /etc/nginx/nginx.conf"
- Location of the default content of the nginx "cd usr/share/nginx/html/"
- What is Forward proxy & Reverse proxy ? Nginx is used as reverse proxy.
- Reverse proxy is mainly used for Load balancers & Server anonymous.
- Location of reverse proxy configuration "vim /etc/nginx/default.d/roboshop.conf"
- What are the famous HTTP status codes ?
- Configure the Roboshop project manually ?
- What is cache (Redis) server ? Example of downloaded movie by 1 user.
- What is Domain name system (DNS) & how do you register your domain ?
- Steps to install any application in linux ?
- What is the difference between Synchronous & Asynchronous in networking ?

### Shellscript 

