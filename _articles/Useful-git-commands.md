---
layout: article
permalink: 
name: 
file_type: 
title: Useful Git Commands
description: >-
  Useful Git Commands
tags:  
category:  
sort_order: 170
rating: 100
changefreq: monthly
priority: 0.5
published: true
create_date: 2017-12-03T00:00:00.000Z
modified_date: 2017-12-03T00:00:00.000Z
created_by: atilla
modified_by: atilla
comments: true
redirect_url: 
toc: false
---

# Useful git commands

## 1. Create a Repository
```bash
# Show configuration
$ git config -l  

# From scratch, Create a local Repository
$ git init

# Download from an existing repository
$ git clone repo_url

# add all changes to statege
$ git add .
$ git commit -m 'description'  #commit staged changes to git repsository
$ git push # push changes to remote repository. sadece remote repository varsa kullanilir. local de calisirken gerek yok.

```
### 2. Observe your Repository 

```bash
#list new or modified files not yet committed
$ git status

# Show the changes to files not yet staged
$ git diff

# Show the changes to staged files
$ git diff --changed

# Show all staged and unstaged file changes
$ git diff HEAD

# Show the changes between two commit ids
$ git diff commit1 commi2

# List the change dates and authors for file
$ git blame [file]

# Show the file changes for a cimmit id and/or file
$ git show [comit]:[file]

# Show full changes history
$ git log

# Show change history for file/directory including diffs
$ git log -p [file/directory]

# Adding remote origin for local repository
$ git remote add origin git@github.com:atillatan/blog.git
$ git push -u origin master
```

### 3. Working with Branches

```bash
# List all local branches
$ git branch

# List all branches local and remote
$ git branch -av

# Creaging a branch
$ git branch gh-pages
$ git push origin gh-pages

# Switch to a branch and update working directory
$ git checkout gh-pages

# Delete the branch
$ git branch -d gh-pages

# merge branch_a into branch_b
$ git checkout branch_b
$ git merge branch_a

# Merge selected branch to master
$ git checkout gh-pages
$ git merge master

# Tag the current commit
$ git tag my_tag
 
```
### 4. Syncronize - Reset

```bash
# Get the latest changes from origin (no merge)
$ git fetch

# Fetch the latest changes from origin (with merge)
$ git pull

# Fetch the latest changes from origin and rebase
$ git pull --rebase

# Push the local changes to the origin
$ git push

# Unstage file, keeping the file changes
$ git reset [file]

# revert everything to the last commit
% git reset --hard
```

### 5. Change user

```bash
# kullanici degistirmek
$ git config --global user.name "username"
$ git config --global user.email "mail"
$ git config --global credential.email "mail"
```

### 6. Finally

```bash
# when in doubt, use git help
$ git command --help
# or visit https://training.github.com/
```