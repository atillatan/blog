---
layout: article
permalink:
name:
file_type:
title: IdentityServer4-Angular-6-integration
description: >-
  IdentityServer4-Angular-6-integration
tags:  
category:  
sort_order: 100
rating: 300
changefreq: monthly
priority: 0.5
published: true
create_date: 2018-05-25
modified_date: 2018-05-25
created_by: atilla
modified_by: atilla
comments: true
redirect_url:
toc: false
---

# IdentityServer4-Angular-6-integration

### 1. Add Client configuration to IdentityServer4

 

```csharp

// Angular client config
new Client
{
    ClientId = "angular-client",
    ClientName = "AngularClient",
    AccessTokenLifetime = 60*60,// 60 minutes
    AllowedGrantTypes =  GrantTypes.Implicit,
    ClientSecrets ={new Secret("*****".Sha256())},
    RequireConsent = false,
    AllowAccessTokensViaBrowser = true,
    RedirectUris = {
        "http://localhost:4200" // Your Angular client url
    },
    PostLogoutRedirectUris = {
        "http://localhost:4200" // Your Angular client url
    },
    AllowedScopes = {
        IdentityServerConstants.StandardScopes.OpenId,
        IdentityServerConstants.StandardScopes.Profile,
        IdentityServerConstants.StandardScopes.Email,
        "role",
        "core.service.api"
    },
    AllowedCorsOrigins = new List<string>{
        "http://127.0.0.1:4200",
        "http://127.0.0.1:5001"
    }

}

```

### 2. Add Module to Angular Project


```shell
npm install angular-auth-oidc-client --save
```

Then configure your `app.module.ts`

```js
// app.module.ts
import { NgModule, APP_INITIALIZER } from '@angular/core';
import { HttpClientModule } from '@angular/common/http';
 
import {
    AuthModule,
    OidcSecurityService,
    OpenIDImplicitFlowConfiguration,
    OidcConfigService,
    AuthWellKnownEndpoints
} from 'angular-auth-oidc-client';
 
export function loadConfig(oidcConfigService: OidcConfigService) {
    console.log('APP_INITIALIZER STARTING');
    return () => oidcConfigService.load_using_stsServer('https://localhost:44318');
}
 
@NgModule({
    imports: [
        ...
        HttpClientModule,
        AuthModule.forRoot()
    ],
    declarations: [
        ...
    ],
    providers: [
        OidcConfigService,
        {
            provide: APP_INITIALIZER,
            useFactory: loadConfig,
            deps: [OidcConfigService],
            multi: true
        },
        ...
    ],
    bootstrap:    [AppComponent],
})

export class AppModule {

  constructor(
    private oidcSecurityService: OidcSecurityService,
    private configService: ConfigService,
  ) {
    this.configService.onConfigurationLoaded.subscribe(() => this.configService.setupSSO(this.oidcSecurityService));
    console.log('APP STARTING');
  }
}
```

Then provide API method on your RESTFull  service, it must return like below

```json
//  http://localhost:5001/api/js/json/config.js
{
  Name: "core", 
  DefaultLanguage: "tr-TR",
  DefaultPagingSize: "15",  
  DefaultAPIAddress: "http://localhost:5001",
  SSOAddress: "http://localhost:5000",
  SSOClientId: "angular-client",
  AllowedMaxExportSize: "2000",
  FileUploadPath: "wwwroot/files",
}
```


Then add `ConfigService` to Angular project
```shell
ng generate service config
```
then paste below code

