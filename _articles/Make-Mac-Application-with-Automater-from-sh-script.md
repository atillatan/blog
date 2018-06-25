---
layout: article
permalink:
name:
file_type:
title:  Make Mac Application with Automater from sh script
description: >-
   Make Mac Application with Automater from sh script
tags:  
category:  
sort_order: 100
rating: 100
changefreq: monthly
priority: 0.5
published: true
create_date: 2017-10-23T10:20:00Z
modified_date: 2017-10-23
created_by: atilla
modified_by: atilla
comments: true
redirect_url:
---
---

# Make Mac Application with Automater from sh script

## How to run sh script with Automater

- Open spotlight with "CMD+Space", type "Automater"
- Click File/New and select "Application"

![1.png]({{site.img}}/automater/1.png)


- Find "Run shell script" from left menu, and double click
- Write your script like as below.

```
cd /Users/atilla/Applications/Aqua\ Data\ Studio\ 18.0
sh datastudio.sh >& /dev/null &
```

- Open some windows application with wine


```
/usr/local/bin/wine /Users/atilla/apps/Winamp/winamp.exe >& /dev/null &

```
- You can export these scripts as  App with File/Export
- After you can double click on "yourapp.app"  
