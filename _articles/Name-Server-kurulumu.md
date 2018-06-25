---
layout: article
permalink: null
name: null
file_type: null
title: Name Server Kurulumu
description: Name Server Kurulumu
tags: System
category: null
sort_order: 120
rating: 100
changefreq: monthly
priority: 0.5
published: true
create_date: 2017-15-13T10:20:00Z
modified_date: 2017-15-13
created_by: atilla
modified_by: atilla
comments: true
redirect_url: null
---

# Name Server Kurulumu

Amaç : herhangi bir yerden aldigimiz alan adinin sorumlu DNS inin degistirilmesidir.

Normalde alan adi aldigimiz sirketler aldigimiz alan adinin "name server" kayitlarina kendi DNS lerini yazarlar,
fakat bizim burda amacimiz, alan adini aldigmiz sirketin, aldigimiz alan adlari için,
alan adindan sorumlu "Name Server" olarak bizim DNS imizin IP sini yazmasidir.

Bu bize ne saglar? bu bize Internette tanimli bir DNS saglayici olanagi saglar bu sayede aldigimiz bütün alan adlarini kendi
"Name Server" umuza yönlendirebiliriz, istedigimiz alan adina sub domain ekleyebiliriz mx kaydi ekleyebiliriz.
alan adi ile aklimiza gelen her türlü isi biz yapmis oluruz.

Örnek:

Bize ait 3 tane alan adi olsun, bunlarin hepsini www.netsol.com dan aldigimizi düsünelim

Alan Adi NS(DNS)
sirket1.com ns1.netsol.com,ns2.netsol.com
sirket2.com ns1.netsol.com,ns2.netsol.com
sirket3.com ns1.netsol.com,ns2.netsol.com

Seklinde 3 alan adi almis olalim, bunlardan biri için NS (Name Server) tanimlayalim.

ns1.sirket1.com 68.78.88.98 (bizim sabit IP adresli DNS server)
ns2.sirket1.com 68.78.88.98 (bizim sabit IP adresli DNS server)

Simdi yukardaki aldigmiz 3 alan adinin NS (Name Server) kayitlarini bizim tanimladigimiz ile degistirelim

Alan Adi NS (DNS)
sirket1.com ns1.sirket1.com, ns2.sirket1.com
sirket2.com ns1.sirket1.com, ns2.sirket1.com
sirket2.com ns1.sirket1.com, ns2.sirket1.com

Bu sayede, internette herhangi birisi, "www.sirket2.com" a ulasmak istediginde,
"sirket2.com" alan adindan sorumlu DNS, root DNS lere sorulur. root DNS lerden baslayan bu sorgulama isi
sonuçta bizim DNS sunucumuza kadar gelirler. Sorumlu DNS bizim DNS imiz oldugundan dolayi, simdi "www" host'unun
IP adresi sorulur, biz DNS sunucumuzda "www" host'una hangi IP'yi tanimlamissak direkt olarak o IP numarasi verilir.

Önemli Not: Yukarda bazi degisikleri yaptiktan sonra yaptim ama olmadi, yada yapamiyorum gibi düsünmeyin çünkü
bu islemler den bazilari 1 dk ile 24 saat arasinda degisen bir sürede internet üzerinde aktiflesir.

örnegin.
sirket2.com alan adinin NS kaydina ns1.sirket1.com yazdiniz diyelim bu islemin aktif olmasi 24 saat sürer.
