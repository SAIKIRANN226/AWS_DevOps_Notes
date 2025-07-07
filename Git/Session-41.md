### Git (Global Information Tracker)
- It is nothing but a stupid content tracker, lets see how git will track using below example.
- echo "Hello world"
- Commit-ID ---> echo "Hello world" | git hash-object --stdin
- Commit-ID ---> Is called "SHA code" it has 40 chars (Universal unique ID) for the content.
- If you are storing any content like file or folder or repo in the Github, it has a SHA code.
- git log ---> Commit-ID of the entire content of that repo in github.
- Git is a Key-Value pair (commit-id = Key & content = Value), if you change the content, commit-id will also
  changes.
- So git will calculate commit-id depending on the content.
- We have ".git" folder in that only everything will be there like tracking.
- If you want the information about the commit-id then "git cat file <commit_id> -p"


### Protection rule in Git for main branch
- In Settings ---> Branches --> Add branch protection rule here, we have many rules but we choose according to
  the project, as of now we are selecting just two among them as a minimum protection to the main branch.
- One is "Pull request" and another one is "Require approvals" should be morethan 1
- And also "Dismiss stale pull request approvals when new commits are pushed" nothing but if once pull request is
  approved by reviewers, again who commits to the feature branch, it automatically will be unapproved.
- 
