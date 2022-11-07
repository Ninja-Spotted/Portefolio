---
title: "Git"
parent: C code
permalink: "/c/git"
layout: default
---

### Version Control Systems

A version control system (VCS) is a software tool used to track and manage changes to a filesystem, often used in collaborative work.  
Nowadays, one of the most used VCS is Git, used via remote repositories like GitHub, GitLab or BitBucket.

#### Git Characteristics

- On the same project every repository has the same data (if up-to-date)
- Faster than other VCS
- Space used is minimized on local and push/pull data transfers
- Simple and large userbase and excelent tools

#### Git Commands

Git comes with a wide variety of commands that appear overwhelming, but just like linux, the syntax is well defined and compreensive. Some of them are:

- `git clone <https://name-of-the-repository-link>`  
"Clones", or rather, download existing source code from a remote repository, making an identical copy of a version of a project on your computer.
- `git branch <branch-name>`  
Makes a **local** branch, allowing several people to work in parallel on the same project.
- `git push -u <remote> <branch-name>`  
To upload/push it to the remote repository (as a branch).
- `git branch or git branch --list`  
Use this command to see all the existing branches inside a project.
- `git branch -d <branch-name>`  
This is used to delete a branch from a project.
- `git checkout <name-of-your-branch>`
Another often used command is checkout, since it allows the user to switch between branches.  
For this to work: Changes **must** be commited or stashed and the following branch should exist.
- `git status`  
Gives information such as if the branch is up-to-date, if there is anything to commit, push or pull, or files staged, unstaged or untracked or even created, modified or deleted.
