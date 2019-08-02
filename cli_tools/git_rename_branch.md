# Renaming a git branch (both local and remote)
1. `git branch -m old-name new-name` - Rename local branch
1. `git push origin :old-name new-name` -  Delete the old-name remote branch and push the new-name local branch
1. `git push origin -u new-name` - Reset the upstream branch for the new-name local branch

Alternately:
1. `git branch -m old_branch_name new_branch_name` - Rename local branch
1. `git push origin :old_branch_name` - Delete the old remote branch
1. `git push --set-upstream origin new_branch_name` - Push the new branch, set local branch to track the new remote
