---
layout: article
title: Automater ile application yapmak
description: Automater ile application yapmak
comments: true
sortorder: 100
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
