### What is crontab and why it is useful ?
Crontab is used for scheduling the scripts and we will trigger to delete old log files everyday in our servers. Instead of logging manually and deleting old log files with .log extensions, we can delete using crontab. Crontab will target a particular directory, which consist of more than 14 days old with ".log" extension only, so crontab has a particular syntax, which consist of 5 stars like "5 4 * * *" go and check crontab guru website and you can see the examples provided in the website itself, just see the crontab 
linux example in the same website.

### Usage of crontab and giving the script location
"crontab -e" ---> Enter this command in the server in "cd", -e is editing & just enter 5 stars as of now and followed by script location ---> <stars_and_script_location>. This is the example of usage "* * * * * sh /home/centos/shell-script/15.delete-old-logs.sh" this line should be entered in the editor and script location generally we give absolute path and save the file :wq! To see the logs "tail -f /var/log/cron"  

### Shellscript optargs 18-greetings.sh
Generally we saw arguments to the shellscript like $1,$2 etc. Nothing but sending the arguments as options, lets say i have a script which is optargs called "greetings.sh" then optargs look like "greetings.sh -n saikiran" here -n is the command line options or optargs or options arguments, it is our wish to give or not as args like -n <name> or -w <wishes> etc. Instead of just "sh greetings.sh sai" then you will get "Hello sai how are you", we can use optargs look like "sh greetings.sh -n sai -w "good_morning"

### Shellscript as a Native linux command
If you want to run the shellscript as a native command linux instead of "sh 18-greetings.sh" we have path for every operating system "echo $PATH" nothing but if you install any softwares in these PATHS then automatically windows (or) linux will pick up from this PATH, so you need to keep script in that PATH, generally if you put your script in "/usr/local/bin" you NO need to give ".sh" while running the script. So "sudo cp 18-greetings.sh /usr/local/bin/greeting (copied as a greeting name), and you need to give executive access by "sudo chmod +x /usr/local/bin/greeting", now if you are in any folder otherthan the script folder just run by using name "greeting" (or) greeting -n sai -w "good evening", do this steps in "cd 18-greetings.sh location"

### Automating the creation of aws instances and route53 records
- Till now we created ec2 instance manually. Like if Mongodb,mysql,shipping then t3.small, remaining t2.micro
  along with the route53_records, if web then Public_IP, if not web then Private_IP right ?
- So instead of logging into aws console and creating instances, we can create using "aws command line"

So now we need to write a script to automate, using "aws command line" nothing but creating instances from aws command line instead of aws console, before this we need to have authentication, we have IAM in this IAM we have Authentication and Authorization. In every server we have aws command line, below are the two processes.

- Authentication --> You have username/password,you can go to common area in the company
- Authorization ---> You need to prove your authorization to enter in to the project bays, in other words like
  permissions,different permissions for TL,Manager,Sr,Engineer etc. We call these as ROLES, these roles will be
  changing every year (or) few years after, Persmissions are tagged to these roles, below is the example.

1. Team Manager ---> Has super admin
2. Team Lead ---> Has admin
3. Senior Engineers ---> Normal access
4. Trainee ---> Just read access 

### Authentication 
Here User is a person and he has Username/Password (or) Key

### Authorization
Here Role and Permissions, what is the role of user ? and what are the Persmissions attached to that role

### Permissions
- We have nouns and verbs.
- We have resources in aws ---> Ec2,vpc,route53,cdn,IAM etc. In this resources we have
- Nouns ---> web,catalogue,cart,hostedzone etc.
- Verbs (or) actions ---> create resource,update,delete nothing but CRUD.

### We can give authorization like below
- Sivakumar(Trainee) ----> EC2(resource) ---> Web(instance) ---> READ access only.
- Manish(Junior DevOps) ----> EC2(resource) ---> Web(instance) ---> READ and UPDATE access only.
- Mahesh(Senior Engineer) ---> EC2(resource) ---> Web(instance) ---> READ and "CRU" access not delete.
- Aditya(Team Lead) ----> EC2(resource) ---> All instances ---> READ and "CRU" access only not delete.
- Suman(Team manager) ----> EC2(resource) ---> All instances ---> READ and "CRUD" including delete.

Not only for persons, resources should also have access to access another resource, For that we have "roles to resources" like for example if you have created one EC2 and this EC2 instance should go and create other new instances (or) route53 records, so we need to give role to the EC2 by going to IAM click on roles create role and select EC2 as a use case/next/amazonEc2fullaccess/

### Command to create instance 
"aws ec2 run-instances --image-id ami-xxxxxxxx --count 1 --instance-type t2.micro --security-group-ids sg-903004f8". You will get error "Unable to locate credentials, you can configure by "aws configure". So Create one user and then configure it by going to IAM/Users/Create_user/Attach_policies_directly/Administrator
Access/Click_on_the_created_user/Security_credentials/Create_accesskey/CLI and then "aws configure". Now try to create instance using above command in server. Here if it is a person he can keep Access_key & Secret_keys safely, but what if EC2 can keep these credentials secretly ? If anybody has access to this EC2 he can able to see these credentials using ls -la in cd .aws/ in credentials. So thats why create a role for EC2 by going to IAM/roles/create_role/select EC2 in usecase/you can give admin access also (or) amazonEc2 full access and also give route53 full access/give a role name/. Now select the already created instance & Actions/Security/Modify IAM role/Select your created role, so that this Ec2 instance will create another EC2 instances and also update route 53 records aswel for that only we have created role to the instance EC2, if you get the same error remove the old credentials which was created for aws console in .aws folder by using rm -rf command.

### Go through the "roboshop.sh" file in Roboshop-Shellscript
- This file will create all instances and route53 records from the command line without logging into the aws.

### We can improve the script like below
- If web get Public_IP and create records.
- Check if records already exists, If exists update, If not exists then create.

### Points to remember
- To see the logs of crontab "tail -f /var/log/cron" 
- One Ec2 is creating another instances, we have two ways. a) Create one user and aws configure. b) Create a
  role and attach to this instance.
- Go through "roboshop.sh" in VS.
- Tag specifications is used to give names of the instances automatically.
- --query is to get the PrivateIP of the instances.
- Important point So overall create any one instance and give a role to it, so that it will create multiple
  instances from this instance only, you need to clone the "roboshop-shellscript" in this server and run the
  "roboshop.sh" script.
