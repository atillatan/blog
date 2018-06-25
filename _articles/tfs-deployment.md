---
layout: article
permalink:
name:
file_type:
title: TFS ile Otomatik deployment yapmak
description: >-
  TFS ile Otomatik deployment yapmak
tags:  
category:  
sort_order: 190
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

# TFS ile Otomatik deployment yapmak

Tfs ile scheduled yada check-in ile tetikelenen build yada deployment islemi yapilabilmektedir.


## MsBuild icin build.xml yapmak.



## TFS uzerinde Build Agent kurulumu


## Build scriptiin TFS icinden calistirilmasi
TFS icerisinden "Exec" secilerek "bat" dosyasi calistirilabilir
`<Exec Command="BranchName-Prod.bat $(Configuration)"/>`


## Deployment sonucunun mail olarak TFS kullanicilarina gonderilmesi

- Eger projede her check-in isleminde talep numarasi ve yapilan islem yaziliyor ise
 Gonderilen mail den "Release notes" cok rahat cikartilabilir.
