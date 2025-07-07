### Git (Global Information Tracker)
- It is nothing but a stupid content tracker, lets see how git will track using below example.
- echo "Hello world"
- Commit-ID ---> echo "Hello world" | git hash-object --stdin
- Commit-ID ---> Is called "SHA code" it has 40 chars (Universal unique ID) for the content.
- If you are storing any content like file or folder or repo in the Github, it has a SHA code.
- git log ---> Commit-ID of the entire content of that repo in github.
- Git is Key-Value pair (commit-id = Key, content = Value) if you change content, commit-id will also change
- So git will calculate commit-id depending on the content.
- We have ".git" folder in that only everything will be there like tracking.
- If you want the information about the commit-id then "git cat file <commit_id> -p"
- If you want a commit-id for your content then echo "Hello world" | git hash-object --stdin

### Protection rule in Git for main branch
- In Settings ---> Branches --> Add branch protection rule here, we have many rules but we choose according to
  the project, as of now we are selecting just two among them as a minimum protection to the main branch.
- One is "Pull request" and another one is "Require approvals" should be morethan 1
- And also "Dismiss stale pull request approvals when new commits are pushed" nothing but if once pull request
  is approved by reviewers, again who commits to the feature branch, it automatically will be unapproved.
- Now create a branch ? git branch -M feature and add any content in this. When you "git log" you will get the
  commit-id like "68abb5...." 40 char SHA code, you still dint add anything in the feature branch, so main
  branch and feature branch commit-id will be same.
- When you add something in feature branch and do commit, and when you do "git log" then the commit-id will
  change from "68abb5..." to "78bcc...(something)" that means feature branch is moving forward with new
  commits.
- Working on the feature branch is completed now developer merge it through raising "pull request" by writing
  a meaningful message in the description.
- Next reviewers will approve in their github account.
- Once developer got approval, then he will get merge option, in this we have three options
- Create a merge commit, Squash and merge, Rebase and merge.
- If you merge, a merge commit-id will be created, if you take this merge commit-id, that means a main branch is one step forwarded, when you "git log" in main branch, 






### Points to remember
- If content changes then commid-id will also changes.
- git log --oneline ---> Will print commit-id in oneline.
- 
