---
layout: post
comments: true
title:  "Git Basics"
date:   2023-03-29 00:04:58 +0530
categories: general
---

### 1. Git command
```sh
git init
git help init
git commit
Git reflog
git log
git log --all --graph --decorate : show the log w.r.t to <HEAD>
git checkout <hash>
 git cat-file -p <hash>: explore the status of commit
git diff hello.txt or git diff HEAD hello.txt
git tag : show the tag associated to repo
```
```sh
git stash

stash   meaning hidden storage
git stash: stash the uncommitted changes
git stash list: show all the stashes
git stash apply: apply the top stash
git stash apply n
git stash apply stash@{n}
git stash pop == git stash apply && git stash drop
git stash drop n
git stash clear
```

### 2. Branching and merging

```sh
git checkout hello.txt : discard the changes
git branch -vv : shows local branches
git branch -a : shows all branches including remote
git branch -d <BRANCH> : delete the branch locally 

git branch <branch name> && git checkout <branch name>
or git checkout -b <branch name>


git merge <branch> : merge with HEAD     git merge --abort
git add <file>
git merge --continue
```

### 3. Merge with develop branch
```sh
git checkout develop 
git pull -p 
git checkout feature_branch 
git merge develop 
git push origin feature_branch
```

### 4. Git clean
Remove the untracked file
```sh
git clean -n (check which files will be removed, it will not remove ignored file as well as directory)
git clean -n -x -d (it will show remove all untracked file including dir, gitignored and file)
git clean - - force -x -d (it forcefully removed the untracked file)
```

### 5. Remote
```sh
git remote add <name><url> 
e.g. git remote add origin ../remote

git push <remote><local branch>: <remote branch>
e.g. git push origin master:master

git branch --set-upstream-to = origin/master
```

### 6. Clone
```sh

git clone <url> <destination>
e.g git clone ./remote demo2

git fetch && git merge : fetch and merge to the file
git pull : alternate for fetch and merge
```

### 7. Git config
```sh
git config or vim ~/.gitconfig
```
### 8. How to remove already committed file in git
- Remove a file you already pushed to the git repository
```sh
git rm –cached name_of_file
```
- Remove a file you accidentally committed in your last commit (but haven’t pushed yet)
```sh
git reset --soft HEAD^1
git rm --cached <file-name>
```
