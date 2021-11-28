# Reflog
 
Basically, a log of head pointers. It keeps track of every movement of the head pointer.

Head pointer in _reflog_ points to every action done in the repository.

## Uses
* To recover deleted commits
* To recover deleted branches

```
git reflog
```
Displays the log of head pointers
```
d6e5515 (HEAD -> master) HEAD@{0}: rebase (finish): returning to refs/heads/master
d6e5515 (HEAD -> master) HEAD@{1}: rebase (pick): Modified index
d05c035 HEAD@{2}: rebase (pick): an updated commit msg
636cf09 HEAD@{3}: rebase (reword): ok
079f10e (feature) HEAD@{4}: rebase: fast-forward
570276a HEAD@{5}: rebase (start): checkout 570276a
6d6b02a HEAD@{6}: rebase (finish): returning to refs/heads/master
6d6b02a HEAD@{7}: rebase (start): checkout 570276a
6d6b02a HEAD@{8}: rebase (finish): returning to refs/heads/master
6d6b02a HEAD@{9}: rebase (start): checkout 570276a
6d6b02a HEAD@{10}: rebase (finish): returning to refs/heads/master
6d6b02a HEAD@{11}: rebase (start): checkout 570276a
6d6b02a HEAD@{12}: checkout: moving from feature to master
079f10e (feature) HEAD@{13}: reset: moving to 079f10e
d1bc289 HEAD@{14}: checkout: moving from master to feature
6d6b02a HEAD@{15}: checkout: moving from master to master
6d6b02a HEAD@{16}: checkout: moving from feature to master
d1bc289 HEAD@{17}: checkout: moving from master to feature
6d6b02a HEAD@{18}: checkout: moving from master to master
6d6b02a HEAD@{19}: cherry-pick: Modified index
7329cbd HEAD@{20}: checkout: moving from feature to master
d1bc289 HEAD@{21}: commit: Modified index
....
```
A sample reflog can be  seen above

## Recovering a deleted commit

Checking the current set of commits and deleting the recent one

```
$ git log --oneline
f336f60 (HEAD -> master) Added newline to readme1.md
12e0c03 Added newline to readme2.md
7e0963b Combined 3 n 4 
9f77873 Added newline to readme5.md
a5a6d88 Created 5 readme files
5a98e41 Created readme1.md

$ git reset --hard 12e0c03
HEAD is now at 12e0c03 Added newline to readme2.md

$ git log --oneline
12e0c03 (HEAD -> master) Added newline to readme2.md
7e0963b Combined 3 n 4
9f77873 Added newline to readme5.md
a5a6d88 Created 5 readme files
5a98e41 Created readme1.md
```
**Step 1:** Choose the action from the reflog where you deleted the commit and go back one action, copy the hash of it.
```
12e0c03 (HEAD -> master) HEAD@{0}: reset: moving to 12e0c03
f336f60 HEAD@{1}: rebase (finish): returning to refs/heads/master
f336f60 HEAD@{2}: rebase (start): checkout a5a6d88
f336f60 HEAD@{3}: rebase (finish): returning to refs/heads/master
f336f60 HEAD@{4}: rebase (start): checkout 5a98e41
f336f60 HEAD@{5}: rebase (finish): returning to refs/heads/master
f336f60 HEAD@{6}: rebase (start): checkout 5a98e41
...
```
Here, in the above example, we copy _f336f60_ 

---
**Step 2:** Use the reset command 

```
git reset --hard [hashkey]
```
Now, the commit would be successfully restored which can be verified from the commit log

```
$ git log --oneline
f336f60 (HEAD -> master) Added newline to readme1.md
12e0c03 Added newline to readme2.md
7e0963b Combined 3 n 4
9f77873 Added newline to readme5.md
a5a6d88 Created 5 readme files
5a98e41 Created readme1.md
```

## Recovering a deleted branch

We've deleted the _feature_ branch in this example.
```
$ git reflog
12e0c03 (HEAD -> master) HEAD@{0}: checkout: moving from feature to master
12e0c03 (HEAD -> master) HEAD@{1}: checkout: moving from master to feature
12e0c03 (HEAD -> master) HEAD@{2}: reset: moving to 12e0c03
f336f60 HEAD@{3}: reset: moving to f336f60
f336f60 HEAD@{4}: reset: moving to HEAD
f336f60 HEAD@{5}: reset: moving to f336f60
12e0c03 (HEAD -> master) HEAD@{6}: reset: moving to 12e0c03
```
So we copy the hash of the second action where we switch to the _feature_ branch and restore the branch using the command
```
git branch [branch_name] [hashkey]
```
Now, let's restore our _feature_ branch and verify it.
```
$ git branch feature 12e0c03

$ git branch
  feature
* master
```
Deleted branch _feature_ is recovered successfully :)


