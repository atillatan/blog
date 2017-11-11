---
layout: article
permalink:
name:
file_type:
title: Docker Cok kullanilan komutlar
description: >-
  Docker Cok kullanilan komutlar
tags:  
category:  
sort_order: 30
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
# DOCKER



## Cok kullanilan komutlar

- Docker bilesenleri versionlarini gondermek

```bash
$ docker --version
Docker version 1.12.3, build 6b644ec

$ docker-compose --version
docker-compose version 1.8.1, build 878cff1

$ docker-machine --version
docker-machine version 0.8.2, build e18a919

```

- `docker images` image listelemek, hub.docker.com dan indirilen images lardir.
image i silmek baska bir sey, container i silmek baska birseydir.
container lari local de biz olusturruz sileriz
- `docker rmi <imageid>` image silmek
- `docker ps` Calisan Container lari gosterir
- `docker stop <containerid>` Calisan Cotainer lari durdurmak
- `docker run -d -p 80:80 --name webserver nginx`  Start service, create container image
- `docker stop webserver` stop container
- `docker start webserver`  : starting service
- `docker ps -a` :  stop olmus container lari da gosterir.
- `docker stop $(docker ps -a -q)`  tum container lari stop eder
- `docker rm $(docker ps -a -q) `  Delete all containers
- `docker rmi $(docker images -q)` Delete all images
- `docker-machine ls` calisan docker engine bilgisini gosterir.
- `docker-machine start default` default olan docker machine start edilir
- `docker-machine start default` default olan docker machine stop edilir
- `docker-machine env` docker-machine ortam bilgilerini gosterir.
- docker-machine i manuel baslatmak icin
`docker-machine start`
`docker-machine env`
`eval $(docker-machine env)`
komutlari calistiriliri.
- docker-machine e baglanmanin 2 yolu vardir.
   1. `docker-machine ssh default` seklinde docket-machine e ait olan cli komutu ile.
   2. `ssh docket@192.168.99.100` pass:tcuser

- `docker-machine config`
- `docker-machine env`
- `docker-machine inspect`
- `docker-machine ip`
- `docker-machine kill`
- `docker-machine provision`
- `docker-machine regenerate-certs`
- `docker-machine restart`
- `docker-machine ssh`
- `docker-machine status`
- `docker-machine upgrade`
- `docker-machine url`
- `docker run -it ubuntu bash` ubuntu bash calistirilir.
- `docker run -d -p 80:80 --name webserver nginx`  nginx imaji kullanilarak webserver adinda bir container olusturur ve calistirir, `-d` deamon olarak yani servis olarak calismasini saglar `-p` ise portu belirten parametredir. `:` ile kullanildiginda ilk configurasyon host a ikincisi ise docker servisine aittir.
- bir container a ssh ile baglamak, usiswiki adli containera baglaniyoruz

```beanshell
bash -c "clear && DOCKER_HOST=tcp://192.168.99.100:2376 DOCKER_CERT_PATH=/Users/atilla/.docker/machine/machines/default DOCKER_TLS_VERIFY=1 docker exec -it usiswiki sh"
```

- Kitematik programini kullanarak ta container lara baglanabilirsiniz.
- ssh ile baglanmanin diger yolu OpenSSH kurmak olabilir
- `docker run --name usiswiki -p 80:80 -v $(pwd):/usr/share/nginx/html -d nginx` usiswiki adinda bir container olusturur ve onu calistirir `-v` parametresi host taki bir directory yi tamemen container a yansitmaktadir. mapleme isi yapilmaktadir.
- `:ro` readonly demektir. `-v` parametresinden sonra kullanilir, bir directory maplendiginde sanal makinanin bu directory ye readonly erismesini saglar.
- Dockerfile : docker image olusturmak icin kullanilan dosyadir, bu dosyanin oldugu klasorde
- `docker build -t imagename .` komutu verildiginde **imagename** adinda bir image olusturulur.
sonundaki . nokta bulundugu klasoru ifade eder
- `docker run --name containername -P -d imagename`  bir image dan container olusturup calistirmak.
- `docker run -i -t --volumes-from containername --name imagename debian /bin/bash` dockerfile da VOLUME maping var ise volume lara ulasmak icin

