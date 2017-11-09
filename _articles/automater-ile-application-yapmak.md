---
layout: article
permalink:
name:
file_type:
title:  Automater ile application yapmak
description: >-
   Automater ile application yapmak
tags:  
category:  
sort_order: 100
rating: 100
changefreq: monthly
priority: 0.5
published: true
create_date: 2017-10-23
modified_date: 2017-10-23
created_by: atilla
modified_by: atilla
comments: true
redirect_url:
---
---

# Automater

## bir sh script calistirmak

- Automater acilir.
- New document secilir.
- Application secilir.
- Soldaki menuden "Run shell script" secilir.
- shel script icine asagidaki gibi bir calistirma scripti yazilir.
```
cd /Users/atilla/Applications/Aqua\ Data\ Studio\ 18.0
sh datastudio.sh >& /dev/null &
```
- Wine ile bir executable acmak
```
cd /Users/atilla/apps/Everything
/usr/local/bin/wine Everything.exe >& /dev/null &
```
- Dokuman program.app olarak sh scriptinin yanina kaydedebiliriz.
- File/Export secilerek programi istedigimiz yere kaydedebiliri.
