### Roboshop-Infra-Dev (CICD for project infra)
In previous session, like i said we can also write Jenkinsfile for project infra also right ? and also we wrote Jenkinsfile for VPC. Now create the whole project infra using same method instead of doing manual process like using terraform commands init, plan and apply. So create by writing 1 Jenkinsfile to all the project infra. If there is NO dependency from one folder to another folder like 04-databases and 05-app-alb. For that we have "Parallel stages" in Jenkins pipeline (we need to use keyword called parallel) so because of this parallel, both resources will create at a time to save the time. Other folders like VPC, SG, VPN have dependencies (like it is following sequential process). We can also keep plan command also if you want.

### Roboshop-Infra-Dev (CICD for catalogue)
Now go for catalogue application (already created in the previous session from "Shared library" in multi branch pipeline)

### Project management (or) Ticketing tool (Jira or Service now)
Here also we raise CR by keeping  project code, application code, approvals, date & time, version, deployment process, revert back process, post deployment testing and attaching test results, attach scanning results, we mention Dev, Sit, Uat status, Jenkins build URLs. We need to mention the screenshots of results. After rasing this we will get ticket id for JIRA and also we mention CR number also after rasing CR request below

### Change management process
We will raise CR (change request) every organization have their own tool to manage CR. DevOps team will raise CR in this CR ticket we have project code, application code, approvals, date and time, version, deployment process, revert back process, post deployment testing, JIRA id. Then this ticket will rise or it will go into new status. First this new status go to the team lead will check the JIRA ticket id, he will write some comments and approve. Secondly this go to the delivery manager, he also writes some comments and approve, then goes to the client.

### Jira to Jenkins Integration
JIRA team will do this, in JIRA we have a button "trigger prod" then JIRA will check CR is approved or not, prod trigger time is same as in CR. Then it will trigger Jenkins pipeline







































### Points to remember
- Interview question ? Explain the CICD architecture in your project ?
- Go through the CICD in concepts folder
