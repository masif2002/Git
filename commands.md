# Git Commands

```
git init
```
Intializes git in the current path

---


```
git clone [SSH link of the remote repo]
```  
Clones the remote repository into your local machine


---
## Add & Commit

```
 git add [filename]
```
Tracks the file (tracks the changes you've made)

* Using . instead of filename will track all the files that have not been tracked

---

```
git status  
```   
Displays the status of the files.

---


```
 git commit -m "Commmit Title" -m "Some Description"
```

Commits the changes (saves changes locally)

---
```
 git commit -am "Title" -m "Desc"
```

Adds the file and commits it. Works only with modified files.

  * New files need to be added seperately before committing.

---

```
git remote add origin [SSH link of the remote repo] 
```
Connects to the remote repository
* *origin* is actually the location of our git repository

---
```
git remote - v
```
Checks if the connection has been established to the repository

---
```
git push -u origin master
```

Pushes all the committed files to the **master** branch in the remote repository

 * -u sets the default push location to _origin master_
---
```
git push
```
Pushes directly to _origin master_ since the default location has been set to it in the previous command.

---
---
## Branching

```
git branch
```
Displays all branches in the local repository

---
```
  debug
  feature
* master
```
Current branch is indicated with *

---

```
git branch -d [branch]
```
Deletes the specified branch.

---
```
git checkout -b [branch_name]
```
Creates a new branch with the given name

---
```
git checkout [branch]
```
Switches to the specified branch

---
```
git diff
```
Shows the difference in code after changing but before tracking

---
## Merging


```
git pull origin master
```
Pulls the merged master file from the remote repository to the local machine


---
```
git merge [branch]
```
Merges the given branch to the main branch

---
---
## Reset

```
git reset [filename]
```
Resets all the changes in file that has been tracked but not yet committed

---
```
git reset
````
Reset command without the filename resets all the files that have been modified

---
```
git reset HEAD~1
```
This command undoes the commit.  
It actually resets the pointer which is currently pointing to **HEAD** (the latest commit) and sets it to **HEAD-1**

---
```
git log 
```
Displays the log of all the commits  
* Adding `--oneline` flag will display a shorter version of the commits, each per line

----


```
commit fcac5d13beb1390b5c7feee3cac17fef010632a0 (HEAD -> master)
Author: Mohamed Asif <mohamedasif.masif@gmail.com>
Date:   Mon Nov 22 17:02:34 2021 +0530

    Final Commit

commit f9e7f9d938d782653fb6cb7dbaf55bf34ff64e21   // Hashkey
Author: Mohamed Asif <mohamedasif.masif@gmail.com>
Date:   Mon Nov 22 16:26:54 2021 +0530

    Modified README.md

commit bf527ab209d2016ed4cd6bbc0577aa46446221de (origin/master)
Author: Mohamed Asif <mohamedasif.masif@gmail.com>
Date:   Mon Nov 22 16:22:13 2021 +0530

    Created index.html
```
Above, we can see 3 commits of a sample git log

---
```
git reset [hashkey]
```
Resets to the commit with the specified hashkey.  
 * Hashkeys of commits can be found in the first line of every commit in _git log_

---
```
git reset --hard [hashkey]
```
Resets to the commit specified and also deletes all the commits after the current one
___
---
