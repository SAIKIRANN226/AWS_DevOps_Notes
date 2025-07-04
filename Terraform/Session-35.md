### 3-Tier architecture diagram
![infra](https://github.com/user-attachments/assets/747c7e17-2f4a-4aa6-b2d1-bf8bbf363371)
Start a project "Roboshop-infra-Dev" in VS, this is for Dev environment, as this is multi-env, you have three options like Tfvars-method, Workspaces-method and Different repos for different env's, present siva is now creating different folders for different env's. Every method has pros and cons, you can tell this in interview. We also need to create for Sit,Uat,Prod also. So any project starts with VPC. Gothrough the resources in VS.






### Points to remember
- Auto-scaling is only for web and app tier apps, for Database we use RDS,DynamoDB etc.
- Keeping "sg.yaml" file is just to understand the how the connection is happening.
- Ansible PUSH is nothing but ansible server itself pushing the configuration to the nodes.
- Ansible PULL is nothing but nodes itself PULL go the ansible server and pull the configuration.
- We have one disadvantage that it is possible for anybody to disturb the configuration by logging manually.
- In ansible PULL architecture we can schedule a crontab to pull the configuration periodically from git and
  run it, anyhow ansible implemented idempotency in nature, so no problem even if we runs the configuration
  multiple times.
- 


