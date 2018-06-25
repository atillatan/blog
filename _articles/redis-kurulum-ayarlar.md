---
layout: article
permalink:
name:
file_type:
title: Redis kurulumu ve ayarlari
description: >-
  Redis kurulumu ve ayarlari
tags:  
category:  
sort_order: 100
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
# Redis kurulumu ve ayarları

- Öncelikle Redis bilgisayara kurulur

- Değiştirilen ayarlar aşağıdaki şekildedir.
- Redisin konfigürasyon dosyası açılır

```bash
# ilk kurulumda daha detayli log gormek isteyebilirsiniz
loglevel debug
# log dosyasini, herzaman rahatlikla ulasabileceginiz ve
# diski doldurma ihtimali olmayan bir yere kaydedin.
logfile "f:\\Redis\\logs\\Redis.log"
# Kac adet databse olmasini istiyorsaniz
databases 2
```
- Log'u verbose yapıp detayları görmek lazım
- Windows ta test yapıyorsanız ve "Sistem log"'u yes, ise windows event log'larına yazıyor dikkat etmek lazım.
- Windows serverlarda, Servisin Konfigürasyonunda windows event leri daha kullanışlı olabilir.

## Memory i kaydetme işlemleri iptal edildi
Redis ilk kurulduğunda, default ayarlarla kurulduğu için, bazı özellikler
faklı makina kaynaklarına uygun olmayabilir. örneğin redis periyodik olarak database lerini
diske kaydedebilmektedir. Eğer bu ayar açık olursa ve redise ayrılan memory alanı büyük olursa,
belirli periyotlarda redisin tıkandığını görebilirsiniz.

```bash
# save 900 1
# save 300 10
# save 60 10000
```

## heapdir lokasyonu değiştirildi.
```bash
  heapdir "d:\\Redis\\"
```

Eger redisi production a kuruyorsaniz, yuksek bir memory ayari yapmak isteyebilirsiniz.

- Redis in kullanacağı max memroy aşağıdaki şekilde ayarlanabilir.
```bash
maxheap 64GB
```

- Veritabanı dosyasının nerede olduğu ayarlanmalıdır, dosylarin kaydedilecegi disk te en az memory kadar boş olması lazım

- Eğer ./ adresinde yeterince yer yoksa maxheap değeri düşürülebilir, yada ./ adresi değiştirilebilir.
```bash
dir "f:\\Redis\\"
```


- Windows sürümü https://github.com/ServiceStack/redis-windows sayfasından indirilebilir.
- Son sürüm için bir ayar yapmaya gerek kalmıyor. Default ayarlarda duzenleme yapilmis "Redis-lates"

- Windowsta deneme yaparken, komut satırından Redis-server.exe ye konfigürasyon dosyasının adı verilerek deneme yapılabilir.



# servis olarak kurmak için

Redis-server --service-ınstall Redis.windows.conf --loglevel verbose
