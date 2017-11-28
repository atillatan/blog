---
layout: article
permalink:
name:
file_type:
title: IdentityServer Nedir
description: >-
  IdentityServer Nedir
tags:  
category:  
sort_order: 22
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
toc: true
---

# IdentityServer Hakkinda

## IdentityServer Nedir?
* IdentityServer bir SSO (Single Sign On) implementasyonudur,
* diger bir SSO implementasyonu olan OpenID ozelligini de beraberinde saglar.
* IdentityServer bir Framework tur, kurulum yapilan bir yazilim degildir.
* Uygulamalarin guvenligini yaparken bu framework kullanilir.
Uygulama guvenligi genis bir kavram oldugu icin, burada uzerinde duracagimiz iki ana baslik vardir.
  - SSO implementasyonu
  - Web-API, implementasyonu
- IdentityServer, Security Token Service yaparken kullanilan bir framework tur.
- IdentityServer, SSO saglarken iki protokolu implemente etmistir. OpenID ve OAuth2

## Neden ihtiyac duyulur
- Application (Uygulama) 'larda gelellikle bir Authentication (kimlik dogrulama) islemi vardir. bu islem sirasinda kullanicidan
`kullaniciadi` ve `sifresi` sorularak, kullaniciya ait bilgiler dogrulandiktan sonra, kullanici application icine alinir.
- Eger birden cok application yapiyorsaniz ve ayni kullanici kitlesine hitab ediyorsaniz, tum uygulamalarda Authentication islemini
implemente (gelistirme) etmeniz gerekecektir.
- Belkide butun sistemlere ayni kodu kopyalayip yapistiracaksiniz, muhtemelen ayni database (veritabani) i kullanacaksiniz.
fakat bu ideal ve istenen bir yontem degildir,
- Authentication'un en ideal yontemi bir SSO implementasyonu kullanmaktir.
bu yontem sayesinde tek bir application, gelistirilen diger applicationlar ile haberleserek Authentication'u saglayabilmektedir.
- Bu yontem sayesinde, kullanicilar tum sistemler icin tek sifre kullanarak giris yapabilecektir, ayni zamanda sistemler arasinda
gecis yaparken, defalarca kullaniciadi-sifre girmek zorunda kalmayacaklar.
- Sonuc olarak IdentityServer, Authentication isleminin tek bir lokasyona tasinmasi ve servis haline getirilmesini saglar.
diger bir deyis ile IdentityServer,  STS (Security Token Service) rolunu ustlenmis olur.
- IdentityServer, diger applicationlar icin bir Authentication sevisi sunar.

## Nasil calisir
- Kullanici, IdentityServer uzerinden bir kereye mahsus olarak login olur,
daha sonra IdentityServer kullanicinin kimligini diger application'lara iletir.
- IdentityServer uzerinden login olmus olan client application, daha sonra ortamdaki
diger applicationlara (ornegin Web-API) cagri yaparken, IdentityServer'dan almis oldugu Token'u da
yapmis oldugu cagriya ekler. bu sayede application cagri yapanin kimligini bilir.

Bir nevi browser larda calisan cookie authentication gibi, authentication sonucu verilen ticket cookie olarak browser a kaydedilir,
daha sonra browser yaptigi tum isteklere, cagrilara cookie 'lerini de ekleyerek istekte bulurnur, bu sayede web application, cookie'ye tam olarak guvenir.

## Web-API ile birlikte kullanimi
- Web-API servisi bircok application tarafindan kullanilabilir, bunlarin arasinda browser gibi cookie tutabilen
  application lar da vardir, bazen ise cok ilkel applicationlar Web-API servisini kullanabilir.
  bu yuzden Web-API guvenligi gelistirilirken sadece browser dusunulmemelidir.
 ve Web-API servisi cookie authentication yontemini kullanmamalidir.
- Web-API servisi bir client application tarafindan cagrildigi gibi ayni zamanda bir server-side application tarafindan da cagrilabilir.

- Web-API bir mobile application tarafindan da cagrilabilir. Mobil application lar da cookie desteklemeyebilir.
- Web-API servisi baska bir Web-API servisi tarafindan cagrilabilir.

