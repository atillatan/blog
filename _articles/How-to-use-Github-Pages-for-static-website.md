---
layout: article
title: How to use Github Pages for static website
description: How to use Github Pages for static website
comments: true
sortorder: 40
---

# How to use Github Pages for static website


- You can turn your Github  repository into a page very easily
- How do we do this in 3 steps

## Step-1: Create your local git repository

```bash
# Create folder
$ mkdir blog
$ cd blog
# git initiation and commit index.html
$ git init
$ touch index.html
# you can write some html into index.html
$ git add .
$ git commit -m 'init'
$ git status


```

## Step-2: Create your remote Github repository and push your local repository into Github repository.
- Open www.github.com and click "+" button in the Github page then type your "new repository" name like "blog", after that click "Create Repository" button.
- Open terminal and push an existing repository to Github
```bash
$ git remote add origin git@github.com:atillatan/blog.git
$ git push -u origin master
```

## Step-3 Create your "gh-pages" branch

- "gh-pages" is a special name for github, this branch is hosted up at github.  

```bash
# Create branch
$ git branch gh-pages
$ git push origin gh-pages
```

That's it, you can navigate your gitgub page [https://your_github_username.github.io/blog](https://atillatan.github.io/blog)


## Next step: You're probably going to want to have your own custom domain name.
- How do we do this?

```bash
# create CNAME file for custom domain name
$ touch CNAME
# open CNAME file with nano editor
$ nano CNAME
# in the nano editor type your custom domain name (tanrikulu.biz) and save the CNAME file

$ git add .
# commit CNAME file to the master branch
$ git commit -m 'cname'
# switch gh-pages branche
$ git checkout gh-pages
$ git merge master
$ git push

```
after that you can change  your DNS settings.
in the DNS settings replace your A record IP address with github pages IP address
```
192.30.252.153
192.30.252.154
```

you can navigate your custom domain name with your browser.
