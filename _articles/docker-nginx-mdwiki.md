---
layout: article
title: Docker Nginx mdwiki
description: Docker Nginx mdwiki
---
# Docker, Nginx, mdwiki
Docker uzerinde nginx server da statik bir websitesi yayinlamak
burada secilen statik websitesi altyapisi mdwiki denilen kucuk bir markdown viewer uzerinden yapilmisitr.
## Nasil Yapilir?
1. https://github.com/Dynalon/mdwiki adresinde acik kaynak olarak sunulan Wiki altyapisi download edilir.
2. Bilgisayarda static sayfalarin yayinlanacagi bir klasor olusutrulur. orn c:\website yada /Users/ahmet/website
3. Docker da asagidaki komut calistirilir.
_(Docker hakkinda bilgi almak icin [docker](http://www.filehoo.com) makalesini okuyabilirsiniz)_
Mac  OS icin
```beanshell
docker run -p 80:80 -v /Users/ahmet/website/:/usr/share/nginx/html nginx
```
Windows icin
```beanshell
docker run -p 80:80 -v c:\website:/usr/share/nginx/html nginx
```
4. Browser dan 192.168.99.100/mdwiki.html adresini girdiginizde calismasi gerekiyor,
bende calismamisti, browser dan console a baktigimda bazi sayfalarin eksik oldugunu gorup.
http://dynalon.github.io/mdwiki adresinden eksik sayfalari indirdim
   - http://dynalon.github.io/mdwiki/navigation.md tarayicidan farkli kaydet secip website klasorune kaydedebilirsiniz.
   - http://dynalon.github.io/mdwiki/config.json arayicidan farkli kaydet secip website klasorune kaydedebilirsiniz.
