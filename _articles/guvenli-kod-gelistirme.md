---
layout: article
permalink:
name:
file_type:
title: Guvenli Kod Gelistirme
description: >-
  Guvenli Kod Gelistirme
tags:  
category:  
sort_order: 20
rating: 100
changefreq: monthly
priority: 0.5
published: true
create_date: 2017-10-23T10:20:00Z
modified_date: 2017-10-23
created_by: atilla
modified_by: atilla
comments: true
redirect_url:
toc: false
---

# Guvenli Kod Gelistirme

## Temel Kavramlar

- OpenSSL deki zafiyet

`heartbeat` zafiyetine `heardbleed` demisler, burada `hearthbeat(string char[], int length)` gibi bir methodun icinde memoryden alacagi rasgele string degeri verilmis bundan faydalanan hacker lar, memoryi ele gecirebilmisler.

- CVSS (Common Vulnerability Scoring System) score zafiyet(savunmasizlik) puanlamasidir hearthbleed zaafiyeti 11 degerinde bir zaafiyet almis, cok yuksek

- Guvenlik zaafiyerlerinin bir cogu string concatanation ile olusur.

- Guvenlik zaafiyetlerinin bir cogu kullanicilardan aldigimiz vei ile kodu karistirmamizdan kaynaklanir.

**Guvenli yazilim:** normal sartlar altinda dogru calisiyor ise, saldiri altinda da dogru calismasi demektir.

**Hatalarin kullaniciya verilmesi:** Hatalar da son kullaniciya full stacktrace verilmemelidir, guvenlik acigidir.

- Kullanicilardan aldigimiz girdileri azaltmak basitlestirme bazinda iyi bir yontemdir.
- Kullanicilardan aldiklarimi bilgilieri direk olarak kod ile birlesirmek yanlis bir yontemdir,
- Her bir girdinin kontrol edilmesi gerekmektedir.

**Guvenli kod gelistirme ilkeleri**

- Kullanicilardan alinan girdi minimumda tutulmali.
- Kullanicilardan alinan girdilerin kontrolsuz string birlestirme isleminde kullanilmamasi
- Her katmanda yetkilendirme yapilmasi

### SOP - Same Origin Policy

Ayni kaynak politikasi Browserlar, scriptler icin bu kurali kullanir, bir script sadece kendi kaynagina ait isteklerde bulunabilir.

- **XMLHttpRequest (AJAX) icin SOP** www.abc.com daki bir script kendi kaynagindaki (www.abc.com) daki herhangi bir adrese request gonderebilir ve cevabini alir. Fakat www.abc.com adresindeki bir script www.xyz.com adresine bir request gonderdiginde cevabini alamaz.

- **Browser Cookie yonetimi** Browser daha once ayni domain den aldigi bir cookie yi ayni domain e giderken isteklere otomatik ekler.

  - domain adi farkli olursa cookiler gondedilmez
  - http den https e yada https ten http ye giderken de SOP engelleme yapar.
  - port farkli olursa SOP engeller,
  - domain adi tam uyusmalidir, subdomain ler arasi da SOP engelleme yapar.

session hijacking : javascript ile cookie caliniyor, sayfamiza bir script gomer ise.

## TEDBIR ALMA YONTEMLERI

**Not: saldirilarda encoding tedbir almanin birinci kurali** tum encodingler yerinde kullanilmalidir.

- Html encoding
- Attribute Encoding
- URL encoding
- Javascript Encoding

```
"   --> \x22
>  -->  \x3c
```

**AntiXSS** : microsoftun bir kutuphanesidir, yazilimda kullanilabilir encoding ve decoding yaparken bu library kullanmak faydali olabilir.

- Burp adindaki tool kullanilarak Httmp Request ve Response lar izlenebilir, http proxy olarak calisiyor., girilenleri gosteriyor ve mudehale etme imkani veriryor.

### 1- Blacklisting

Bilinen kotu karakter veya karakter kumelerinin reddedilmesidir. Cok kullanilan ama guvensiz bir girdi denetimidir. ornegin `<script>` gecen girdilerin reddedilmesi. `or 1=1` gecen girdilerin reddedilmesi.

blacklisting kotudur, bir onlem degildir.

### 2- Whitelisting

Sadece iyi karakter veya karakter kumelerinin kabul edilmesidir. Guvenli bir girdi denetimidir.

### 3- Normalizasyon

Bir dizginin en basit, en temel haline cevrilmesidir.

### 4- Sanitize - Temizleme islemi

Girdinin kabul edilebilir bir formata donusturulmesidir. ornegin girdi icindeki tek tirnak karakterlerinin temizlenmesi `<script>` ifadelerinin temizlenmesi.

### 5- Encoding

