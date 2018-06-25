---
layout: article
permalink:
name:
file_type:
title: Online Proje Dokumantasyonu, Docker, Nginx, mdwiki
description: >-
  Online Proje Dokumantasyonu, Docker, Nginx, mdwiki
tags: docker
category:  
sort_order: 30
rating: 100
changefreq: monthly
priority: 0.5
published: true
create_date: 2017-10-23T00:00:00.000Z
modified_date: 2017-10-23T00:00:00.000Z
created_by: atilla
modified_by: atilla
comments: true
redirect_url:
---
# Online Proje Dokumantasyonu, Docker, Nginx, mdwiki
Docker uzerinde nginx server da statik bir websitesi yayinlamak
burada secilen statik websitesi altyapisi mdwiki denilen kucuk bir markdown viewer uzerinden yapilmisitr.
## Nasil Yapilir?
1. https://github.com/Dynalon/mdwiki adresinde acik kaynak olarak sunulan Wiki altyapisi download edilir.
2. Bilgisayarda static sayfalarin yayinlanacagi bir klasor olusutrulur. orn c:\website yada /Users/ahmet/website
3. Docker da asagidaki komut calistirilir.
_(Docker hakkinda bilgi almak icin [docker](/docker-cok-kullanilan-komutlar/) makalesini okuyabilirsiniz)_

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
   - http://dynalon.github.io/mdwiki/config.json tarayicidan farkli kaydet secip website klasorune kaydedebilirsiniz.

- Projenizde dokumantasyonu markdown formatinda yaparsaniz, dokumanlari markdown formatinda yayin yapan herhangi bir sunucuda yayinlayabilirsiniz, IIS ile kullanacaksaniz mdwiki cok guzel bir aractir.  linux te yayin yapacaksaniz nginx yada apache kullanabilirsiniz.
Ayrica, projeniz acik kaynak ise,  dokumantasyonu github pages te de yayinlayabilirsiniz.

- Markdown formatinda dokumantasyon, dokumanlarin tarihcesinide tutar.
- TFS, SVN, GIT gibi repository araclarinda otomatik build ayarlayip, periyodik olarak dokumantasyonun publish edilmesini
saglayabilirsiniz, bu sayade proje calisanlar farkli versiyonlardaki dokumanlari email yolu ile paylasma zahmetinden kurtulur.

- Proje dokumantasyonu icin kullanilan ornek bir wiki sayfasi asagidadir.

 ![1.png]({{site.img}}/wiki/1.png)
