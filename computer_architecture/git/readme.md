---
title: "Git"
parent: Computer Architecture
permalink: "/computer_architecture/git"
layout: default
---

### Version Control Systems

A version control system (VCS) is a software tool used to track and manage changes to a filesystem, often used in collaborative work.  
Nowadays, one of the most used VCS is Git, used via remote repositories like GitHub, GitLab or BitBucket.

#### Git Characteristics

- On the same project every repository has the same data (if up-to-date)
- Faster than other VCS
- Space used is minimized on local and push/pull data transfers
- Simple, large userbase and excelent tools

#### Git Commands

Git comes with a wide variety of commands that appear overwhelming, but just like linux, the syntax is well defined and compreensive. Some of them are:

- Git Clone
  - `git clone <https://name-of-the-repository-link>`  
  "Clones", or rather, download existing source code from a remote repository, making an identical copy of a version of a project on your computer.
- Git Branch
  - `git branch <branch-name>`  
  Makes a **local** branch, allowing several people to work in parallel on the same project.
  - `git push -u <remote> <branch-name>`  
  To upload/push it to the remote repository (as a branch).
  - `git branch or git branch --list`  
  Use this command to see all the existing branches inside a project.
  - `git branch -d <branch-name>`  
  This is used to delete a branch from a project.
- Git Checkout
  - `git checkout <name-of-your-branch>`  
  Another often used command is checkout, since it allows the user to switch between branches.  
  For this to work: Changes **must** be commited or stashed and the following branch should exist.
- Git Status
  - `git status`  
  Gives information such as if the branch is up-to-date, if there is anything to commit, push or pull, or files staged, unstaged or untracked or even created, modified or deleted.
- Git Add
  - `git add <file>` and `git add -A`  
  If a file is created, modified or deleted, changes will only occur locally unless they are included in the commit.
- Git Commit
  - `git commit -m "commit message"`  
  It is one of the most used commands of Git and it allows the creation of "checkpoints" as it saves the changes made and makes possible to go back if needed.  
  By itself, it only __saves changes locally__.
- Git Push
  - `git push <remote> <branch-name>` and `git push --set-upstream <remote> <name-of-your-branch>`  
  After commiting, the next step is to send the changes to the remote server.
- Git Pull
  - `git pull <remote>`  
  This command get updates from the remote repository into your local repository.
- Git Revert
  - `git revert <hash code>`  
  This is the safer way to undo changes and avoid deletion, first checking the commit history with `git log -- oneline`. This adds a new commit without deleting the reverted commit, so it will still appear in the history.  
  Since everything happens in the local system, unless pushed, it is safer to use and prefered.
- Git Merge
  - `git merge <branch-name>`
  When development is complete and everything works, the final step is merging with the parent branch (dev or master), basically integrating the branch with all commits into the parent. For example (feature branch into the dev branch):
  `git checkout dev` -> Switch to dev branch  
  `git fetch` -> Update local dev branch  
  `git merge <branch-name>` -> Merging branch into dev
  
#### Basic Workflow

1. Start a new repository: `git init`
2. Edit files
3. Stage the changes: `git commit -a` or `git add <file>`
4. Review changes: `git status`
5. Commit the changes

#### This page was written in 20/11/2022 and last updated in 20/11/2022.