Girdi icindeki ozel karakterlerin baska bir formata donusturulmesidir.

## ZAAFIYET CESITLERI

### 1\. XXE - Xml External Entity

**Tanim**: XML dokumanlarinin DTD kismina, zararli kod eklenebilmektedir. XML parser kutuphaneleri DTD kismini okuyup calistirmaktadir.

**Onlem**: Kullanicidan aldigimiz XML lerin DTD kisminin calistirilmasini engellemeliyiz. asagida .net icinde kullanilan bir ornek vardir.

XML dokumanlari okur iken DTD bilgisinin okunmasina izin verir isek buradan host dosyasi bile okunabilmektedir.

```csharp
 static void Main(string[] args)
        {

            //guvensiz: XmlReaderSettings setting=new XmlRaderSettings(){DtdProcessing=parse}
            //parse yetkisi verilir ise guvenlik acigi oluyor.
            //guvenli: XmlReaderSettings setting=new XmlRaderSettings(){DtdProcessing=Ignore}

            XmlReader xmlReader = XmlReader.Create(args[0], settings);

            var root = XDocument.Load(xmlReader, LoadOptions.PreserveWhitespace);

            foreach (var reportItemElement in root.Root.Elements("issue"))
            {
                string vuln = (string)reportItemElement.Element("name");
                string host = (string)reportItemElement.Element("host");
                string severity = (string)reportItemElement.Element("severity");

                Console.WriteLine("Host: " + host);
                Console.WriteLine("Vulnerability: " + vuln);
                Console.WriteLine("Severity: " + severity);
            }
        }
```

Host dosyasini okkuyabilen bir XML ornegi

```xml
<?xml version="1.0"?>
<!DOCTYPE issues [
  <!ENTITY % a "<!ENTITY foo SYSTEM 'file:///C:/Windows/System32/drivers/etc/hosts'>">  %a;
]>
<issues burpVersion="1.6.01" exportTime="Thu Aug 14 03:38:12 VET 2014">
  <issue>
    <serialNumber>5626899943859184640</serialNumber>
    <type>1049088</type>
    <name>Fake Vulnerability</name>
    <host ip="176.28.50.165">http://testphp.vulnweb.com</host>
    <path><![CDATA[/search.php]]></path>
    <location><![CDATA[/search.php [manual insertion point 1]]]></location>
    <severity>&foo;</severity>
    <confidence>Tentative</confidence>
    <issueBackground><![CDATA[SQL injection vulnerabilities arise ]]></issueBackground>
    <remediationBackground><![CDATA[The most effective way to prevent SQL injection .</li></ul>]]></remediationBackground>
    <issueDetail><![CDATA[The manual insertion point 1 appears to be vulnerable to SQL injection attacks. The payload <b>' and benchmark(20000000,sha1(1))-- </b> was submitted in the manual insertion point 1\. The application took <b>8591</b> milliseconds to respond to the request, compared with <b>50</b> milliseconds for the original request, indicating that the injected SQL command caused a time delay.<br><br>The database appears to be MySQL.]]></issueDetail>
    <requestresponse>
      <request method="POST" base64="true"><![CDATA[UE9TVCAvc2VhcmNo]]></request>
      <response base64="true"><![CDATA[SFRUUC8xLjEgMjAwIE9LDQpTZXJ2ZXI6IG5naW54L]]></response>
      <responseRedirected>false</responseRedirected>
    </requestresponse>
  </issue>
</issues>
```

- Diger XXE saldirma cesidi ise, sunucuya upload edilen xml icine loop koyarak sunucunun cpu gucunu %100 yaparak sunucuyu devre disi birakmakdir.

- Diger bir XXE saldirisi DOCTYPE kismindan alinan parametrenin direk olarak xml icinde kullanilmasi ve calistirilmasidir.

### 2\. SLOWLORIS saldirisi

- Content-Length": headerinda kullanmamak lazim, Keep-Alive: contentin gelmesinde gecen suredir, bitince timeout ulur. IIS te Keep-Alive defaultu 5 saniyedir. Apache de 15 sn filandir. kucuk tutulmasi tavsiye edilir. saldiri, herbir veri gondermede tek karakter gondererek, keep-alive suresi kadar bekleyip bekleyip bir sonraki karakteri gonderir boylece length*keep-alive suresi kadar sunucu portunu acik tutarak sunucuyu tikar.

ayni sekilde zabbix gibi tool lardan gelen hearth bitlerin portu acik tumasini engellemek icin, isletim sistmeindeki keep-alive zamanini kisaltmakta yapilabilri.

saldiri: ayni domainde calisan kullanicilara, mail at domaini kullanarak siteye script enjekte et, daha sonra kullanici tiklayinca cookie ler calinir. veya bir web sitesi yapilir ve kisinin oraya girmsi saglanir, kullanicninin tikladigi url e script gomebilir.

