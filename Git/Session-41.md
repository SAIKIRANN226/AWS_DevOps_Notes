### Git (Global Information Tracker)
- It is nothing but just a stupid content tracker, lets see how git will track using below example.
- echo "Hello world" (or) echo "Hello world" | git hash-object --stdin (you will get a commid-id)
- Commit-ID ---> Is called "SHA code" it has 40 chars (universal unique ID) for the content.
- If you are storing any content like file (or) folder (or) repo in Github, it has a SHA code.
- git log ---> Commit-ID of the entire content of that repo in github.
- Git is a Key-Value pair (Key=commit-id, Value=content)
- If you change content, commit-id will also changes.
- So git will calculate commit-id depending on the content.
- We have ".git" folder in that only everything will be there like tracking etc.
- If you want the information about the commit-id then "git cat-file <commit_id> -p"

### Protection rule in Git for main branch
- In Settings ---> Branches --> Add branch protection rule here, we have many rules but we choose according to
  the project, as of now we are selecting just two among them as a minimum protection to the main branch.
- One is "Pull request" and another one is "Require approvals" (should be morethan 1)
- We have another option also in protection rule that is "Require linear history", then we can only use
  "rebase" option not "git merge & commit" or "squash" options.
- We have another option "Dismiss stale pull request approvals when new commits are pushed" nothing but if
  once pull request is approved by reviewers, again who commits to the feature branch, it will automatically
  be unapproved.
- Now create a branch ? git branch -M feature and add any content in this. When you "git log" you will get the
  commit-id like "68abb5..." 40 char SHA code, you still dint add anything in the feature branch, so main
  branch and feature branch commit-ids will be same.
- When you add something in feature branch and do commit and when you do "git log" then the commit-id will
  change from "68abb5..." to "78bcc4...(something)" that means feature branch is moving forward with new
  commits.
- Once working on the feature branch is completed, now developer merge it through raising "pull request" by
  writing a meaningful message in the description.
- Next reviewers will approve in their github account.
- Once developer got approval, then he will get merge option, in this we have three options.
- Create a Merge commit, Squash and merge, Rebase and merge. These are nothing but merge strategies.
- If you merge, a merge commit-id will be created, if you take this merge commit-id, that means a main branch
  is one step forwarded, when you "git log" in main branch, if you "git cat-file <cfaa64> -p" then you will
  get few information like tree, parent-ids, author (who commited this) etc.

### Merge commit
When you are merging from one branch to another branch an extra or new merge commit-id will be created always, that have 2 parents, if you take the latest parent commit and do "git cat-file <6b0a63> -p" then it will show the previous commit-id, that means merge will preserve the complete history, it is like chain structure.

### Rebase and merge
When you create another branch, commit new lines and push it to the github, when you do "git log --oneline" you will get a commit-id for this, you will get commit-ids until you finish development, and raise a pull request. Once the approvals are ok, then you have other option in merge section that is "Rebase and merge" so NO extra commits and commit-ids will be changing (rewrites the history). That means in rebase it will not preserve the history.

### Squash and merge
For example in microservices, 1 small feature is developed by 1 developer, that sprint time will be like 2 weeks, if this developer do 60 commits to the main branch, is that good to see ? so he will squash that 60 commits into a single commit. Both squash and rebase are same, which one you will prefer ? we can prefer squash rebase, because it will merge into one single commit, so that we cannot pollute the repo. Which one to use among these three options in merging strategy is purely based on the project.

### When to use "Merge" and When to use "Rebase" ?
- If a branch is developed by mulitple developers, prefer merge because when multiple persons are developing
  we should preserve the history to know who is doing what changes.
- If only one person is developing one feature, then he can use rebase, generally in companies people go for
  the merge option only, however we have advantages in rebase like in microservices development.

### Branching strategy
- Main branch ---> Long live branch.
- Feature branch ---> Short live branch, we can delete this after merging.
- Developers create feature branches, once they complete development, they will raise PR and merge/rebase into
  main branch.
- So where the CICD should takeplace in this branching strategy ?
- In feature branch only, before raising PR, lets do CICD in Dev environment, if CICD is success, then only
  feature branch is completed. Now you can raise PR and then merge/rebase into main branch.
- Code is same across all environments, but configuration is different.
- Configuration should be dettached from the code, since we are storing configuration in SSM Parameter.
- Once we got succeeded in merging code into the main branch, we can deploy into other environments like QA,
  SIT, UAT, and PROD. If we success in DEV and failed in QA, what should i do ? again they should create
  another feature branch, they should change the code again in Dev environment, and then do CICD.
  
### Points to remember
- If content changes, then commid-id will also changes.
- git log --oneline ---> Will print commit-id in oneline.
- We are following feature branching strategy, we have main branch as long live branch, anything otherthan
  main branch we call it as feature branch, developers will work in feature branches, they will do CICD in
  feature branch itself, once it is successful they will raise PR, based on the approvals and discussions that
  will be approved and from the main branch we do deployment into the higher environments like QA, SIT, UAT
  and PROD environments.
- If we got emergency, we can just test in "Dev" env and then directly go for the "Prod" env.
- You will have ".git" folder in every repo, it stores all the information of git like tracking, metadata,
  objects etc. Everything will be stored in this folder only.
- If you want to generate a commit-id for your content then use "echo hello | git hash-object --stdin"