```js
import { Injectable, EventEmitter, Output } from '@angular/core';
import { AuthModule, OidcSecurityService, OpenIDImplicitFlowConfiguration, AuthWellKnownEndpoints } from 'angular-auth-oidc-client';

@Injectable({
  providedIn: 'root'
})
export class ConfigService {

  // tslint:disable-next-line:no-output-on-prefix
  @Output() onConfigurationLoaded: EventEmitter<boolean> = new EventEmitter<boolean>();

  config: any;
  wellKnownEndpoints: any;

  constructor(

  ) { }

  async loadConfig(configUrl: string) {
    try {
      const response = await fetch(configUrl);

      if (!response.ok) {
        throw new Error(response.statusText);
      }

      this.config = await response.json();
      await this.loadSSOConfig(this.config.SSOAddress);
    } catch (err) {
      console.error(`ConfigService 'loadConfig' threw an error on calling ${configUrl}`, err);
      this.onConfigurationLoaded.emit(false);
    }
  }

  async loadSSOConfig(stsServer: string) {
    try {
      const response = await fetch(`${stsServer}/.well-known/openid-configuration`);

      if (!response.ok) {
        throw new Error(response.statusText);
      }

      this.wellKnownEndpoints = await response.json();
      this.onConfigurationLoaded.emit(true);
    } catch (err) {
      console.error(`ConfigService 'loadSSOConfig' threw an error on calling ${stsServer}`, err);
      this.onConfigurationLoaded.emit(false);
    }
  }

  setupSSO(oidcSecurityService: OidcSecurityService) {
    const c = new OpenIDImplicitFlowConfiguration();
    c.stsServer = this.config.SSOAddress;
    c.redirect_url = window.location.origin;
    c.client_id = this.config.SSOClientId;
    c.response_type = 'id_token token';
    c.scope = 'openid profile email role core.service.api';
    c.post_logout_redirect_uri = this.config.SSOAddress + '/Account/logout';
    c.forbidden_route = '/forbidden';
    c.unauthorized_route = '/unauthorized';
    c.auto_userinfo = true;
    c.log_console_warning_active = true;
    c.log_console_debug_active = true;
    c.max_id_token_iat_offset_allowed_in_seconds = 10;
    c.start_checksession = false;
    c.silent_renew = false;
    // c.post_login_route = this.configService.clientConfiguration.startup_route;
    const wn = new AuthWellKnownEndpoints();
    wn.setWellKnownEndpoints(this.wellKnownEndpoints);
    oidcSecurityService.setupModule(c, wn);
  }

}
```

Then generate `unauthorized` component

```shell
ng generate component `unauthorized`
```

Then pase below code to  `unauthorized.component.html`

```html
<br>

<div class="alert alert-danger">
  <strong>{{message}}</strong>
</div>

```

Then pase below code to  `unauthorized.component.ts`

```js
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-unauthorized',
  templateUrl: './unauthorized.component.html'
})
export class UnauthorizedComponent implements OnInit {

  public message: string;
  public values: any[] = [];

  constructor() {
      this.message = '401: You have no rights to access this. Please Login';
  }

  ngOnInit() {
  }

}

```

Then generate navmenu component

```shell
ng generate component navmenu
```

Then pase below code to  `navmenu.component.html`

```html
<!--#region NAVBAR -->
<nav class="navbar navbar-expand-lg  navbar-dark bg-dark">
  <a class="navbar-brand" href="#">Demo App</a>
  <button class="navbar-toggler" type="button" data-toggle="collapse" (click)="isCollapsed = !isCollapsed" data-target="#navbarText"
    aria-controls="navbarText" aria-expanded="false" aria-label="Toggle navigation">
    <span class="navbar-toggler-icon"></span>
  </button>
  <div class="collapse navbar-collapse" id="navbarText" [ngbCollapse]="isCollapsed">
    <ul class="navbar-nav mr-auto">
      <li class="nav-item" [routerLinkActive]="['active']">
        <a class="nav-link" routerLink="/home">Home</a>
      </li>
      <li class="nav-item" [routerLinkActive]="['active']">
        <a class="nav-link" routerLink="/dashboard">Dashboard</a>
      </li>
      <li class="nav-item" [routerLinkActive]="['active']"><a class="nav-link" *ngIf="!isAuthorized" (click)="login()"><span class="glyphicon glyphicon-user"></span>LOGIN</a></li>
      <li class="nav-item" [routerLinkActive]="['active']"><a class="nav-link" *ngIf="isAuthorized" (click)="logout()"><span class='glyphicon glyphicon-log-out'></span>LOGOUT</a></li>
    </ul>
  </div>
</nav>
<!--#endregion NAVBAR -->
```

Then pase below code to  `navmenu.component.ts`