-- normalizer kullanmak XSS sorununu cozer

```csharp
[nomalizer kodu]
public class Normalizer
    {
        public static string URL(string input)
        {
            bool stillEncoded = true;

            while (stillEncoded)
            {
                String decodedInput = HttpUtility.UrlDecode(input);
                if (decodedInput == input)
                {
                    stillEncoded = false;
                }
                input = decodedInput;
            }

            return input;
        }

        public static string HTMLV1(string input)
        {
            bool stillEncoded = true;

            while (stillEncoded)
            {
                String decodedInput = HttpUtility.HtmlDecode(input);
                if (decodedInput == input)
                {
                    stillEncoded = false;
                }
                input = decodedInput;
            }

            return input;
        }

        public static string HTML(string input)
        {
            bool stillEncoded = true;
            int i = 0;
            while (stillEncoded)
            {
                String decodedInput = HttpUtility.HtmlDecode(input);
                if (decodedInput == input)
                {
                    stillEncoded = false;
                }
                input = decodedInput;
                i++;
            }

            if (i>0)
            {
                // kotu niyet yakalandi.
            }

            return input;
        }
    }
```

[egitim]

- normalizer de while loop yerine tek bir decode den gecir ve uyari bilgisini gonderdikten sonra IPban listesine ekle

- normalizer de request icindeki loop ta count siniri da olmali while loop cok fazla olursa sunucu performansini dusurmek te bir aciktir.

bu tip kotu niyetlerin hepsini 10 dakika boyunca sisteme sokmamak lazim bir onlem olarak, yada requesti direk olarak

IPbanlist yapilacak

- username minimum=5 maximum 15 olmali karakterler arasinda _ olmali rakam olmali buyuk kucuk harf olmali

- inputlari beyaz listeden gecirebiliriz.

controller daki actionlarin hepsinin tepesine [ ] validation kontrolu eklenecek hangi karakterlerden olusacak, max min length ne olarak

kod ile veri birbirine karistirildiginda injection zaatlari oluyor. kod ile veriyi karistirmamak lazim.

repository de veri encode edildikten sonra sql ile concat edilecek.

- request validation a guven olmaz, herzaman hacklendi. (blacklisting ten bisey olmaz)

## yazilimi guvenli yapmak icin uygulama sirasi

1- Normalizasyon ve kara liste 2- Beyaz Liste yukardaki uygulamanin girisinde yapili kodun cikisinda da encoding yapalim 3- Encode / Escape

kullanicidan aldigimiz bilgiyi baska bir yerde diger kullanicilara sunuyor isek burada XSS vardir.

bankalarda cookie icin IP kontrolude yapiliyor.

AntiXss librarysini nuget ten alip koyalim

## XSS onleme kurallari

```csharp
<svg onload="alert(1)">  esittir <script>alert(1)</script>
```

## 1\. Kullanicidan alinan veriyi HtmlEncode ederek sayfaya basmak

System.Web.Security.AntiXss.AntiXssEncder, sistem icinekonulan antixss bunun haricinde bir de nuget tan indirmek daha iyi.

```csharp
<%=Microsoft.Security.Application.Encoder.HtmlEncode("")>
```

## 2.

angular kullanirken razor render kullanmayacagiz render edilen seyi $scope.key=<%=rendersomething% > seklinde kullanmaliyiz.

encoding aldigimiz yerde degil, ciktigimiz yerlerde kullanmaliyiz.

attribute icinde encode kullanditimiz da tirnak kullanmak sart, fakat bu da yeterli degil encodingi bulundugumuz yere gore yapmamiz lazim, HtmlEncode, AttributeEncode, JavaScriptEncode , UrlEncode girilen karakterler encode edilmemis seklinde gonderilirse normalizasyondan geciyor bu yuzden en kesin cozum, output un encode edilmesidir.

## RichText nasil alinir

HtmlSanitizer nuget ten indirilebilir. Whitelist usulu calismaktadir.

angular sanitizer bypass edilebiliyor. angular sanbox bypass seklinde aratilabilir.

zengin icerik alacaksak minimum zengin icerik etiketi kabul etmeliyiz. whitelist olusturmaliyiz.

# SQL injection

- storedprocedure kullanmak sql injectionu engellemez

  ' or 1=1) -- seklinde incejtion yapildi

  sql injectionun onlemi prepared statement kullanilmali sqlParameter .... eger sql keyword larinda kullanacaksak ta white list kullanacagiz.

# Guvenli Upload

