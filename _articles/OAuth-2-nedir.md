---
layout: article
title: OAuth 2.0  Nedir  (RFC6749)
description: OAuth 2.0  Nedir  (RFC6749)
comments: true
sortorder: 100
---

# OAuth 2.0  Nedir  (RFC6749)
- OAuth2.0, bir yazilim, yada yazilim kutuphanesi degildir,  IETF tarafindan standartlari belirlenen bir protokoldur.
- OAuth2.0, Bir Http sevise, disardaki bir uygulamanin erisimini denetlemeyi mumkun kilar.
- OAuth2.0, Resource owner (Kaynak sahibi) adina, http servise erisimin denetlenmesi kurallarini standartlastirmistir.,
- OAuth2.0, Http servis ve  dis uygulama arasindaki yetki duzenlemesini standartlastiran bir spesifikasyondur.
- OAuth2.0, Bir onceki surumu OAuth 1.0 dir (RFC5849)

- OAuth, client ile resource owner katmanlarini birbirinden ayirir. araya bir kimlik dogrulama katmani sokar.
- Geleneksel yontemde oldugu gibi, resource owner'un saglamis oldugu kimlik bilgileri ile resource server'a erisim saglanmaz, bunun yerine Authorization server'un saglamis oldugu token ile erisim saglanir.
## OAuth 2.0 da Roller

* **Resource Owner:** Yetkilendirilen bilginin sahibidir, yetki verme islemini yapar.
* **Resource Server:** Yetkilendirilen bilgiyi sunan  
* **Client :** Yetkilendirilen bilgiye erism isteyen  
* **Authorization Server:** Yetkilendirme anahtarlarini uretir.

**Resource server** ve **Authorization server.** rolleri arasinda gecen etkilesim bu spesifikasyonun disinda kalir.  
bu etkilesim ister ayni application icinde, isterse farkli applicationlar olarak gelistirilebilir.

## Protokol Akisi
```
+--------+                               +---------------+
|        |--(A)- Authorization Request ->|   Resource    |
|        |                               |     Owner     |
|        |<-(B)-- Authorization Grant ---|               |
|        |                               +---------------+
|        |
|        |                               +---------------+
|        |--(C)-- Authorization Grant -->| Authorization |
| Client |                               |     Server    |
|        |<-(D)----- Access Token -------|               |
|        |                               +---------------+
|        |
|        |                               +---------------+
|        |--(E)----- Access Token ------>|    Resource   |
|        |                               |     Server    |
|        |<-(F)--- Protected Resource ---|               |
+--------+                               +---------------+
```

- (A) Client, Resource owner dan yetkilendirilme isteginde bulunur.
  resource owner yetkilendirme istegine yukarida oldugu gibi direk olarak cevap verebilir,
  fakat Authorization server'un araci olmasi de tercih edilebilir.

- (B) Client, yetkilendirme cevabini alir, bu cevap icinde resource owner'in izni bulunur
  bu izin, OAuth2 standartlarinda 4 farkli tip ile tanimlanabilir, bunun yaninda Authorization server
  in destekledigi ek tanimlamalar da eklenebilir.
- (C) Client, yetkilendirme iznini kullanarak, Authorization server a giris yapar (authentication), ve Authorization server dan token isteginde bulunur.
- (D) Authorization server, client i kimlik dogrulamasindan gecirir, yetkilendirme iznini dogrular ve token verir.
- (E) Client, token i kullanarak, Resource server dan yetkilendirilmis icerigi ister.
- (F) Resource server, token i dogrular ve icerigi verir.

- Authorization server in araci olarak kullanilmasi yontemdir
```
     +----------+
     | Resource |
     |   Owner  |
     |          |
     +----------+
          ^
          |
         (B)
     +----|-----+          Client Identifier      +---------------+
     |         -+----(A)-- & Redirection URI ---->|               |
     |  User-   |                                 | Authorization |
     |  Agent  -+----(B)-- User authenticates --->|     Server    |
     |          |                                 |               |
     |         -+----(C)-- Authorization Code ---<|               |
     +-|----|---+                                 +---------------+
       |    |                                         ^      v
      (A)  (C)                                        |      |
       |    |                                         |      |
       ^    v                                         |      |
     +---------+                                      |      |
     |         |>---(D)-- Authorization Code ---------'      |
     |  Client |          & Redirection URI                  |
     |         |                                             |
     |         |<---(E)----- Access Token -------------------'
     +---------+       (w/ Optional Refresh Token)
```


### Authorization grant (yetkilendirme izni)
Yetkilendirme izni icinde, resource owner in verdigi izin belirtilir. Bu izin token almak icin kullanilir.
OAuth2 4 farkli izin tipi tanimlar,
- 1- Authorization  code
- 2- Implicit
- 3- Resouce owner password credentials
- 4- Client credentials

- OAuth2,  standarlarina uygun bir web uygulamasi gelistirilir ise, OAuth2 destekleyen tum servislerle entegrasyon yapilabilir.

#### Authorization Code
Authorization'un client tarafindan direk olarak resource owner dan istenmesi yerine,
Authorization server araci olarak kullanilarak resource owner dan elde edilir.
client bu kodu Authorization server dan elde eder