```js
import { Component, OnInit, OnDestroy } from '@angular/core';
import { OidcSecurityService } from 'angular-auth-oidc-client';
import { Subscription } from 'rxjs';

@Component({
  selector: 'app-navmenu',
  templateUrl: './navmenu.component.html'
})
export class NavmenuComponent implements OnInit, OnDestroy {

  isCollapsed: Boolean = true;
  isAuthorizedSubscription: Subscription;
  isAuthorized: Boolean = false;


  constructor(
    public oidcSecurityService: OidcSecurityService
  ) {

    if (this.oidcSecurityService.moduleSetup) {
      this.doCallbackLogicIfRequired();
    } else {
      this.oidcSecurityService.onModuleSetup.subscribe(() => {
        this.doCallbackLogicIfRequired();
      });
    }
  }


  ngOnInit(): void {
    this.isAuthorizedSubscription = this.oidcSecurityService.getIsAuthorized().subscribe(
      (isAuthorized: boolean) => {
        this.isAuthorized = isAuthorized;
      });
  }

  private doCallbackLogicIfRequired() {
    if (window.location.hash) {
      this.oidcSecurityService.authorizedCallback();
    }
  }

  ngOnDestroy(): void {
    this.oidcSecurityService.onModuleSetup.unsubscribe();
  }

  login() {
    this.oidcSecurityService.authorize();
  }

  logout() {
    this.oidcSecurityService.logoff();
  }

}

```

Adding `AuthorizationGuard`
create `authorization.guard.ts` file
ad paste below code

```js
import { Injectable } from '@angular/core';
import { Router, CanActivate, ActivatedRouteSnapshot, RouterStateSnapshot } from '@angular/router';
import { Observable } from 'rxjs';
import { map } from 'rxjs/operators';

import { OidcSecurityService } from 'angular-auth-oidc-client';

@Injectable()
export class AuthorizationGuard implements CanActivate {

  constructor(
    private router: Router,
    private oidcSecurityService: OidcSecurityService
  ) { }

  public canActivate(route: ActivatedRouteSnapshot, state: RouterStateSnapshot): Observable<boolean> | boolean {
    console.log(route + '' + state);
    console.log('AuthorizationGuard, canActivate');

    return this.oidcSecurityService.getIsAuthorized().pipe(
      map((isAuthorized: boolean) => {
        console.log('AuthorizationGuard, canActivate isAuthorized: ' + isAuthorized);

        if (isAuthorized) {
          return true;
        }

        this.router.navigate(['/unauthorized']);
        return false;
      })
    );
  }
}

```
Add `AuthorizationGuard` to providers in `app.module.js`

```js
....
import { AuthorizationGuard } from './services/authorization.guard';
...

providers: [
    OidcSecurityService,
    AuthorizationGuard,
    ...
  ],
```

### Http Intercepter

The HttpClient allows you to write interceptors. We would be to intercept any outgoing HTTP request and add an authorization header. Keep in mind that injecting OidcSecurityService into the interceptor via the constructor results in a cyclic dependency. To avoid this use the injector instead.

```js
/// auth.Interceptor.ts
@Injectable()
export class AuthInterceptor implements HttpInterceptor {
    private oidcSecurityService: OidcSecurityService;
 
    constructor(private injector: Injector) {
    }
 
    intercept(req: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {
        let requestToForward = req;
 
        if (this.oidcSecurityService === undefined) {
            this.oidcSecurityService = this.injector.get(OidcSecurityService);
        }
        if (this.oidcSecurityService !== undefined) {
            let token = this.oidcSecurityService.getToken();
            if (token !== "") {
                let tokenValue = "Bearer " + token;
                requestToForward = req.clone({ setHeaders: { "Authorization": tokenValue } });
            }
        } else {
            console.debug("OidcSecurityService undefined: NO auth header!");
        }
 
        return next.handle(requestToForward);
    }
}
```
Then add to `app.module.ts` following code

```js
import { HttpClientModule, HTTP_INTERCEPTORS } from '@angular/common/http';
...
import { AuthInterceptor } from './services/auth.Interceptor';
...
providers: [

    .....
    {
      provide: HTTP_INTERCEPTORS,
      useClass: AuthInterceptor,
      multi: true
    },
    ....
   
  ],

```


### 3. API configuration

Add library to your project.csproj

```xml
// project.csproj
  <ItemGroup>
    <PackageReference Include="IdentityServer4.AccessTokenValidation" Version="2.4.0" />    
  </ItemGroup>
```

Then add below code to `startup.cs`

```csharp
public void ConfigureServices(IServiceCollection services){

    services.AddCors();

    services.AddMvc()

    // ...
    services.AddAuthorization()
    .AddAuthentication("Bearer")
    .AddIdentityServerAuthentication(options =>
    {
        options.Authority = "http://localhost:5000";
        options.RequireHttpsMetadata = false;
        options.ApiName = "core.service.api";
    });
    // ...
}

public void Configure(IApplicationBuilder app, IHostingEnvironment env){
// ...

app.UseAuthentication();

// ...
}
```