1. Dosya uzanti kontrolu yapilmali.
2. Upload edilen dosya streem olarak bir Image objesine konur ve png olarak kaydedilir, bu durumda dosya icinde resim olmayan kisimlar temizlenerek kaydediliyor.
3. Dosyalar wwwroot altina upload edilmemeli, web klasoru disinda bir yere upload edilmeli, doslayari indirmek isteyenler icin ise handler yazilmasi gerekmektedir.

# OS Commanding

web uuygulamsi icinden shell kullanilir ise kullanicidan parametre alinmamali alinirsade encode edilmeli.

# CR/LF

kullanicinin log dosyasina sahte kayit atmasidir.

# ldap filer encoding

ldap ile calistigimizda mutlaka ldap encoding kullanmaliyiz.

# XPath injection

xml icindeki node lara ulasirken string concat kullanmamak kazim, her karakterini htmlEncode dan gecirmemiz lazim.

## Encryption

base64 de encode edilen herseyin sonunda bir esittir = konulur.

Encrypting ile encoding karistirilmamali.

### Simetrik sifreleme

1. anahtari olan bir sifreleme methodudur. gunumuzdeki en guvenli simetrik sifreleme algoritmasi AES

2. AES icin ecb modunun kullanmasi guvensizdir. CBC kullanilmasi gerekiyor. cok bilindik bir algoritmada bile nasil kullanildigini bilmeden kullanmamak lazim. CBC de her dosya sifrelerken farkli IV kullanilmali.

3. DES guvensiz bir algoritmadir.

4. Hash cok hizli bir tekniktir. sadece formul calistiriyor.

5. Hash yapildiktan sonra salting yapilmailidir.

6. saldirganin hash hesaplama islemini yavaslatmak gerekli.

7. Her sifrenin salt i farkli olmasi gerekiyor.

## Guvenli kimlik dogrulama

Basic authenticationda gider parola networkten acik gider, araya herkes girebilir. uygulamalar arasi kimlik dogrulama,

1. ip adresi kontrol edilebilir.
2. ortada load balancer varsa header a ip x-forwarder-for ile eklenir. forward eden tum proxyler virgul kullanilarak uc uca eklenir.

### CAPCHA replay zaafi

1. seri deneme yapilmasi engellenmelidir. IP banlama ve bekletme islimi yapilmali.

capcha seri saldirilari engellemek icin kullaniriz. capcha imagini ureten kisim farkli ise ve kullanicinin capcha degeri sessiondan okundugunda sessiondaki silmek gerekir. capcha her kullanildiginda silinmelidir.

kimlik dogrulamada basarili basarisiz degerleri mutlaka loglamak gerekiyor. GuvenliParola uretimi icin Membership.GeneratePassword(8,2) kullanmak daha iyi olabilir.

### Oturum Yonetimi

Browserlar tum requestlere site ile ilgili tum cookie ler eklenir.

#### CSRF Cross Site Request Forgery

mesajlasan 2 kullanicidan birinin script icerikli bir mesaj atar ise, saldirgan, kurbana her istedigini yaptirabilir.

onlem: saldirganin hazirladigi sahte fromu anlamak icin, formun icine Html.AntiForgerToken() action methodunun attribute una da [ValidateAntiForgeryToken]

once ugulamada XSS onelmi alinmali sonra forgerytoken kullanmaliyiz

logout ta bile post kullanilmali. mumkun olan her yerde post kullanilmali

SSL olan bir sitede SSL olmayan bir kisim olmamali asp.net in forms authentication kullanilmasi gerekir.

### File Download

file download larda kullanicidan gelen dosya isimlerinin normalize edilmesi ve whitelist kullanilabilir.

onlem `charp string gelenFileName=".../.../"; File f=new File(gelenFileName); if(f.Name!= gelenFileName){ //yakalandi }`

# Mass Assigment

burada kullanicilara mutlarak veritabanindaki modelin aynisi gonderilmemeli, mutlaka viewmodel gonderilmeli.

MD5 basit bir algoritma guvenilmezdir.

wifi hackleme yontemi= ARP poissing

browser icinde JSON.Parse demek gerekiyor.

16 farkli saldiri cesidi ogrenildi hepsnin tane tane yazilmasi lazim.

- sayfanin iframe ye mesaj gondermesi mumkun postMessage ile mesaji alan iframe penceresindeki uygulama encode yapmasi gerekiyor.

- uygulamamnin iframede calismasi engellencek

- Frame Busting Code sayesinde sayfanin iframe de acilmasi gengellenebilir.

```javascript
if(windows.top!=docuemnt.location){
  //icerdeki sayfa disariyi eziyor ve tum sayfayi kendisi degistiriyor.
  window.location="http://www.abc.com"
}
```

- localStorage["key"]=value persistent bir storage

- sessionStorage["key"]= value bu browser acik kaldigi surece tutuluyor

- Jquery nin html encode yontemi var. JQEncder kullanmak gerekir

  ​