## Piyasade Bukadar SSO  urunu varken neden IdentityServer kullanilmali.
- Ana sebep, IdentityServer bir urun degildir, bir framework tur, bu sayede kullanicilara sinirsiz ozellestirme ve tasarim esnekligi saglar,  SSO yazilimi idame edilebilir, surdurulebilir, bir ozellik kazanir.
- Authentication islemi sirasindaki workflow a mudehale edebilirisniz, veya tamemen kendiniz tasarlayabilirsiniz,
ornegin kullanici adi sifreden sonra bir ara islemde notifictionlari kullaniciya gosterebilirsiniz, yada, authentication islemi sirasinda bir lisans sozlesmesi onayalatabilirsiniz.
diger turlu alinan bir urunde sinirli ozellestirmeler konfigurasyonlar ile sinirlidir, bir problem olusturunda sorumlu firmadan destek alinmak zorunda kalinir. kullanan kurum icin kapali bir kutudur. mudehale edilemez.
- Kullanicilar Active directory de kayitli ise

- IdentityServer, standalone kullanildigi gibi ayni zamanda baska bir yazilima monte edilmis olarak ta kullanilabilir.
- IdentityServer icin veritabaninin bir onemi yoktur, hangi veritabani olursa olsun c# kodu ile baglanilabilir, active directory olsada farketmez.
- IdentityServer, yazilimsal olarak genisletilebilir.
### Buyuk Resim
![resim](https://identityserver4.readthedocs.io/en/dev/_images/appArch.png)
- Browser (tarayici), web uygulamalari ile haberlersir.
- Web uygulamasi, Web-Api ile haberlesir.
- Native uygulamalar, web uygulamasi ile haberlesir,
- server-side uygulamalari web uygulamasi ile haberlersir.
- Web-Api ler Web-Api ler ile haberlesir.

## IdentityServer kullanimi
* IdentityServer ile  authentication application'u gelistirmeden once bilinmesi gereken 3 sey
1- user
2- clients
3- scopes
gelistirici IdentityServer framework une bunlari saglamasi gerekir,
Developer bu uc seyi IdentityServer a ogretmesi gerekiyor.

Kurumsal  uygulamalarda genelde 3 katman olur, front-end, middle-tier ve back-end genellikle bu uc katman icinde birtakim guvnelik gereksinimleri vardir.
front-end : web uygulamasi, telefon, destop uygulamasi olabilir, burada hangi rolun onyuzde hangi kisimlara erisim yetkisi vardir bunlarin tanimlanmasi gerekir.
middle-tier: web servis, web-api, rmi, rpc yada bir library olabilir, burada genellikle bussiness is katmani bulunur. buradki guvenlik gereksinimi ise, kimin hangi methodlara erisecegi hangi modullere erisebilecegi seklinde olabilir.
back-and: veri yonetim islemlerini yapildigi katmandir. burada da farkli turdeki veritabanlari yada veri turleri bulunabilir. buralarak hangi rollerin erisim yapabilcegi tanimlanir.
bu yuzden Yetkilendirme islemlerinin bir servis olarak external (harici) bir yerde calismasi daha efektif bit yontemdir.

---
### Obje Modeli
- IdentityServer u anlamak icin asagidaki obje modelini bilmek gerekmektedir. (Users, Clients, Scopes)
![resim](https://identityserver4.readthedocs.io/en/dev/_images/terminology.png)
- IdentityServer bir OpenID Connect provider (OP) dir, OpenID Connect protokoku ve OAuth2 yi destekler.
- IdentityServer un uslendigi rol icin farkli kaynaklarda, farkli kavramlar gorebilirsiniz, ornegin Security Token Service, Identity Provider, Authorization Server, IP-STS ve daha fazlasi.
-  IdentityServer asagidaki ozellikleri icerir.
   -  Authentication (lokal veya external provider)
   -  Session Management, oturum yonetimi saglar
   -  Manage and Authenticate Clients
   - issue identity and access token to Clients
   - validate tokens.
---
OpenId ve OAuth2 cok benzer protokellerdir, aslinda OpenID protokolu, OAuth2 nin bir uzantisidir,
* IdentityServer projesi yapmadan once bir sertifikaya ihtiyac olacak
ornek sertifika adresi : https://github.com/IdentityServer/IdentityServer4.Samples/blob/dev/MVC%20and%20API/src/IdentityServer/idsvr3test.pfx


**1- Users (Kullanicilar)**
Kullanicilar, IdentityServer userinde kayitli bir client i kullanarak verilerine erisebilirler.
Kullanici bilgilerinin, IdentityServer a verilmesi gerekiyor

burada ornek olmasi acisindan InMemoryUser objesi kullanildi,

```csharp

var users = new List<InMemoryUser>
{
    new InMemoryUser{Subject = "818727", Username = "alice", Password = "alice",
        Claims = new Claim[]
        {
            new Claim(JwtClaimTypes.Name, "Alice Smith"),
            new Claim(JwtClaimTypes.GivenName, "Alice"),
            new Claim(JwtClaimTypes.FamilyName, "Smith"),
            new Claim(JwtClaimTypes.Email, "AliceSmith@email.com"),
            new Claim(JwtClaimTypes.EmailVerified, "true", ClaimValueTypes.Boolean),
            new Claim(JwtClaimTypes.Role, "Admin"),
            new Claim(JwtClaimTypes.Role, "Geek"),
            new Claim(JwtClaimTypes.WebSite, "http://alice.com"),
            new Claim(JwtClaimTypes.Address, @"{ 'street_address': 'One Hacker Way', 'locality': 'Heidelberg', 'postal_code': 69118,'country': 'Germany' }", Constants.ClaimValueTypes.Json)
        }
    }
};

```
**2- Clients (Istemci uygulamalar)**
- Clients  bir application dir ve bu application lar IdentityServer dan token isterler.
- Kullanici client uygulamalarini kullanarak, IdentityServer dan Authentication yapar.
- Client Relaying Party RP olarak ta adlandirilir.
- Client lar IdentityServer a kaydedilmelidir.
- Client cesitleri, mobil uygulamalar, masaustu uyguylamalari, SPAs, Server-side uygulamlalar,
-  Burada dikkat edilmesi gereken kontu SPA (Single Page Application) larda OP uzerinden kimlik dogrulamasi yapmasi gerekir, ve bir client olarak kabul edilir.
- Cunku bu applicationlarin Web-API yi kullanmak icin token a ihtiyaclari vardir, Token alacaklari merkezi application ise IdentityServer dir.


```csharp

var clients = new List<Client>
{
  new Client
  {
      ClientName = "Client1",
      ClientId = "client1",
      ClientSecrets = new List<Secret>
      {
          new Secret("madeupsecret".Sha256())
      },

      AllowedGrantTypes = GrantTypes.ResourceOwnerPassword,

      AllowedScopes = new List<string>
      {
          StandardScopes.OpenId.Name,
          StandardScopes.Profile.Name,
          "api1"
      }
  }
};

```

**3- Scopes (Korunmasi gereken veri kapsami)**
- scope, erisilmek istenen kaynagin kendisidir. erisilmek istenilen kaynagi tanimlar
- cogunlukle kullanici profili yada kullanici hesap bilgileri olarak adlandirilir.
-  client appliaction larin erismek istedikleri kaynaktir (profil),
ornegin kullanicinin email adresi, adi (yani identity scopes)  
 - Authentication esnasinda, erisilemek istenilen kaynak kimligi IdentityServer(OP) a gonderilir.
 - iki tur scope tanimi yapilir, **"Identity Scopes"** ve **"Resource Scopes"**
- Identity Scopes, kullanici hakkindaki kimlik bilgilerini ister
- Resource Scopes, Web-Api (Resource Server) icindeki kaynaklardir, ornegin Takvim

- Ozetle IdentityServer hangi user un hangi client ile, neye erismek istedigi bilgisini istiyor, daha sonra buna gore bir Authentication Token, Access token yada her ikisini  uretiyor.

- Authentication Token icinde kullanici icin gerekli minimum tanimlar vardir,
- Authorization Token icinde ise, hem kullanici icin gerekli bilgiler hemde client hakkinda bilgiler bulunmaktadir.

- IdentityServer bir nuget pakati olarak projeye eklenebilir durumdadir,


```csharp
var scopes = new List<Scope>
  {
      StandardScopes.OpenId,
      StandardScopes.Profile,

      new Scope //erisilmek istenilen kaynak tanimi, Name, DisplayName v.b...
      {
          Name = "api1",
          DisplayName = "API 1",
          Description = "API 1 features and data",
          Type = ScopeType.Resource
      }
  };


```


### IdentityServer4  projesi olusturmak
- Visual studio da yeni asp.net core web application (.net core) projesi olustur
- empty project olarak ac
- project.json icine "IdentityServer4":"1.0.0-rc2" (guncel surum) eklenir.


yukaridaki 3 ana obje tanimlandiktan sonra, IdentityServer configurasyonu,
`Startup.ConfigureService` methoduna eklenebilir.

yukarda tanimlanan 3 ana obje (user, clients ve scopes)  IdentityServer'a  verilir.
artik IdentityServer'in ayarlari tanimlanmis oldu.



project.json dosyasinda asagidaki dependency eklenir.

```JSON
 "dependencies": {
    "Microsoft.NETCore.App": {  "version": "1.0.1",  "type": "platform" },
    "Microsoft.AspNetCore.Diagnostics": "1.0.0",    
    "Microsoft.AspNetCore.Server.IISIntegration": "1.0.0",
    "Microsoft.AspNetCore.Server.Kestrel": "1.0.1",
    "Microsoft.Extensions.Logging.Console": "1.0.0",
    "IdentityServer4": "1.0.0-rc2"
  },
```
daha sonra startup dosyasina asagidakiler eklenir.

```csharp
  public void ConfigureServices(IServiceCollection services)
  {
      services.AddDeveloperIdentityServer();
  }
```

* son adim ise, Startup.Configure() methodu icinde application a eklemek.


```csharp
public void Configure(IApplicationBuilder app, IHostingEnvironment env, ILoggerFactory loggerFactory)
{
    app.UseIdentityServer();
    //.....
}
```

- IdentityServer IISExpress uzerinde degilde, console da calistirilirsa daha kullanisli olur, console dan akan loglar cok faydalidir.
Program.cs dosyasinda asagidaki degisiklik yapilir.

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        Console.Title = "IdentityServer";

        var host = new WebHostBuilder()
            .UseKestrel()
            .UseUrls("http://localhost:5000")
            .UseContentRoot(Directory.GetCurrentDirectory())
            .UseIISIntegration()
            .UseStartup<Startup>()
            .Build();

        host.Run();
    }
}
```

yukarda tanimlanmis olan scopes ve clients `Startup.ConfigureServices();` methodunda
sevislere eklenebilir.

```csharp