```bash
docker build -t nginximage1 .
docket images
docker run --name nginxcontainer1 -P -d nginximage1
docker ps
docker run -it --volumes-from nginxcontainer1 --name nginxvolumecontainer1 debian /bin/bash
```

- Mounting files

```bash
docker run --name nginx-container \
  -v /path/to/static/files/on/host:/usr/share/nginx/html:ro \
  -v /path/to/conf/on/host:/etc/nginx/nginx.conf:ro \
  -P -d nginx
```

yada

```bash
docker run --name nginx-container \
  -v $(pwd)/html:/usr/share/nginx/html:ro \
  -v $(pwd)/nginx.conf:/etc/nginx/nginx.conf:ro \
  -P -d nginx
```

- interaktif olarak loglari gondermek `-it`

```bash
docker run -it --name nginx-container \
  -v $(pwd)/html:/usr/share/nginx/html:ro \
  -v $(pwd)/nginx.conf:/etc/nginx/nginx.conf:ro \
  -P nginx bash
```

### Ozet olarak 4 adimda nginx kurulumu yapilabilir

1. Dockerfile olusturulur, icinde FROM ifadesinde docker hub taki hangi image kullanilacagi bildirlirlir.

```bash
FROM nginx
RUN echo "runing command"
VOLUME /usr/share/nginx/html
VOLUME /etc/nginx
```

2. `docker build -t nginximagename .` seklinde image olusturulur, olusan image `docker images` komutu ile gorulebilir.
3. image kullanilarak container olusturulur ve run edilir.
`docker run -it --name usiswikicontainer -v $(pwd)/src:/usr/share/nginx/html:ro -v $(pwd)/nginx/nginx.conf:/etc/nginx/nginx.conf:ro -P -d nginximagename`  
veya
`docker run -it --name wiki1 -p 8181:80 -v /Users/atilla/WP/usiswiki/src/:/usr/share/nginx/html/ -v /Users/atilla/WP/usiswiki/nginx/nginx.conf:/etc/nginx/nginx.conf:ro -P -d usiswikiimage`
4. sonraki calistirma ve kapatma islemleri su sekulde yapilir.

```bash
docker start usiswikicontainer
docker stop usiswikicontainer
```

- `docker network ls`

- `docker run --name mysqlc1 -p 3306:3306 -e MYSQL_ROOT_PASSWORD=123 -d mysql` mysql container olusturmak `-e` parametresi environment variable vermek oluyor.

- `docker exec ...` container icinde komut calistiriyor.
- `docker exec -it mysqlc1 bash`


- Widows ta docker in networke acilmi var fakat mac te yok, -p parameteresine host ip adresi de eklenerek yapiliyor.
`-p 192.168.2.3:80:8080` gibi

- image olusturma dosyasi `Dockerfile` container olusturma dosyasi ise `.yml`

### Ozet

host: Docker machine in kurulu oldugu bilgisayardir.
Dockre machine: bir sanal maikandir ve container lari calistirir. adresi: 192.168.99.100:2370
image : sanal makina imajlaridir.
container: image dan kopyalanmis sanal makinalardir.

sonuc olarak docker-machine icinde containerler calisir.
herbir container bir nNIC network kartina sahiptir ve bunlar
docker machine uzerindeki vSwitch e baglidir. switch e disardan gelen trafik 192.168.99.100 uzerinden gelir.
portuna gore icerdeki bir sanal makinaya yonlendirilir.
bu durumda her port bir servis yada sanal makina olarak dusunulebilir


### Hangi Driver

Docker asagidaki driverlari destekler

Amazon Web Services
Microsoft Azure
Digital Ocean
Exoscale
Google Compute Engine
Generic
Microsoft Hyper-V
OpenStack
Rackspace
IBM Softlayer
Oracle VirtualBox
VMware vCloud Air
VMware Fusion
VMware vSphere
parallels

host isletim sistemine gore hangisinin kullanilacagina karar verilebilir.
orgnegin windows hostlar uzerinde docker calistirilirken hyperv kullanmak daha mantiklidir.

- Docker machine bir driver eklemek icin
- `docker-machine create --driver hyperv vm`
- `eval $(docker-machine env machine-name)` yeni docker-machine active etmek icin
