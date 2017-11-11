---
layout: article
permalink:
name:
file_type:
title: JMater notlari, kurulum ve kullanim
description: >-
  JMater notlari, kurulum ve kullanim
tags:  
category:  
sort_order: 10
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

<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [JMETER NOTLARI, KURULUM VE KULLANIM](#jmeter-notlari-kurulum-ve-kullanim)
	- [1. JMeter Nedir?](#1-jmeter-nedir)
	- [2. JMeter Kurulumu ve Ayarlar](#2-jmeter-kurulumu-ve-ayarlar)
	- [3. JMeter test dosyalarini otomatik calistirmak](#3-jmeter-test-dosyalarini-otomatik-calistirmak)
	- [4. JMeter Egitimi](#4-jmeter-egitimi)
	- [5. Bilinmesi Geken Bazi Kavramlar](#5-bilinmesi-geken-bazi-kavramlar)
	- [6. Standart bir test icin eklenmesi gereken temel elementler.](#6-standart-bir-test-icin-eklenmesi-gereken-temel-elementler)
	- [7. Test script olusturmak,](#7-test-script-olusturmak)
	- [8. Recording](#8-recording)
	- [9. Regular expression Extractor:](#9-regular-expression-extractor)
	- [10. CSV kullanmak](#10-csv-kullanmak)
	- [11. Script logic controller](#11-script-logic-controller)
	- [12. Assertions](#12-assertions)
	- [13. Functional testing and checking for errors](#13-functional-testing-and-checking-for-errors)
	- [14. Beanshell scripting](#14-beanshell-scripting)
	- [15. ThirtParty plugins](#15-thirtparty-plugins)
	- [16. Load and Throughput shaping](#16-load-and-throughput-shaping)
	- [17. Gelismis raporlama](#17-gelismis-raporlama)
	- [18. TUNING ve JMETER ile yasanan tecrubeler](#18-tuning-ve-jmeter-ile-yasanan-tecrubeler)
		- [18.1. Analize baslarken](#181-analize-baslarken)
		- [18.2. External servis baglantilari.](#182-external-servis-baglantilari)
		- [18.3. Browser Cache in calismama durumu](#183-browser-cache-in-calismama-durumu)
		- [18.4. Web sitesinde loglamanin acilmasi ve izlenmesi](#184-web-sitesinde-loglamanin-acilmasi-ve-izlenmesi)
		- [18.5. Audit Logging izlenmesi](#185-audit-logging-izlenmesi)
		- [18.6. Veritabninin izlenmesi](#186-veritabninin-izlenmesi)
		- [18.7. www.newrelic.com analizi](#187-wwwnewreliccom-analizi)
		- [18.8. Ic methodlar](#188-ic-methodlar)
		- [18.9. Tail / Wintail](#189-tail-wintail)
		- [18.10. Cache](#1810-cache)
		- [18.11. Cok sure alan 1000ms uzeri methodlar](#1811-cok-sure-alan-1000ms-uzeri-methodlar)
		- [18.12.  External Services (Dis servis)](#1812-external-services-dis-servis)

<!-- /TOC -->
# JMETER NOTLARI, KURULUM VE KULLANIM
**Basliklar**


## 1. JMeter Nedir?
* JMeter load test (yuk testi) yada stress testi yapmak icin kullanilan, Apache tarafindan gelistirilen ucretsiz bir aractir.
* JMeter kullanarak, bir web sitesi uzerinde yaptiginiz islemleri kaydederek daha sonra bu kaydi ayni anda binlerce defa calistirabilirsiniz. Bu sayede, test yapacaginiz sistem uzerinde ayni anda binlerce kullanicinin bulunma durumunu simule etmis olursunuz.

* Kaydederek daha sonra calistirdiginiz test yapisina "Test Senaryosu" yada "Test script" denir.
* Test scriptler tek kullanici icin kaydedildikten sonra, cok kullanici testleri yapabilmek icin, olusan jmeter test adimlarini amaca uygun sekilde  degistirilmesi gerekir.
* JMeter, test yapilacak sisteme gonderilecek verileri (parametre yada degisken de diyebiliriz)
farkli kaynaklardan alabilir.
  - Bir dosya icinden alabilir, genellikle bu dosya csv dosyasi olur, ornegin bir csv dosya icine bin adet kullaniciadi, parola kaydederek, jmeter ayarlarini yaptiktan sonra  login testi yapabilirsiniz.
  -  Test parametresi olarak, jmeter elemenlerinden bazi veriler alinabilir.
  -  Karsidaki sistemin, bir onceki response (cevabindan) ayiklanarak (parse, extrack) alinabilir.

## 2. JMeter Kurulumu ve Ayarlar
www.apache.org sitesinden son surumu indirilebilir.
indirdikten sonra, terminal ekranindan kurulum klasorune gidilerek

* mac osx icin
```sh
 $ sh jmeter
```

* windows icin
```bash
> jmeter.bat
```
seklinde calistirilabilir.
* Windows'ta calistirilirken **"bin"** klasoru altindaki **"jmeter.bat"** dosyasini calistirmak yeterli olacaktir,
* Uygulamanin 32bit calismamasini saglamak lazim, Jre (Java Runtime Environment) 64bit olursa daha iyi olur. bunu anlamak icin windows task manager a bakilabilir. windows 32bit calistirdiklari uygulamanin yanina (32bit) seklinde belirtiyor.
Ikici olarak 32bit uygulamalar icin maksimum bellek (RAM) 2048MB tir, daha buyuk bir XMS vererek deneme yapilabilir.
yapacaginiz testteki kullanici (thread) sayisina gore memory degerinizi belirleyebilirsiniz.

* ornegin:
```sh
JVM_ARGS="-Xms4G -Xmx6G"
echo  "JVM_ARGS: $JVM_ARGS"
```
seklinde ayar yapiliyor, echo ile console/terminal e bastirilan ayarlari kullanarak baslayacaktir.
diger yandan jmeter adinda bir script dosyasi var oradan da detayli ayarlamalar yapabilirsiniz.

## 3. JMeter test dosyalarini otomatik calistirmak
* Blazemeter adli siteye jameter scriptini (.jmx dosya) gonderdiginiz zaman, belirli bir ucret karsiliginda
istediginiz kadar client IP den test uygulayabilirsiniz.
* Blazemeter uzerinden yapilan testler sayesinde tamamen gercek ortam simule edilebilir. Request lerin hepsi farkli IP adreslerinden gelecektir.
* Calistiginiz kurum buna kaynak ayirirsa daha guzel olur.

* https://blazemeter.com/ : tesetleri otomatik calistiran cloud

##  4. JMeter Egitimi
* JMeter hakkinda detayli bilgi edinmek icin asagidaki web adresleri incelenebilir.
https://blazemeter.com/resources
http://mwebhack.blogspot.com.tr/
* Benim burada yazdigim makale ise, daha cok ogrendiklerimi unutmamak adina, kendi notlarimdan olusturdugum bir derlemedir.
* Bana gore test yapabilmek icin bilinmesi gereken minimum bilgiyi icermektedir.

## 5. Bilinmesi Geken Bazi Kavramlar

![1.png]({{site.img}}/jmeter.md.images/1.png)

* JMeter ilk acildiginda, ekranin 2 bolmeden olustugunu gorursunuz.
  * **Sol Panel:** Test planindaki tum elementleri/objelerin listesini hiyerarsik bir bicimde duzenli olarak gosterir
  * **Orta Panel:** Sol panelden secilen objelerin ayarlari orta kisimda acilir.
* Menu de *Options/Coose language (Ayarlar/ Dil secimi)* dil degistirebilirsiniz. Dil degisimi yaptiginizda, tum ekran arayuzleri sectiginiz dile uygun sekilde acilacaktir. fakat Help/Yardim kismi herzaman ingilizce acilacaktir.
* Burada ingilizce ekranlar uzerinden anlatim yapilacaktir.
* JMeter yardim ekranina menuden ulasabilirsiniz. Cok detayli ve cok guzel bir anlatimi vardir.
* Yardim icin, cok cok guzel bir ozellik ise sudur, sol paneldeki herhangi bir obje uzerinde sag tikladiktan sonra "Help" tiklandiginda, direk olarak ilgili yardim konusuna gitmektedir.
* JMeter ilk acildiginda, sol panel de iki obje yer alir. "Test Plan", "WorkBench" bu container lara asagida deginilmistir.
* JMeter da, sol paneldeki herhangi bir element uzerinde sag tiklayip "Add" kismina
	gelindiginde,

>>>>>![3.png]({{site.img}}/jmeter.md.images/3.png)

mevcut element altina eklenebilecek elementlerin listesi gelmektedir.
- **Thread:** User, her bir thread bir kullaniciyi simule eder.

-  **Test Plan:** JMeter script, yapilacak test scripti icindeki tum objeler bu container da yer alir. ana kapsayicidir. teste yonelik genel ayarlari icerir.

- **Thread Group:** User grup, Test adimlarini yerlestirdigimiz container dir, burada conainer icinde bulunan, testin kac kullanici ile yapilacagini ayarlayabiliriz.  **Play** butonuna basildiginda bu element calistirilir. ve icindeki elementler sira ila calistirilir.

-  **Samplers:**  Request yapan elementler (make a request)

- **Config Elements:** Browser, caches, cookies, headers, defaults gibi bircok ayarlarin yapilmasini saglayan elementlerdir. (some configurations, simulate like browser, caches, cookies)

- **Timer:** Add a delay, gercek ortami simule etmek icin bazi bekleme degerleri eklenebilir.

- **Listener:** Reporting, logging, and debugging, yapilan test sonuclarini dinleyip rapor olarak gosteren elemenlerin butunudur.

 - **Assertions:** Error checking, tekil request/response lardaki bazi kontroller yapmak icin kullanilabilir, ornegin response icinde bir text aratmak ve bu text gelmediginde hata firlatmak gibi.

- **Pre processor:** Modify the request, before send, Request yapmadan once bir takim parametrelerin request icine ekleyebiliriz genel olarak ``${parametere}`` seklinde kullanilir. bu parametreler bir onceki response icinden extract edilmis olabilir. veya genel parametre olabilir. Ornegin test ortamindaki tum kullanicilarin sifresi ayni yapilip, Login ekrani request ini yaparken genel parametre olarak eklenebilir. ``${password}``

- **Post processor:** Parse the response, after response received, Request sonucunda aldigimiz Response lar icinde islemler yapmak icin bu elementi kullaniriz. ornegin login requesti sonucunda bize donen response icinde, eger karsidaki sayfa form authentication yapiyorsa ve cookie kullaniyorsa, response icinden `Set-Cookie` headersini extract (cikarmak) ederek bir sonraki requestlerde kullanmak uzere bir parametreye setlenebilir.

- **Logic Controller:** Yazilimsal if, for, while gibi donguler kurulabiliryor

- **WorkBench:** Temp working space (test record etc.)

- **Ramp-up:** Kac saniyede bir belirtilen kullanici kadar thread canlandiracagini belirler
ornegin thred group: 10 olursa ramp-up:10 olursa her saniye 1 thread calistirir toplam 10 saniye
sonra tum thread lari calistirmis olur.

- Once bir "Thread Group" olusturulur daha sonra eklenecek elementler bunun altina eklenir.
- Play buttonuna tiklandiginda test plani icindeki islemler yukaridan asagiya dogru uygulanir.

## 6. Standart bir test icin eklenmesi gereken temel elementler.
* **Thread Group:** Kullanici grubu,
*  **Http Cache Manager:** Image css filan bunlari cache leme simulasyonu yapar
 ornegin ilk request te ister ondan sonra browser gibi davranarak istemez. bu elementin ayarlarinda
 clear cache each iteration secilmez ise bircok requestte http 304 gorebiliriz bu da cache in kulanildigini gosterir.
  * **User Defined Variables:** Name/value collection dir, burada degisken ve degeri girilebilir, diger elemenler icinde ise Value icinde ``${parameter}``  seklinde cagrilabilir.
	burada kullanilabilecek parametrelerden en uygunlari  host=112.123.123.233, protocol=https
v.b. daha sonra "Http Request Defaults" elementinde ``${host}`` gibi cagrilabilir.
 * **Http cookie Manager:** Browser simulasyonu yapar, authentication icin kritiktir. tipki bir browser gibi websitesinin cookie kaydetmesine izin verir.
 * **Http Request Defaults:** Tum requestler icin ortak olan parametreler burada tanimlanir
 * **Constant Time:** H[erbir request arasinda nekadar beklenilecegini simule eder,
 * **View Result Tree:** Request/Response lari gosterir. bunun gibi rapor gostermi yapan baska elementler de vardir, kendiniz ekleyerek deneme yapabilirsiniz. test senaryosunu olustururken en cok kullanilan listener viewresult tree dir.   fakat cok kullanici ile test ederken performans harcamamasi icin disable etmek daha iyi olur, cok kullanicili testlerde "Summary Report" daha uygundur.
* **Http Header Manager:** Tum requestler deki header bilgisini override eder yani ezer.
* **Web sistesinde:** documentation altindaki component reference kisminda, tum elementler hakkinda detayli anlatim mevcuttur.

## 7. Test script olusturmak,
Test scritp recording ozelligi kullanilarak otomatik olusturulabilir, fakat burada bircok gereksiz islem olabilir, bunun yerina scriptin manual olusturulmasi daha saglam bir yontemdir,
bununla beraber recoding yapilarak, recod sonucu olusan script ten faydalanmak ve mauel olusturulan ile kiyaslamak iyi bir yontemdir.

## 8. Recording

 **File/Template -> Templates :** Recording sablonu acilir. Create buttonuna tiklanir.
 **WorkBench:** Burada Test script recorder vardir. Bu bir proxy olarak davaranir
 burdaki 8888 portuna herhangi bir browser proxy tanimlamasi yapar ise, tum requestler jmeter tarafindan kaydedilr.

* Test script recorder icinde "url pattern to exclude" ayari vardir burdan bazi dosya uzantilari exclude edilebilir.
![4.png]({{site.img}}/jmeter.md.images/4.png)

* Record yaptiktan sonra Thread Group altindaki, Recording Controller altina
her bir sayfa requesti icin bir group olusturur, yani ayni sayfadaki tum requestleri group yapar.
* JMeter sayfa bazinda yaptigi gruplamalari isimlendirirken numara verir. daha sonra bu isimleri degistirebilirsiniz. Ornek ekran goruntusundeki 362 ile baslayan grup, jmeter tarafindan isimlendirilmistir ve ismi degistirilmemistir. digerleri ise degistirilmistir.
![2.png]({{site.img}}/jmeter.md.images/2.png)
## 9. Regular expression Extractor:
Response icinden bir datayi extract eder ve bir degiskene atar, bu
degisken bir sonraki request te parametre olarak kullanilabilir.
Bu yontem bircok jmeter tesinde kullanilan bir yontemdir. Bircok jmeter testinde, bir onceki response ta gonderilen veri ile bir sonraki request olusturulur. Ornegin kullanici adi sifre ile girilen bir web uygulamasi icin test yapacaksaniz, oncelikle login olmaniz gerekir, login olabilmeniz icin ise web uygulamasi tarafindan size gonderilen cookie deki sessionid yi kullanmaniz gerekir, cunku web uygulamasi
icin sessionid tekil bir kullanicidir. requestlerde bu veriyi de gondermeniz durumunda siz bir tekil kullanici olmus olursunuz. gondermez iseniz, her requestiniz yeni bir session (oturum) olarak degerlendirilir.
* Test yaparken, login ekraniniza ilk girisinizde web uygulamasinin response unda size "Set-Cookie" seklinde bir http-header gonderdigini gorebilirsiniz, test esnasinda request-response lari izlamak icin *view results tree* kullanabilirsiniz.
ornek:
**Reference name=** sessinid,
**regular expression=** `Set-Cookie: ASP\.NET_SessionId=(.\*); path,`
**template=** \$1\$

baska bir regex ornegi:
` fc-yellow[^.]*? data-courseno=\\"(.*?)\\"`
fc-yellow ile baslayan ve aradaki karakterleri onemsemeden data-courseno= ile devam eden ifadeleri yakaliyor.
regex icin kullanabileceginiz site www.regex101.com
**template:** string olusturmak icin kullanilir. verilen numara ise regex teki match sirasini gostrerir ornegin soyad yakalayan bir regex yazilmis ise su sekilde bir string olusturulabilir. "Ad \$1\$" : Ad Soyad seklinde string olusturulmus olur ve bu bir degiskene setlenir. Degisken tum scope icin gecerli olacakdir. sonraki requestlerin hepsinde gecerli olacaktir.
* Burda  css/jquery selector gibi kullanim daha kolay olabiliyor:
```
degisken1[^.]*?degisken2[^.]*?arananifade(secilenifade)
```

* Authentication: web siteleri genelde ilk requestte browser'a bir key verir bunu cookie veya header ile verir, daha sonra  yapilan tum isteklerde, bu key ile request yapilir.  login olundugunda bu key kullanilarak token uretimi saglanir. Bu durumda eger cookie kullanilmiyor ise, jmeter da regular expression extractor ile pre processors'te key alinir, daha sonra login istegi yapilan  yerde bu key kullanilir, gelen token yine response icinden parse edilerek alinabilir.

* jmeter daki "http request" objesinin bir ozelligi olan ve tik atilabilen, "follow redirects"  sunucu tarafinda yapilan yonlendirmeleri takip etmesini ayarlar.  Eger "View resutl tree" de  bir requestin altin 2 tane daha child request goruluyor ise bunlardan ilki redirect oldugu icindir, responsunda su yazar
  "Response code: 302" Moven temporarily seklindedir. response header daki Location: /account/login?returnurl=/ kismi sayfanin redirect edildigi adrestir.

* Http Request objesinin parameterelerinde altta bulunan "Retrieve all embeded resources" seklinde bir tik var bu isaretlenirse, flash videolari filan da
  get yapilir, burada "URL must match" kismina regex girilecek mesela `http://82.251.41.xxx/.*`

* `__randomString(10,abcxyz,)` : jmeter fonksiyonudur ve requestlerde kullanilabilir. bunun gibi bircok fonksiyon vardir
  options menusunda "function helper dialog" vardir buradan fonksiyonun parametreleri hakkinda bilgi bulunur, ayrica help buttonuna tiklanirsa
  help altindan ilgili fonksiyonun tum detaylarina erisilebilir. veya web sitesinden tum detaylar ogrenilebilir.

## 10. CSV kullanmak
 * Config element altinda "CSV data set config" olarak eklenir.
   jmx file ile ayni konuma konuldugunda, dosyanin ismini vermek yeterli. dosyadaki kolonlari `${columnname}` seklinde herhangi bir post icinde veye get icinde kullanabiliriz.

* **Listeners:** Genellikle en cok kullanilan listener "View result tree" fakat bunun disinda daha detayli bilgiler sunan listener lar olmasina ragmen  listener lar makina kaynaklarini asiri tuketir, eger cok sayida kullanici ile test etmek istiyorsak listener sayisini dusurmemiz gerekmektedir.  Az sayida kullanici ile debug yaparken yaygin olarak kullanilan listnerlar sunlardir
  - View results in table
  - Summary report
  - Graph results

  **Not:** Burada onemli olan bir web sitesinin limitlerini olcmektir, buna bagli olarak, senaryodaki kullanici sayisini lineer olarak artirmak
  ve yatay eksende artan kullanici sayisina gore response time daki farklilik raporu cok guzel fikir verecektir.

  **Not:** Graph result ta dikey eksen response time i gostermektedir.


## 11. Script logic controller
  ForEach Contoller
  ifController: eger login olursa bunu yapsin, gibi bir kontrol olabilir.
  ifcontroller altina yeni elementler eklenerek yapiliyor, ifcontroller icindeki condition true donerse, controller altindaki islem yapilir.
  bu if in else i yok sadece condition true ise icine giriyor okadar
  WhileController

  * "Advanced web test plan" adinda bir template var onu kullanmakta fayda var

## 12. Assertions
 Burada condition gerceklesmedigi zaman hata firalatir.
 **Duration assertions:** sayfadan belli bir sure cevap gelmediginde firlatir
 **Response assestions:** response icinde specifig bir text arar bulursa true doner

## 13. Functional testing and checking for errors

## 14. Beanshell scripting
[Detayli bilgi](https://blazemeter.com/blog/queen-jmeters-built-componentshow-use-beanshell)
not: options menusunden log viewer acilabilir

**Ornek Script:**
```java
import org.apache.jmeter.protocol.http.sampler.HTTPSamplerProxy;
import org.apache.jmeter.protocol.http.control.CookieManager;
import org.apache.jmeter.protocol.http.control.CacheManager;
import java.util.Date;
import java.text.SimpleDateFormat;

String response=new String(data);
log.info(response);
```

## 15. ThirtParty plugins
[Detayli bilgi](http://www.jmeter-plugins.org)

## 16. Load and Throughput shaping

## 17. Gelismis raporlama

**Not:** Summary report kismi cok onemli, burada Max yazan kisim milisaniyeyi gosteriyor, Aferage ise oratalama response time ini gosteriyor.
jmeterda response time lar cok uzar ise testlerin fail olmamasi icin asagidaki configurasyon yapilir.

```sh
user.properties dosyasyinda
httpclient4.retrycount=1
httpclient3.retrycount=1
hc.parameters.file=hc.parameters
httpclient.parameters.file=httpclient.parameters

hc.propertites dosyasyinda
http.socket.timeout$Integer=300000
http.connection.stalecheck$Boolean=false

httpclient.parameters dosyasinda
http.socket.timeout$Integer=300000
http.connection.stalecheck$Boolean=true
```


## 18. TUNING ve JMETER ile yasanan tecrubeler

yapilan yuk (stress) testlerinde yasanan ve duzeltme uygulanan bazi ornekler

### 18.1. Analize baslarken
Cogu sistemde kullanicilar belirli bir gun veya belirli bir saat araliginda sisteme yogun bir sekilde baglanirlar.
Yuk testi hazirlanirken, bu yogun donemde kullanicilarin yapiti islemler dikkata alinarak yapilabilir.
ornegin, yillik faaliyet beyannamesi   abc tarihinde bitiyor ise, faaliyet beyanname verilmesi de birkac web formundan belki birkac rapor dan olusuyor olabilir.
Yuk testinde, bu yogun donemde kullanicinin yaptigi tum islemler eklenmelidir.
Test senaryosunu mumkun oldugu kadar gercekci hazirlamak gerekir.
senaryo hazirlandiktan sonra, her bir test adimi ayrintili sekilde analiz edilmelidir. methodlarin yada requeslerin
sureleri incelenmelidir. veritabani incelenmelidir.

jmeter ile kullanicilari ayni anda sisteme sokup kullanicilarin ayni anda ayni islemleri yapmasi saglanabilir.
bu durumda test adimlarinin hangilerinin yogun yuk altinda sikistigini gozleyebilirsiniz.

fakat gercekci bir test yapilmasi daha da onemlidir. yani kullanicilarin bir kismi testin ilk adiminda iken bir kismi son adiminda olabilir. kullanicilar herzaman ayni anda ayni islemleri yapmazlar,
bu sekilde test yapildiginda test adimlarinin birbirlerine etkisi de gozlenmis olur,
ornegin son adimda "onayla" islemi bulunsun, 3. adimda da kaydet islemi bulunsun bu iki islemin ayni anda
yuk altinda bulunmasi veritabaninda deadlock olusturabilir.

### 18.2. External servis baglantilari.
sistem islemler sirasinda dis bir sisteme baglaniyor ise, tehlikeli bir durumdur, kullanici yogun zamanlarda dis sistemin durmasi, mevcut sisteminde durmasina sebep olacagindan,
dis sistemin durmasi durumu icin bir B plani hazirlamak, iyi bir cozum olabilir.
yuk testlerini yaparken, dis sisteme yapilan Request/Response sureleri mutlaka izlenmeli,
kullanicinin yogun oldugu zamanlarda dis sistemin tavri da izlenmelidir.
yapilabiliryor ise, dis sistemi devre disi birakarak test yapilmasi ve dis sistem devrede oldugu durumla karsilastirilmasi cok faydali olacaktir, kumulatif olarak kullanilarin islem suresini cok uzatabilir.

### 18.3. Browser Cache in calismama durumu
Tum sayfalarda kullanilan html header i icinde yer alan bazi css veya scriplerin boyutlari
cok fazla olabilr, bu durumlarda browser cache ozelliginin calisir durumda olmasi cok onemlidir.
ciddi manada network I/O sorunu olusturabilir.

### 18.4. Web sitesinde loglamanin acilmasi ve izlenmesi
stres testinin uygulandigi sistemdeki loglarin acilmasi ve izlenmesi cok onemlidir.
websitesinde icerik logunun izlenmesi lazim, eger bir web-api yada WCF servisi var ise method surelerinin izlenmesi gerekir.

### 18.5. Audit Logging izlenmesi
eger sistemde bir AuditLog yapisi var ise buradan cok faydalanilir.
en cok cagrilan method, yada iclerik yada
en uzun suren method, yada request uzerine yougunlasilarak tuning yapilabilir.

### 18.6. Veritabninin izlenmesi
Veribanini izlerken, cok kaynak tuketen queryler de duzenleme yapilabilir.
burada cok fazla select atilan tablolar uzerinde indexleme yapilabilir, fakat
index atilmasi herzaman iyi bir cozum olmayabilir.
ayni tabloya cok fazla insert/delete olasi durumunda index sistemi asiri yavaslatacaktir.
yasanilan iki tecrube su sekildedir.
- index yanlis olusturuldugunda, insert/delete islemlerinde tablo lock olmasin seklinde ise
bu durum asiri deadlock a sebebiyet vermektedir.
- index yapilan tabloya cok fazla insert oluyor ayni zamanda delete yapiliyor ise.
index in rebuild yapilmasindan dolayi, delete islemleri timeout olacaktir.
- yogun cagrilan methodlarda, sql ler cok iyi analiz edilmeli, sql icinde birkac tabloda islem yapiliyor
ise ve insert/update/delete ler var ise, bu durumda deadlock olusma olasili cok fazladir.

### 18.7. www.newrelic.com analizi
[www.newrelic.com](http://www.newrelic.com) adresindeki sirket, sunucu performans analizi hizmeti vermektedir.
burdan bir hesap acip, sunucular uzerine sireketin ajan(agent) yazilimlari kuruldugunda, agent yazilimlar sunucu daki web uygulamsinin database in ve IIS in tum performans counter larini topluyor.
daha sonra www.newrelic.com adresinden detayli raporlar sunuyor.
yuk testleri sirasinda cok faydali olacaktir.

### 18.8. Ic methodlar
loglara dusmeyen ic methodlarda
```csharp
Stopwatch sw=new Stopwatch();
sw.Start();
//method.....
sw.Stop();
Console.Debug.WriteLine("Elapsed time:"+sw.ElapsedMilisecond);
```

### 18.9. Tail / Wintail
gibi programlar ile loglarda filtreleme yaparak, specific bir methoda odaklanmak mumkun

### 18.10. Cache
 - ####  In Memory Caching (Uygulama capinda on bellek)
* Yazilim icindeki sabit verilerin her saferinde veritabanindan cekilmesi performansi dusurebilir.
yazilim icinde tuning  yapilacaksa, Cache leme yontemi cok faydasini gorebilirsiniz.
Cacleme yaparken, uygulama capinda cok sik degismeyen ve cok fazla cagrilan veriler cache lene bilir.
genellikle sabit liste verileri (Combobox, Listbox) gibi verilerin cache lenmesi, guvenlik kontrolu yapilan collection un cache lenmesi,
roller yetkiler. v.b bunlar cok ise yarayacaktir.
* internal memory cache lerin sorgu performansi takip edilmeli,
uygulamada Thread Lock durumlari olabilir,  ozellikle custom cache implementasyonlarinda bu duruma cok
raslanir, yazilimci cac icine liste atar, methodlar synronized tir ve methodlarin siraya girdigini dusunur
fakat cache icine liste atildiginda listedeki birkac thered tarafindan alindiginda, referanslari ayni olacaktir,
yani cache ten alinan objeler clone lanmayacaktir. buru durumda ayni referansli objelere birkac thread degisiklik yapmak isterse lock olusabilir.

- #### Distributed Caching (Dagitik Bellek)
Cache hizmeti veren bir ek yazilimdir, dis sistemlerden kullanilabilir.
Kisacasi birden cok sunucudan yada uygulamadan kullanilabilien, networke servis veren merkezi bir cache sistmeidir.
gunumuzde en cok ragbet goren cache servisi Redis tir.


 - #### Browser Caching (Tarayici Bellegi)
 Bazen kurumsal uygulamalarda, bazi script dosyalari, image lar v.b,  MB seviyesinde olabiliyor, browser in her severing bu dosyalari cekmesi
 ciddi bir network I/O  problemi olusturabilir. bu yuzden yazilim icinde tarayiciya hangi elementi nekadar belleginde tutacaginin talimati verilmelidir.

- fakli platformlar icin cache kontolu

PHP:
```php
header("Cache-Control: no-cache, no-store, must-revalidate"); // HTTP 1.1.
header("Pragma: no-cache"); // HTTP 1.0.
header("Expires: 0"); // Proxies.
```
Java Servlet, or Node.js:
```java
response.setHeader("Cache-Control", "no-cache, no-store, must-revalidate"); // HTTP 1.1.
response.setHeader("Pragma", "no-cache"); // HTTP 1.0.
response.setHeader("Expires", "0"); // Proxies.
```
ASP.NET-MVC
```asp.net
Response.Cache.SetCacheability(HttpCacheability.NoCache);  // HTTP 1.1.
Response.Cache.AppendCacheExtension("no-store, must-revalidate");
Response.AppendHeader("Pragma", "no-cache"); // HTTP 1.0.
Response.AppendHeader("Expires", "0"); // Proxies.
```
ASP.NET:
```asp
Response.AppendHeader("Cache-Control", "no-cache, no-store, must-revalidate"); // HTTP 1.1.
Response.AppendHeader("Pragma", "no-cache"); // HTTP 1.0.
Response.AppendHeader("Expires", "0"); // Proxies.
```
ASP:
```asp
Response.addHeader "Cache-Control", "no-cache, no-store, must-revalidate" ' HTTP 1.1.
Response.addHeader "Pragma", "no-cache" ' HTTP 1.0.
Response.addHeader "Expires", "0" ' Proxies.
```
Ruby on Rails, or Python on Flask:
```ruby
response.headers["Cache-Control"] = "no-cache, no-store, must-revalidate" # HTTP 1.1.
response.headers["Pragma"] = "no-cache" # HTTP 1.0.
response.headers["Expires"] = "0" # Proxies.
```
Google Go:
```go
responseWriter.Header().Set("Cache-Control", "no-cache, no-store, must-revalidate") // HTTP 1.1.
responseWriter.Header().Set("Pragma", "no-cache") // HTTP 1.0.
responseWriter.Header().Set("Expires", "0") // Proxies.
```
Apache .htaccess file:
```html
<IfModule mod_headers.c>
    Header set Cache-Control "no-cache, no-store, must-revalidate"
    Header set Pragma "no-cache"
    Header set Expires 0
</IfModule>
```
HTML4:
```html
<meta http-equiv="Cache-Control" content="no-cache, no-store, must-revalidate" />
<meta http-equiv="Pragma" content="no-cache" />
<meta http-equiv="Expires" content="0" />
```
Python/Pyramid:
```python
def my_api_call(context, request):

    # disable caching
    request.response.headerlist.extend(
        (
            ('Cache-Control', 'no-cache, no-store, must-revalidate'),
            ('Pragma', 'no-cache'),
            ('Expires', '0')
        )
    )
```

```html
<meta http-equiv="cache-control" content="max-age=0" />
<meta http-equiv="cache-control" content="no-cache" />
<meta http-equiv="cache-control" content="no-store" />
<meta http-equiv="cache-control" content="must-revalidate" />
<meta http-equiv="expires" content="0" />
<meta http-equiv="expires" content="Tue, 01 Jan 2016 1:00:00 GMT" />
<meta http-equiv="pragma" content="no-cache" />
```

### 18.11. Cok sure alan 1000ms uzeri methodlar
bu method lar icinde zaman aldigi tahmin edilen kisimlarda sure hesabi yapilarak,
methodu uzatan kisim tespit edilmeye calisilmalidir.

### 18.12.  External Services (Dis servis)
dis serviste kullanilan data toplu cekilerek offline moda alindi
online mod sure: 30
web servis offline  500 kullanici,
