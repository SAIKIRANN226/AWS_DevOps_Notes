- What is Computer and what characterstics does computer hold and What are the use cases of Server, TV,
  Phone etc. Linux is the servers world.
- What is Client-Server Architecture ?
- What is Operating systems like Windows and what does it do ?
- What is the difference between Operating systems Linux and Windows ?
- How to connect to Linux servers and what is the another name of Server ?
- What are the Authentication mechanisms to connect to linux server ?
- How to generate (or) create a link between "LOCK and KEY" using a command ?
- How to enable extensions in control panel ? File explorer, view, unhide extenions for known files.
- What is the syntax of Public-key ? ssh-rsa {code} Laptop-name
- What is the syntax of Private-key ? BEGIN OPENSSH PRIVATE KEY {code} END OPENSSH PRIVATE KEY
- Now create a server in aws and connect to that server using Public and Private keys.
- Import keypair in aws by going to --> Network & security options --> Keypairs --> Actions and Import
  key pair (Publickey) without any gaps.
- Create a Security group (Firewall) for inbound. All traffic 0.0.0.0/0 (Representation of internet)
- Launch instance with keypairs and take Amazon Linux 2AMI (HVM)
- ssh -i saikiran.pem ec2-user@123.23.234.5 ---> In pwd location.
- Amazon Linux / Amazon Linux 2 ---> Default user name is "ec2-user"
- Ubuntu ---> Default user name is "ubuntu"
- Centos ---> Default user name is "centos"
- Debian ---> Default user name is "admin (or) debian"
- RHEL ---> Default user name is "ec2-user (or) root"
- Make sure the key pair name while you are launching instance should match the key pair in Network &
  Security (Key Pairs).
- Cheapest region is "us-east-1" ---> Latency is somewhat slow which is negligible.
- What is Absolute path and Relative path ?
- HTTP --> 80 Hypertext Transfer Protocol (Unencrypted web traffic)
- HTTPS --> 443 Hypertext Transfer Protocol Secure (Encrypted web traffic)
- SSH --> 22 Secure Shell (Secure remote login and file transfer)
- SMTP --> 25 Simple Mail Transfer Protocol (Sending email)
- DNS --> 53 Domain Name System (Resolving domain names to IP addresses)
- Gitbash ---> Is an ssh client and also a mini linux
- Protocol ---> We have different protocols like https, http etc.
- Ec2 server ---> SSH server
- "$" ---> Normal user
- "#" ---> Root user(sudo su -) to exit from root just "exit"
- "pwd" ---> Present working directory you will be launched in /c/users/saikiran
- "uname" ---> Will tell the kernel name
- "command-name" --help ---> Get help from that particular command
- What are the basic linux commands ?
- What does CRUD do in software industry. Example of facebook
- Updating file with content commands and how to save or read the file ?
- Removing file and folder commands.
- Copy command in linux and how to copy the files ?
- Move command in linux and how to move the files ? With in the same folder if you use mv command, it
  works as a rename also.
- Grep command in linux grep Linux is a case sensitive. Linux will treat DevOps and DEVOPS as different.
  So to make this case insensitive (i) use "grep -i"
- Piping symbol ? | ---> One command output will become the input to the another command.
- What is wget and curl commands in linux and what is the difference ?
- What is cut and awk commands in linux ? We use cut to quickly extract specific columns or character ranges
  from text using delimiters. It’s simple and lightweight. We use awk when we need more advanced processing
  like filtering rows, formatting output, or doing calculations — since it’s a full text-processing language.
- What are Head and Tail commands in linux ? Head is used to view the first few lines of a file, while tail
  is used to view the last few lines. Both are useful for quickly inspecting logs or large files, and tail -f
  allows real-time monitoring.
- What is VIM in linux ? Is used for creating files and editing files.
- Different types of search in a file in server ? :/, :?, shift+G, gg, n
- How to find and replace something in the server ?
- 


