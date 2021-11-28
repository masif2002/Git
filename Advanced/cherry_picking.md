# Cherry Picking

Cherry pick allows individual commits from other branch to be integrated with the main branch.

Generally, the complete branch is integrated with the master branch. But here, only the commit is integrated.

For example, when you accidentally commit to the _main_ branch instead of a _feature_ branch, you can use **_cherry pick_** to merge the commit from the main branch to feature branch.

## Workflow
1. Check out to the branch you actually want your commit to be
2. Copy the commit hash of the accidental commit you made on the main branch
3. And run the command
```
 git cherry-pick [hash]  
```  
  Now the accidental commit from main branch has been picked and committed in the branch, where you actually wanted it to be  

4. And as we learned before, we can clean up the master branch with the help of reset command 
```
git reset --hard HEAD~1
```