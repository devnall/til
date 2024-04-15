# Git: Change default branch name (e.g. from "master" to "main")

If you need to change your default branch's name (e.g. change it from "master" to "main")...

First, rename it in your _local_ git repo:
1. `git checkout master`
2. `git branch -m master main`
3. `git status` and make sure it shows:
```
On branch main
Your branch is up to date with 'origin/master'.

nothing to commit, working tree clean
```

Then, rename the remote branch:
1. `git push -u origin main`
2. `git push origin --delete master`
Note: The push might get rejected, especially if you're using GitHub. If so, go to the repo's page, go to Settings, and update the default branch from "master" to "main". Then re-run the above command to delete the "master" branch.


Update local on any other systems where the repo is already checked out:
1. `git checkout master`
2. `git branch -m master main`
3. `git fetch`
4. `git branch --unset-upstream`
5. `git branch -u origin/main`