public void ConfigureServices(IServiceCollection services)
{
    // configure identity server with in-memory stores, keys, clients and scopes
    services.AddDeveloperIdentityServer()
        .AddInMemoryScopes(scopes)
        .AddInMemoryClients(clients);
}
```
calistirdiktan sonra
http://localhost:5000/.well-known/openid-configuration
adresinden IdentityServer in calisip calismadigi kontrol edilebilir.
asagidaki gibi bir sonuc gorunur, burada IdentityServer hakkinda metadata vardir.

```JSON
{
  "issuer": "http://localhost:5000",
  "jwks_uri": "http://localhost:5000/.well-known/openid-configuration/jwks",
  "authorization_endpoint": "http://localhost:5000/connect/authorize",
  "token_endpoint": "http://localhost:5000/connect/token",
  "userinfo_endpoint": "http://localhost:5000/connect/userinfo",
  "end_session_endpoint": "http://localhost:5000/connect/endsession",
  "check_session_iframe": "http://localhost:5000/connect/checksession",
  "revocation_endpoint": "http://localhost:5000/connect/revocation",
  "introspection_endpoint": "http://localhost:5000/connect/introspect",
  "frontchannel_logout_supported": true,
  "frontchannel_logout_session_supported": true,
  "scopes_supported": [
    "api1"
  ],
  "claims_supported": [],
  "response_types_supported": [
    "code",
    "token",
    "id_token",
    "id_token token",
    "code id_token",
    "code token",
    "code id_token token"
  ],
  "response_modes_supported": [
    "form_post",
    "query",
    "fragment"
  ],
  "grant_types_supported": [
    "authorization_code",
    "client_credentials",
    "refresh_token",
    "implicit"
  ],
  "subject_types_supported": [
    "public"
  ],
  "id_token_signing_alg_values_supported": [
    "RS256"
  ],
  "token_endpoint_auth_methods_supported": [
    "client_secret_basic",
    "client_secret_post"
  ],
  "code_challenge_methods_supported": [
    "plain",
    "S256"
  ]
}
```

## IdentityServer API projesi eklenmesi
olusturulmus olan IdentityServer prjesi haricinde birde yetkilendirilecek olan API projesini olusturalim, bu proje


yeniden bir ASP.net core web-api projesi olusturulur. ve launchSettings.json dosyasindan calisacagi port farkli bir port secilir biz 5001 sectik

 Api projesine yeni bir controller eklenir. Adi IdentitiyController olarabilir.

 ```csharp
