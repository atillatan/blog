---
layout: article
title: TFS ile Otomatik deployment yapmak
description: TFS ile Otomatik deployment yapmak
---

# TFS ile Otomatik deployment yapmak

Tfs ile scheduled yada check-in ile tetikelenen build yada deployment islemi yapilabilmektedir.


## MsBuild icin build.xml yapmak.



## TFS uzerinde Build Agent kurulumu


## Build scriptiin TFS icinden calistirilmasi
TFS icerisinden "Exec" secilerek "bat" dosyasi calistirilabilir
`<Exec Command="OBS-V3-main-20141124-Patch-Prod.bat $(Configuration)"/>`


## Deployment sonucunun mail olarak TFS kullanicilarina gonderilmesi

- Gonderilen dosya dan "Release notes" cok rahat cikartilabilir.
