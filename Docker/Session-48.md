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
Physical severs (laptop) ---> Virtualization (VM) ---> Containerization

For example in Guest OS, we have created one For Centos ---> 1GB ram, Ubuntu, 100GB HDD. But application is used only 0.1GB of ram, 10GB of HDD, remaining space is wasted right ? So this is nothing but virtualization VM concept right ? and here Hypervisor is blocking remaining space, that means resource utilization is not that much better. So in this VM only we have Containerization concept, nothing but we have containers installed in this VM, containers are isolated from each other (similar to the individual rooms example) but system resources (centos ---> 1GB ram, Ubuntu, 100GB HDD) are shared, that means containers will take resources based on demand from this system resources. System resources will dont block. Boot time is very less (with in seconds) compared to VM (EC2 instance)














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
