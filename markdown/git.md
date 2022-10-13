```yaml
title: Git
date: 12-Oct-2022
tags:
    - github
    - gitlab
    - version
    - VCS
categories:
    - Linux Command
intro: This cheat sheet summarizes commonly used Git command line instructions for quick reference.
```

**Table of Contents**

<!-- vscode-markdown-toc -->
* 1. [Create a Repository](#CreateaRepository)
* 2. [Make a change](#Makeachange)
* 3. [Configuration](#Configuration)
* 4. [Working with Branches](#WorkingwithBranches)
* 5. [Observe your Repository](#ObserveyourRepository)
* 6. [Synchronize](#Synchronize)
* 7. [Remote](#Remote)
* 8. [Temporary Commits](#TemporaryCommits)
* 9. [Tracking path Changes](#TrackingpathChanges)
* 10. [Ignoring Files](#IgnoringFiles)
* 11. [Rename branch](#Renamebranch)
* 12. [Log](#Log)
* 13. [Branch](#Branch)
* 14. [Commit](#Commit)
* 15. [Git Aliases](#GitAliases)

<!-- vscode-markdown-toc-config
	numbering=true
	autoSave=true
	/vscode-markdown-toc-config -->
<!-- /vscode-markdown-toc -->

Getting started 
---------------

###  1. <a name='CreateaRepository'></a>Create a Repository
Create a new local repository
``` shell script
$ git init [project name]
```

Clone a repository 
``` shell script
$ git clone git_url
```

Clone a repository into a specified directory
``` shell script
$ git clone git_url my_directory
```




###  2. <a name='Makeachange'></a>Make a change 
Show modified files in working directory, staged for your next commit
``` shell script
$ git status
```

Stages the file, ready for commit
``` shell script
$ git add [file]
```

Stage all changed files, ready for commit
``` shell script
$ git add .
```

Commit all staged files to versioned history
``` shell script
$ git commit -m "commit message"
```

Commit all your tracked files to versioned history
``` shell script
$ git commit -am "commit message"
```

Unstages file, keeping the file changes
``` shell script
$ git reset [file]
```

Revert everything to the last commit
``` shell script
$ git reset --hard
```

Diff of what is changed but not staged
``` shell script
$ git diff
```

Diff of what is staged but not yet commited
``` shell script
$ git diff --staged
```

Apply any commits of current branch ahead of specified one
``` shell script
$ git rebase [branch]
```


###  3. <a name='Configuration'></a>Configuration

Set the name that will be attached to your commits and tags
``` shell script
$ git config --global user.name "name"
```

Set an email address that will be attached to your commits and tags
``` shell script
$ git config --global user.email "email"
```

Enable some colorization of Git output
``` shell script
$ git config --global color.ui auto
```

Edit the global configuration file in a text editor
``` shell script
$ git config --global --edit
```



###  4. <a name='WorkingwithBranches'></a>Working with Branches

List all local branches
``` shell script
$ git branch
```

List all branches, local and remote
``` shell script
$ git branch -av
```

Switch to my_branch, and update working directory
``` shell script
$ git checkout my_branch
```

Create a new branch called new_branch
``` shell script
$ git checkout -b new_branch
```

Delete the branch called my_branch
``` shell script
$ git branch -d my_branch
```

Merge branchA into branchB
``` shell script
$ git checkout branchB
$ git merge branchA
```

Tag the current commit
``` shell script
$ git tag my_tag
```



###  5. <a name='ObserveyourRepository'></a>Observe your Repository
Show the commit history for the currently active branch
``` shell script
$ git log
```
Show the commits on branchA that are not on branchB
``` shell script
$ git log branchB..branchA
```
Show the commits that changed file, even across renames
``` shell script
$ git log --follow [file]
```
Show the diff of what is in branchA that is not in branchB
``` shell script
$ git diff branchB...branchA
```
Show any object in Git in human-readable format
``` shell script
$ git show [SHA]
```



###  6. <a name='Synchronize'></a>Synchronize

Fetch down all the branches from that Git remote
``` shell script
$ git fetch [alias]
```

Merge a remote branch into your current branch to bring it up to date
``` shell script
$ git merge [alias]/[branch]
# No fast-forward
$ git merge --no-ff [alias]/[branch]
# Only fast-forward
$ git merge --ff-only [alias]/[branch]
```

Transmit local branch commits to the remote repository branch
``` shell script
$ git push [alias] [branch]
```

Fetch and merge any commits from the tracking remote branch
``` shell script
$ git pull
```

Merge just one specific commit from another branch to your current branch
``` shell script
$ git cherry-pick [commit_id]
```




###  7. <a name='Remote'></a>Remote
Add a git URL as an alias
``` shell script
$ git remote add [alias] [url]
```

Show the names of the remote repositories you've set up
``` shell script
$ git remote
```

Show the names and URLs of the remote repositories
``` shell script
$ git remote -v
```

Remove a remote repository
``` shell script
$ git remote rm [remote repo name]
```

Change the URL of the git repo
``` shell script
$ git remote set-url origin [git_url]
```






###  8. <a name='TemporaryCommits'></a>Temporary Commits

Save modified and staged changes
``` shell script
$ git stash
```

List stack-order of stashed file changes
``` shell script
$ git stash list
```

Write working from top of stash stack
``` shell script
$ git stash pop
```

Discard the changes from top of stash stack
``` shell script
$ git stash drop
```




###  9. <a name='TrackingpathChanges'></a>Tracking path Changes
Delete the file from project and stage the removal for commit
``` shell script
$ git rm [file]
```

Change an existing file path and stage the move
``` shell script
$ git mv [existing-path] [new-path]
```

Show all commit logs with indication of any paths that moved
``` shell script
$ git log --stat -M
```


###  10. <a name='IgnoringFiles'></a>Ignoring Files

```
/logs/*

# "!" means don't ignore 
!logs/.gitkeep

/# Ignore Mac system files
.DS_store

# Ignore node_modules folder
node_modules

# Ignore SASS config files
.sass-cache
```
A `.gitignore` file specifies intentionally untracked files that Git should ignore



Git Tricks 
------

###  11. <a name='Renamebranch'></a>Rename branch 
- #### **Renamed** to `new_name`
    ```shell script
    $ git branch -m <new_name>
    ```
- #### **Push** and reset
    ```shell script
    $ git push origin -u <new_name>
    ```
- #### **Delete** remote branch
    ```shell script
    $ git push origin --delete <old>
    ```



###  12. <a name='Log'></a>Log
Search change by content
```shell script
$ git log -S'<a term in the source>'
```
Show changes over time for specific file
```shell script
$ git log -p <file_name>
```
Print out a cool visualization of your log
```shell script 
$ git log --pretty=oneline --graph --decorate --all
```

###  13. <a name='Branch'></a>Branch 
List all branches and their upstreams 
```shell script
$ git branch -vv 
```
Quickly switch to the previous branch
```shell script
$ git checkout -
```
Get only remote branches
```shell script
$ git branch -r
```
Checkout a single file from another branch
```shell script
$ git checkout <branch> -- <file>
```



###  14. <a name='Commit'></a>Commit
Rewrite last commit message
```shell script
$ git commit -v --amend
```


###  15. <a name='GitAliases'></a>Git Aliases
```cmd
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.st status
```
See also: [More Aliases](https://gist.github.com/johnpolacek/69604a1f6861129ef088)
