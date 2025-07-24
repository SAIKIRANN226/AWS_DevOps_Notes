### Overview of previous sessions
- We learned linux and how to use linux commands.
- Configured the project manually.
- We automated (or) configured the project using shellscript.
- We automated (or) configured the project using ansible also.
- Then created infrastructure using terraform.
- Infrastructure using terraform + Jenkins CICD for apps + we installed applications.
- Finally we deployed into the VMs in AWS cloud (Like EC2 is nothing but a VM)
- That means till now our applications are deployed into VM based.
- From this session, we are going to deploy applications in Docker & Containerization.

### Containerization
Containerization is a lightweight form of virtualization (VM) that involves packaging an application and all its dependencies (like libraries, configuration files, and binaries) into a single, self-contained unit called a container. This allows the application to run consistently across different environments from a developer's laptop to test environments to production servers. How the world evolved from past is the below example.
Physical severs (laptop) ---> Virtualization (VM) ---> Containerization. When we compare these 3 we have more security in Physical servers, however we can increase security by taking few steps.

For example in Guest OS, we have created one For Centos ---> 1GB ram, Ubuntu, 100GB HDD. But application is used only 0.1GB of ram, 10GB of HDD, remaining space is wasted right ? So this is nothing but virtualization VM concept right ? and here Hypervisor is blocking remaining space, that means resource utilization is not that much better. So in this VM only we have containerization concept, nothing but we have containers installed in this VM, containers are isolated from each other (similar to the individual rooms example) but system resources (centos ---> 1GB ram, Ubuntu, 100GB HDD) are shared, that means containers will take resources based on demand from this system resources. System resources will dont block. Boot time is very less (with in seconds) compared to VM (EC2 instance)

### Configuration
When comparing with the example of vacating the place from Independent house, Apartment, Individual rooms. We can take all the things in a single bag (configuration) and vacate the Individual rooms with in hours, but when we try to vacate the Flat in Apartment, your things (configuration) will be more compared to Individual room and vacate with in 2-3 days. So similarly when vacting from the Independent house is also same things (configuration) will be more.

### Container (or) Image
What we have done previously ? In this container (or) image ---> We have FAT OS (4GB) + Application run time (java, nodejs etc) + Created users + Created a directory + Installed the application right ? and what we have done in AMI ? while deploying catalogue ? We took 1 server + Configured the server using ansible like above all + Stop the server + Take AMI ---> This is nothing but Amazon Machine Image, we can use AMI image how many times we want, instead of taking one server and doing from the scratch, if image is ready, it is easy for us. Similarly docker image is also same, but the only difference when compared to docker image and container.
Docker image (like individual room) ---> We have Base OS (5MB-250MB) + Application run time (java, nodejs etc) + Created users + Created a directory + Installe the application ---> Total space used around 500MB.

### Working in DEV, but not working in PROD 
Main issue is configuration changes and OS, is if you use different OS in QA, UAT or PROD, but the advantage of docker image is we take same image from Dev to Sit, Uat, Prod. Thats why we call it as immutable image and portable, we even dont know what is the base OS we are using, but our intention is image should work.

### How to install docker in servers ?
- Create 1 server with (t2.micro) with 30GB
- Search in google "docker install for centos"
- Run the shown commands in the server with sudo su -
- When you install docker, a group called "docker" created, users who are in this group can access docker
  commands without root user. Users like centos should add in this group, then only commands like "docker ps"
  will work without root user, otherwise you must be root user.
- "usermod -aG docker centos" after this you need to logout and login again in server.

### Difference between Image (AMI) & Container (EC2 instance)
AMI is like physical thing, we have a memory in this, when you run AMI you will get EC2 instance, similarly Image is physical thing it has memory, configuration files etc. When you run the image we get container, that means container is the running version of image.

### Docker commands
- docker images ---> Show you the images exist in server
- docker pull nginx ---> Image will be pulled from "Docker Hub" here nginx image = Base OS + nginx 
- Bydefault it will pull the latest nginx (or) if you want you can give specific tags also, for example
  "docker pull nginx:stable-bullseye" etc.
- Now create container from the above created image, "docker create nginx:latest"
- To see only the running container "docker ps" to make run "docker start <container_id>"
- To remove "docker rm <container_id>" before you need to stop "docker stop <container_id>"
- "docker ps -a" ---> All containers with all status
- To remove images ---> "docker rmi <image_name>/id"
- To remove all images at a time ---> "docker images -a -q" then "docker rmi `docker images -a q`"
- Instead of Pull+Create+Run commands ---> "docker run nginx" to run in background "docker run -d nginx"

### Points to remember
- In virtualization VM ---> Cloud technologies are using VM-ware concept, a big physical server (for example
  16GB ram, 1TB HDD & CPU) will be there. We will divide this big server into multiple logical servers.
- Host OS ---> Windows ; VM-ware ---> We install Hypervisor software in Host OS ---> Guest OS
- In Guest OS ---> We can create multiple logical servers like below
- For Ubuntu ---> 1GB ram, Ubuntu, 100GB HDD (isolated from the other servers)
- For Centos ---> 1GB ram, Ubuntu, 100GB HDD (isolated from the other servers)
- For Fedora ---> 1GB ram, Ubuntu, 100GB HDD etc. (isolated from the other servers)
- This whole process is called "Resource utilization"
- When you create server in aws, it will create from the big physical server only, however these servers are
  isolated from the other servers and big physical server.
- Resource utilization is good in VM compared to physical servers, we can utilize 1 server fully.
- We also have "Dedicated Hosts" in aws, nothing but physical servers used by big companies.
- When we are moving to docker and kubernetes, we dont care what is the underline OS.
- Create an account for docker hub 
