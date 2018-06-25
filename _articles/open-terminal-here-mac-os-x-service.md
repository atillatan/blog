---
layout: article
permalink:
name:
file_type:
title: Open terminal here mac os x service
description: >-
  Open terminal here mac os x service
tags:  
category:  
sort_order: 90
rating: 100
changefreq: monthly
priority: 0.5
published: true
create_date: 2017-10-23 00:00:00 +0000
modified_date: 2017-10-23
created_by: atilla
modified_by: atilla
comments: true
redirect_url:
---

# Open terminal here with Mac OS X service

## Open terminal here solution


Making service/context menu on Mac OS with

- OS X Services available in contextual menus, for instance when you right-click on a file or folder in the Finder.
- It’s easy to create your own service commands using any shell or scripting commands.

### How to make open terminal here in 4 steps

- Step-1 Launch Automator and when asked to choose a type for your document select “Service”.

![1.png]({{site.img}}/osxservices/1.png)

- Step-2 From the library on the left select “Run Shell Script” action.

![2.png]({{site.img}}/osxservices/2.png)


- Step-3 Set the following Services parameters:

```
Service receives: Folders
In: Finder.app
Shell: /bin/bash
```
Paste the below scritp

```bash
open -a /Applications/Utilities/Terminal.app $1
```


![3.png]({{site.img}}/osxservices/3.png)

The Services files you create are stored in the following directory:
```
~/Library/Services/
```


## Other Context menu or Mac OS X services implementations

### 1- Open with wine (For windows executables)

```bash
/usr/local/bin/wine $1 >& /dev/null &
```

### 2- New text file here

```bash
cd $1
touch NewTextFile.txt
open -a /Applications/TextEdit.app NewTextFile.txt
```

### 3- Edit with TextEdit

```bash
open -a /Applications/TextEdit.app $1
```


- Open live-serve here (it opens terminal and show command result)
- Jekyll serve here (it opens terminal and show command result)
- Git pull (it opens terminal and show command result)
- Git push (it opens terminal and show command result)


![4.png]({{site.img}}/osxservices/4.png)


[Download services](/downloads/services.zip)
