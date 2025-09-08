- What is Git and how it will track ?
- How to generate a commit-id for your content or file ? echo hello | git hash-object --stdin
- Git will calculate based on the content.
- Commit-id is also known as SHA code which has 40 characters (Universal unique id)
- git log --> You will get the commit-ids of the entire content of that repo in github.
- Git is a Key-Value pair (Key=commit-id, Value=content)
- If you want the information about the commit-id then "git cat-file <commit_id> -p"
- If you want all commit-ids in oneline ---> git log --oneline
- Protection rule in Git for main (or) master branch ?
- What is the minimum protection to the main branch ? PR, Require approvals, Require linear history, Dismiss
  stale pull request approvals when new commits are pushed.
- When you create a feature branch and you cloned the main branch. But still commit-ids of main branch &
  feature branch are same and why ? When will the commit-id of feature branch will change ?
- Once developers got approvals, he will get merge options like Merge commit, Squash and merge, Rebase and
  merge. These are nothing but merging strategies.
- Which merging strategies will be preferred among these three ?
- Most in companies go for the Merge commit, not Squash and Rebase why ?
- When to use Merge and when to use Rebase ?
- We are following feature branching strategy, we have main branch as long live branch, anything otherthan
  main branch we call it as feature branch, developers will work in feature branches, they will do CICD in
  feature branch itself, once it is successful they will raise PR, based on the discussions, PR will be
  approved and from the main branch, we do deployment into the higher environments QA, SIT, UAT, PROD.
- Once we got succeeded in merging code into the main branch, we can deploy into higher environments like QA,
  SIT, UAT, and PROD. What if we success in DEV and failed in QA ? what should i do ? again they should create
  another feature branch, they should change the code again in Dev environment and then do CICD.
- You will have ".git" folder in every repo, it stores all the information of git like tracking, metadata,
  objects etc. Everything will be stored in this folder only.
