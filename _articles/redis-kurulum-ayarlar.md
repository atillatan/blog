---
layout: article
permalink:
name:
file_type:
title: Redis Kurulumu ve ayarlari
description: >-
  Redis Kurulumu ve ayarlari
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
# Redis Kurulumu ve ayarlari

- degistirilen ayarlar asagidaki sekildedir.

loglevel debug
logfile "f:\\redis\\logs\\redis.log"
databases 2
## Memeory i kaydetme islemleri iptal edildi
```
# save 900 1
# save 300 10
# save 60 10000
```

## heapdir lokasyonu degistirildi.
  heapdir "d:\\redis\\"

- redis in kullanacagi max memroy ayarlanabilir.
maxheap 8GB


- veritabani dosyasinin nerede oldugu ayarlanmalidir, c de en az memory kadar bos olmasi lazim
- eger ./ adresinde yeterince yer yoksa maxheap degeri dusurulebilir, yada ./ adresi degistirilebilir.

dir "f:\\redis\\"


- yeni susumr github/servicestack/windows-redis sayfasindan indirildi.
son surum icin bir ayar yapmaya gerek kalmiyor. "redis-lates"
- komut satirindan redis-server.exe ye configurasyon dosyasinin adi verilerek deneme yapilabilir.
logu verbose yapip detaylari gormek lazim
- sistem logu yes, ise windows event larina yaziyor dikkat etmek lazim.
- servisin configurasyonda windows event leri daha kullanisli olabilir.

# servis olarak kurmak icin


redis-server --service-install redis.windows.conf --loglevel verbose
