### What is Git and why is it used in DevOps ?
Git is a distributed version control system used to track changes in code. In DevOps, it provides collaboration, rollback, and code history. Since every developer has a local copy, work continues even without connectivity. It’s essential for CI/CD pipelines, infrastructure as code, and managing large teams across projects.

### What are the differences between Git and SVN or other centralized VCS ?
- Git is Distributed, every developer has full history, offline commits possible.
- SVN/Centralized VCS is Central server required, offline work limited, slower branching/merging.
- In DevOps, Git is preferred due to speed, scalability, and flexibility.

### Explain the difference between git fetch, git pull, and git clone ?
- git fetch: Downloads latest commits from remote but doesn’t merge.
- git pull: Fetch + merge into current branch.
- git clone: Creates a copy of the remote repo locally with full history.

### What is the difference between git merge and git rebase ?
- Merge will Creates a new commit combining histories, keeps branch history intact.
- Rebase will Moves commits on top of another branch, creating a cleaner linear history.
- In DevOps, rebasing is used for cleaner commits, while merge is safer for preserving history.

### How do you resolve Git conflicts ?
To resolve merge conflicts, I run git status to identify conflicted files, then edit them manually to keep the correct changes. After resolving, I run git add and git commit (or git rebase --continue if rebasing)
- Run git status to identify conflicted files.
- Manually edit files to resolve conflicts.
- Mark resolution with git add <file> and commit.
- Use tools like git mergetool or IDE integrations.
- In CI/CD pipelines, I prefer rebasing often and keeping PRs small to reduce conflicts.

### How do you undo a commit that has been pushed to a shared branch ?
Use git revert <commit-hash> → creates a new commit that undoes the change.

### How do you handle multiple environments (Dev, Staging, Prod) using Git ?
Separate branches for different environments.
