- What is Computer and what characterstics does computer hold and What are the use cases of Server, TV,
  Phone etc.
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
- Take PublicIP of the instance and username is "ec2-user" (or) Centos & "Privatekey"
- ssh -i saikiran.pem ec2-user@123.23.234.5 ---> In pwd location. Use Centos as username not ec2-user.
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
- Port number for SSH ---> 22
- Ec2 server ---> SSH server
- "$" ---> Normal user
- "#" ---> Root user(sudo su -) to exit from root just "exit"
- "pwd" ---> Present working directory you will be launched in /home/ec2-user
- "uname" ---> Will tell the kernel name
- "command-name" --help ---> Get help from that particular command (or) you can get help from man command
  also "man"
- 
