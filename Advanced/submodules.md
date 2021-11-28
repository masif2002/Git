# Submodules

You can add a submodule to your git repository by
```
git submodule add [URL of the repo] 
```

* The submodule is a fully featured git repository 
* Actual contents of the submodule are not stored in the parent repository
* The parent repo only stores the submodule's configuration.. ie-
  + The remote URL
  + Local path inside the main project
  + Checked out revision

## Edge Case

When you clone a repository that contains submodules, the files of the submodules won't be present as we have learnt earlier that a parent repository does not store a submodule's content but only it's configuration. 

So for cloning a repo with submodules, we use the following command. 

```
git clone --recurse-submodules [URL of the repo]
```
This command initialises all the submodules automatically after cloning

## Checked Out Revision

When you checkout from a branch (A), then the last commit on this branch is the checked out revision on the new branch (B). And as you add commits to the new branch (B), the latest commit is the checked out revision.

But, a submodule git repository is checked out on a specific commit. When a new commit happens, the checked out commit does not change.