public class Program
    {
        public static void Main(string[] args)
        {
            var host = new WebHostBuilder()
                .UseKestrel()
                .UseUrls("http://localhost:5001")
                .UseContentRoot(Directory.GetCurrentDirectory())
                .UseIISIntegration()
                .UseStartup<Startup>()
                .Build();

            host.Run();
        }
    }
 ```

```csharp
[Route("identity")]
[Authorize]
public class IdentityController : ControllerBase
{
    [HttpGet]
    public IActionResult Get()
    {
        return new JsonResult(from c in User.Claims select new { c.Type, c.Value });
    }
}
```
Bu kontroler uzerinde testler yapilabilir.

project.json dosyaina `"IdentityServer4.AccessTokenValidation": "1.0.1-rc2"` satiri eklenmelidir.
burada IdentityServer u kullanan bir client servisi kullanacagiz.

`Startup.Configure()` methoduna asagidaki satirlari ekleyecegiz.

```csharp
public void Configure(IApplicationBuilder app, ILoggerFactory loggerFactory)
{
    loggerFactory.AddConsole(Configuration.GetSection("Logging"));
    loggerFactory.AddDebug();

    app.UseIdentityServerAuthentication(new IdentityServerAuthenticationOptions
    {
        Authority = "http://localhost:5000",
        ScopeName = "api1",

        RequireHttpsMetadata = false
    });

    app.UseMvc();
}
```
http://localhost:5001/identity adresinden test yapildiginda
401 hatasi alindigi gorulecektir.





## IdentityServer client-side code

- IdentitiyServer dan token alipi API ye request ayapacak bir console uygulamasi yapacagiz,
- IdentitiyServer clientlerin kullanmasi icin "identitiyModel" adinda bir library yapmistir.
- Console uygulamasi cookie tanimadigi icin ham olarak http request yapilacak, ve token kullanilacak.

Visual Studio da bir console appliation olusturup `project.json` icine `"IdentityModel": "2.0.0"` depandenty eklenir.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Net.Http;
using System.Threading.Tasks;
using IdentityModel.Client;

using IdentityModel;

using Newtonsoft.Json.Linq;

using System.Text;


namespace IdentityServerConsoleAppClient
{
    public class Program
    {
        public static void Main(string[] args)
        {

            RequestClientCredentials();

        }

        public static void RequestClientCredentials()
        {
            try
            {

                var client = new TokenClient("http://localhost:5000/connect/token", "client", "secret");
                TokenResponse tokenResponse = client.RequestClientCredentialsAsync("api1").Result;

                ShowResponse(tokenResponse);


                //call API

                var httpClient = new HttpClient
                {
                    BaseAddress = new Uri("http://localhost:5001/Identity")
                };

                httpClient.SetBearerToken(tokenResponse.AccessToken);
                var response = httpClient.GetStringAsync("identity").Result;

                Console.WriteLine("\n\nService claims:");
                Console.WriteLine(response);

            }
            catch (Exception e)
            {
                Console.WriteLine(e);
            }
        }

        private static void ShowResponse(TokenResponse response)
        {
            if (!response.IsError)
            {

                Console.WriteLine("Token response: "+response.Json);

                if (response.AccessToken.Contains("."))
                {
                    Console.WriteLine("\nAccess Token (decoded): ");

                    var parts = response.AccessToken.Split('.');
                    var header = parts[0];
                    var claims = parts[1];

                    Console.WriteLine(JObject.Parse(Encoding.UTF8.GetString(Base64Url.Decode(header))));
                    Console.WriteLine(JObject.Parse(Encoding.UTF8.GetString(Base64Url.Decode(claims))));
                }
            }
            else
            {
                if (response.ErrorType == ResponseErrorType.Http)
                {
                    Console.WriteLine("HTTP error: ");
                    Console.WriteLine(response.Error);
                    Console.WriteLine("HTTP status code: ");
                    Console.WriteLine(response.HttpStatusCode);
                }
                else
                {
                    Console.WriteLine("Protocol error response:");
                    Console.WriteLine(response.Json);
                }
            }
        }


    }
}

```
