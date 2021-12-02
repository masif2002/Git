# Interactive Rebase
 
A tool for optimizing and cleaning up your commit history but only on your local machine. It is not meant for remote repositories

## Uses:

+ Change a commits message
+ Delete commits
+ Reorder commits
+ Combine multiple commits into one
+ Edit/Split existing commits to multiple ones

## Workflow

### Step 1:  Determine the range of commits you want to manipulate
---
For example,
```
$ git log --oneline

6d6b02a (HEAD -> master) Modified index.html
7329cbd Added notes.md
f9e7f9d Modified README.md
bf527ab Created index.html
ff8181b Created New Rep

```
From above, If you want to manipulate the 3rd commit, you will have to copy the hash of the 4th commit to the clipboard and use it in **_Step 2_** 

### Step 2: Run command with specified range
---
You need to run:
```
git rebase -i [hashkey]
```

Or you also can use the head pointer, where _n_ th commit is the commit you want to manipulate
```
git rebase -i HEAD~n
```
Then, an editor window containing the range of commits will pop up.
> The hashkey used for the example is _bf527ab_
```
pick f9e7f9d Modified README.md
pick 7329cbd Added notes.md
pick 6d6b02a Modified index.html

# Rebase bf527ab..6d6b02a onto bf527ab (3 commands)
#
# Commands:
# p, pick <commit> = use commit
# r, reword <commit> = use commit, but edit the commit message
# e, edit <commit> = use commit, but stop for amending
# s, squash <commit> = use commit, but meld into previous commit
# f, fixup [-C | -c] <commit> = like "squash" but keep only the previous
#                    commit's log message, unless -C is used, in which case
#                    keep only this commit's message; -c is same as -C but
#                    opens the editor
# x, exec <command> = run command (the rest of the line) using shell
# b, break = stop here (continue rebase later with 'git rebase --continue')
# d, drop <commit> = remove commit
# l, label <label> = label current HEAD with a name
# t, reset <label> = reset HEAD to a label
# m, merge [-C <commit> | -c <commit>] <label> [# <oneline>]
# .       create a merge commit using the original merge commit's

```
Here, in this window, you only need to choose _what to do_ with the commits, _not change it_ in this window.  

  To choose what to do with the commits, specific action keywords are used which is present as comments above, in the editor window  
  For Example:
  + reword - is used to *_rewrite_* a commits message.
  + squash - is used to *_combine_* the commit with the one above it in the editor window.


```
reword f9e7f9d Modified README.md  
pick 7329cbd Added notes.md
pick 6d6b02a Modified index.html

# Rebase bf527ab..6d6b02a onto bf527ab (3 commands)
#
# Commands:
# p, pick <commit> = use commit
# r, reword <commit> = use commit, but edit the commit message
# e, edit <commit> = use commit, but stop for amending
# s, squash <commit> = use commit, but meld into previous commit
# f, fixup [-C | -c] <commit> = like "squash" but keep only the previous
#                    commit's log message, unless -C is used, in which case
#                    keep only this commit's message; -c is same as -C but
#                    opens the editor
# x, exec <command> = run command (the rest of the line) using shell
# b, break = stop here (continue rebase later with 'git rebase --continue')
# d, drop <commit> = remove commit
# l, label <label> = label current HEAD with a name
# t, reset <label> = reset HEAD to a label
# m, merge [-C <commit> | -c <commit>] <label> [# <oneline>]
# .       create a merge commit using the original merge commit's

```

### Step 3: Manipulate the commit
---

After finishing *Step 2* another window will pop up
```
Modified README.md

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# Author:    Mohamed Asif <masif2002@outlook.com>
# Date:      Mon Nov 22 17:00:53 2021 +0530
#
# interactive rebase in progress; onto bf527ab
# Last command done (1 command done):
#    reword f9e7f9d Added exlamation at line3 q
# Next commands to do (2 remaining commands):
#    pick 7329cbd Added notes.md
#    pick 6d6b02a Modified index.html
# You are currently editing a commit while rebasing branch 'master' on 'bf527ab'.
#
# Changes to be committed:
#       modified:   index.html
#

```
This is the window where you will **_actually_** manipulate the commit! ie - In our case, rewrite the commit message
```
Commit message rewritten

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# Author:    Mohamed Asif <masif2002@outlook.com>
# Date:      Mon Nov 22 17:00:53 2021 +0530
#
# interactive rebase in progress; onto bf527ab
# Last command done (1 command done):
#    reword f9e7f9d Added exlamation at line3 q
# Next commands to do (2 remaining commands):
#    pick 7329cbd Added notes.md
#    pick 6d6b02a Modified index.html
# You are currently editing a commit while rebasing branch 'master' on 'bf527ab'.
#
# Changes to be committed:
#       modified:   index.html
#

```
> Since the default editor window opens in **_vim_**, here are some vim commands  
> * **_i_** - for _insert_  
> * **_Esc_** - to come out of the editing interface
> * **_:x!_** - for save and exit

You can also push the changes to the remote repository by
```
git push --force origin master
```

