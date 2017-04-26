# Convert a cloned git repo to a fork

If you clone a repo and realize you want it to be a fork instead:

1. Fork their repo on GitHub
2. In your local, rename your origin remote to upstream:
`git remote rename origin upstream`
3. Add a new origin pointing to your fork:
`git remote add origin git@github...my-fork`
4. Fetch and push
`git fetch origin`
`git push origin`
