---
layout: article
permalink:
name:
file_type:
title: Making Enterprise Angular Project Step by Step
description: >-
  Making Enterprise Angular Project Step by Step
tags:  
category:  
sort_order: 21
rating: 300
changefreq: monthly
priority: 0.5
published: true
create_date: 2018-05-25T10:20:00Z
modified_date: 2018-05-25
created_by: atilla
modified_by: atilla
comments: true
redirect_url:
toc: false
---

# Making Enterprise Angular Project Step by Step

This project demonstrates how to build Enterprise Grade Angular Project.

## When we want to build Enterprise Project, We always need following pieces/functionalities 

- **User Interface and Design:** Bootstrap and Material Design give you easily create beautiful user interfaces, nowadays these two libraries is best practices

- **Web Icons:** We will need some useful icons on our project `Material Icons` is more common for Angular projects

- **Enterprise CSS Style:** All Enterprise project must have common enterprise style, you can add global CSS file for this purpose

- **Enterprise Utility Class:** All Enterprise project must have common utility methods, you can add global JavaScript/TypeScript file for this purpose.

- **JQuery:** Generally we don't use `JQuery` in Angular project but some developer likes JQuery, they believe JQuery more handy tool than others. "Just in case", you can add JQuery to your project.

- **Best Practice Angular Modules:** You can add best practice Angular modules to your project, for example, CommonModule, BrowserModule, HttpClientModule, FromsModule, AppRoutingModule, BrowserAnimationsModule, Mat**Module etc.

- **Browser Storage Module:** SPA applications need to use these browser storages `SessionStorage`, `LocalStorage` 

- **Configuration:** All Enterprise applications needs `Configuration` you can take configuration from js/json file like this `http://localhost:4200/assets/config.js`

```js
{
    Name: "core",
    AssetsUrl: "http://asset.mycompany.com",
    DefaultLanguage: "en",
    DefaultPagingSize: "15",
    DefaultBrowserTitle: "My Company",
    DefaultWebAPIAddress: "http://localhost:5001",
    SSOAddress: "http://sso.mycompany.com",    
    AllowedMaxExportSize: "2000",
    FileUploadPath: "wwwroot/files",
    //...
}
```

- **Authentication Interceptor:** All Enterprise applications must have `Authentication`, For this purpose, you can use "IdentityServer4". It supports `OpenID` and `OAuth2`, Then you can make `AuthenticationInterceptor` in Angular project in order to add the token to http header.

- **Authorization Guard:** A Common usage of Authorization guard is activating or deactivating authorized components

- **Unauthorized Component:** If user don't have an access permission to specific pages, you can redirect `unauthorized` page.

- **Internationalization:** By default, Angular uses the locale en-US, which is English as spoken in the United States of America, if you want to use another locale you can use `LOCALE_ID`

- **Application Loading Animation:** SPA application always use loading animation for the first visit.

- **Page Load Animation:** Using page routing animation is a common approach for SPA. The purpose of animation  related UX  concerns

- **Menu:** All application must have `Menu` for navigation. 

- **Progress Bar:** According to UX Concerns, some server requests takes a long time, you can show what's going on the background with a progress bar.

- **Dialog Window:** We are building an interactive web application. Sometimes we want to ask/show some confirmation/information to the user, for example, delete confirmation.

- **Notifications:**  According to UX Concerns, Interactive applications always give feedback to the user. Best way to notify the user is using `toast` component.

- **Common Back-End and Front-End Objects** Angular applications can communicate with back-end using `JSON`. Enterprise application always uses common object between Back-end and Front-end because we want to know Request.IsSuccess, what is the resultType (information, Success, Warning, Error) is response have a message or exception? for this purpose, we want to use some common object between to side. For Example:

```js
export class ServiceResponse<T> {
    public IsSuccess: boolean;
    public ResultType: ResultType;
    public Message: string;
    public TotalCount: number;
    public Data: T;
}

export enum ResultType {
    Information = 1,
    Validation = 2,
    Success = 3,
    Warning = 4,
    Error = 5,
}
```

- **Interceptor for Server Side Messages:** Usually Enterprise application have Exception handling, we can intercept server-side messages/exceptions with Angular Interceptor.

- **CRUD Operation Service:** Best way to prevent code repetition is making a common class. Sometimes we always repeat same code on the same application layer. For example database layer always have CRUD (Create, Read, Update, Delete) operations, But Enterprise applications generally use common object/classes for this. We can make Angular service that includes these methods: post, get, put, delete

- **Translate Service:** If we want to build multilingual application we must create translator service.

- **Delete Confirmation:** If we want to make enterprise application, we usually show data with data grid or data table, then we have to implement delete confirmation on table or grid.

- **ToolTip:** Sometimes we use Icons on the user interface, in enterprise application we have to show icon meaning with tooltip.

- **Data Table or Data Grid:** If we want to make enterprise application, we usually show data with data grid or data table.

- **Database Pagination:** Sometimes we have a lot of record on the database table, we don't show all record on the user interface, it's effect application performance and usability of the application. Pagination is the best way to show data.


## 1. Create Angular Project

- Download nodejs from [https://nodejs.org](https://nodejs.org) and install it

- Open your terminal or, Windows PowerShell, then execute following commands


**Install Angular**

```shell
npm install -g @angular/cli
```

**Create Angular Project**

```shell
ng new Enterprise-Angular-Project
cd Enterprise-Angular-Project
ng serve --open
```

Using the --open (or just -o) option will automatically open your browser on http://localhost:4200/.

you can also read the following tutorial [https://angular.io/guide/quickstart](https://angular.io/guide/quickstart)

## 2. Install Dependencies

**Install Angular Material and Angular CDK**

```shell
npm install --save @angular/material @angular/cdk
npm install moment --save
```

Moment.JS is an intelligent JavaScript library to Parse, validate, manipulate, and display dates and times for given formats.
`moment` will be used from DateTimePicket component

Import required modules, that you want to use
in this example, I want to use Material Modules

Then modify your `app.module.ts` like this

```js
// app.module.ts
//...
import {
  MatAutocompleteModule, MatBadgeModule, MatBottomSheetModule, MatButtonModule, MatButtonToggleModule,
  MatCardModule, MatCheckboxModule, MatChipsModule, MatDatepickerModule, MatDialogModule, MatDividerModule,
  MatExpansionModule, MatGridListModule, MatIconModule, MatInputModule, MatListModule, MatMenuModule,
  MatNativeDateModule, MatPaginatorModule, MatProgressBarModule, MatProgressSpinnerModule, MatRadioModule,
  MatRippleModule, MatSelectModule, MatSidenavModule, MatSliderModule, MatSlideToggleModule, MatSnackBarModule,
  MatSortModule, MatStepperModule, MatTableModule, MatTabsModule, MatToolbarModule, MatTooltipModule, MatTreeModule,
} from '@angular/material';
import {CdkTableModule} from '@angular/cdk/table';
//...

@NgModule({
  imports: [
    //...
    CdkTableModule, MatAutocompleteModule, MatBadgeModule, MatBottomSheetModule, MatButtonModule,
    MatButtonToggleModule, MatCardModule, MatCheckboxModule, MatChipsModule, MatStepperModule,
    MatDatepickerModule, MatDialogModule, MatDividerModule, MatExpansionModule, MatGridListModule,
    MatIconModule, MatInputModule, MatListModule, MatMenuModule, MatNativeDateModule, MatPaginatorModule,
    MatProgressBarModule, MatProgressSpinnerModule, MatRadioModule, MatRippleModule, MatSelectModule,
    MatSidenavModule, MatSliderModule, MatSlideToggleModule, MatSnackBarModule, MatSortModule,
    MatTableModule, MatTabsModule, MatToolbarModule, MatTooltipModule, MatTreeModule,
    //...
]
})
//...
```

Including a theme is required to apply all of the core and theme styles to your application.

To get started with a pre-built theme, include one of Angular Material's prebuilt themes globally in your application. If you're using the Angular CLI, you can add this to your `styles.css`:

```css
// styles.css
@import "~@angular/material/prebuilt-themes/indigo-pink.css";
```

Some components (mat-slide-toggle, mat-slider, matTooltip) rely on HammerJS for gestures. In order to get the full feature-set of these components, HammerJS must be loaded into the application.

```shell
npm install --save hammerjs
```

After installing, import it on your app's entry point (e.g. src/main.ts).

```js
// main.ts
import 'hammerjs';
```

**Add Material Icons**

```html
// index.html
<link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
```

you can also use the following tutorial [https://material.angular.io/guide/getting-started](https://material.angular.io/guide/getting-started)


## 3. Install Bootstrap, Jquery, and popper.js

```shell
npm i bootstrap --save
npm i ngx-bootstrap --save
npm i jquery --save
npm i popper.js --save
```

Add bootstrap to `angular.json`

```js
"styles": [
  "node_modules/bootstrap/dist/css/bootstrap.min.css",
],
"scripts": [ 
  "node_modules/jquery/dist/jquery.slim.min.js",
  "node_modules/popper.js/dist/popper.min.js",
  "node_modules/bootstrap/dist/js/bootstrap.min.js"
]
```

for more details read following link [https://github.com/valor-software/ngx-bootstrap](https://github.com/valor-software/ngx-bootstrap)

## 3. Add Custom Global CSS 

Create a file named `custom.css`  in the assets folder
then insert following code

```css
.test-style {
    color: red;
}
```

add your `custom.css` to angular.json

```json
"architect": {
    "build": {
	 "options": {
		  ...
		  "styles": [
			  "src/assets/custom.css",
			  "src/styles.css"
			],
		  ...
		}
    }
}
```
Then test it in `index.html`

```html
<body>
 <h1 class="test-style">Test</h1>
 // ...
 
</body>
```
you can also read following the link [http://atilla.tanrikulu.biz/Using-CSS-and-JavaScript-to-an-Angular-Project/](http://atilla.tanrikulu.biz/Using-CSS-and-JavaScript-to-an-Angular-Project/)

## 4. Add Custom JavaScript file

Create files named `custom-utility.js`, `custom-module.js`  in the assets folder

```json
"architect": {
    "build": {
	"options": {
	    ...
		"scripts": [             
                ...
                  "src/assets/custom-utility.js",
                  "src/assets/custom-module.js"            
                ],
           ...
      }
    }
}
```

Then test it in `app.component.ts`


```js
// app-component.ts
import { Component, OnInit } from '@angular/core';
import { CustomModule } from '../assets/custom-module.js'; // <= inserted line 1.

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent implements OnInit {
  module: CustomModule = new CustomModule();// <= inserted line 2.
 
 ngOnInit() {    
    this.module.testMethod1('custom module'); // <= inserted line 3.
  }
}

```

you can also read following link [http://atilla.tanrikulu.biz/Using-CSS-and-JavaScript-to-an-Angular-Project/](http://atilla.tanrikulu.biz/Using-CSS-and-JavaScript-to-an-Angular-Project/)


## 5. Add Best Practice Angular Modules To Your Angular Project

Create `app-routing.module.ts` 

```shell
// --flat puts the file in src/app instead of its own folder.
// --module=app tells the CLI to register it in the imports array of the AppModule.

ng generate module app-routing --flat --module=app
```
then insert following code 

```js
import { NgModule } from '@angular/core';
import { RouterModule, Routes } from '@angular/router';


const routes: Routes = [
  { path: '', redirectTo: '/', pathMatch: 'full' }
];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule { }

```

Then insert following code to `app.module.ts`

```js
import { NgModule } from '@angular/core';

import { BrowserModule } from '@angular/platform-browser';
import { CommonModule } from '@angular/common';
import { HttpClientModule } from '@angular/common/http';
import { FormsModule, ReactiveFormsModule } from '@angular/forms';
import { AppRoutingModule } from './app-routing.module';
import { BrowserAnimationsModule } from '@angular/platform-browser/animations';
import { MatAutocompleteModule, MatBadgeModule, MatBottomSheetModule, MatButtonModule, MatButtonToggleModule,
  MatCardModule, MatCheckboxModule, MatChipsModule, MatDatepickerModule, MatDialogModule, MatDividerModule,
  MatExpansionModule, MatGridListModule, MatIconModule, MatInputModule, MatListModule, MatMenuModule,
  MatNativeDateModule, MatPaginatorModule, MatProgressBarModule, MatProgressSpinnerModule, MatRadioModule,
  MatRippleModule, MatSelectModule, MatSidenavModule, MatSliderModule, MatSlideToggleModule, MatSnackBarModule,
  MatSortModule, MatStepperModule, MatTableModule, MatTabsModule, MatToolbarModule, MatTooltipModule, MatTreeModule}
  from '@angular/material';
import { AppComponent } from './app.component';


@NgModule({
  imports: [
    BrowserModule,
    CommonModule,
    HttpClientModule,
    FormsModule, ReactiveFormsModule,
    AppRoutingModule,
    BrowserAnimationsModule,
    CdkTableModule, MatAutocompleteModule, MatBadgeModule, MatBottomSheetModule, MatButtonModule,
    MatButtonToggleModule, MatCardModule, MatCheckboxModule, MatChipsModule, MatStepperModule,
    MatDatepickerModule, MatDialogModule, MatDividerModule, MatExpansionModule, MatGridListModule,
    MatIconModule, MatInputModule, MatListModule, MatMenuModule, MatNativeDateModule, MatPaginatorModule,
    MatProgressBarModule, MatProgressSpinnerModule, MatRadioModule, MatRippleModule, MatSelectModule,
    MatSidenavModule, MatSliderModule, MatSlideToggleModule, MatSnackBarModule, MatSortModule,
    MatTableModule, MatTabsModule, MatToolbarModule, MatTooltipModule, MatTreeModule
  ],
  declarations: [
    AppComponent
  ],
  providers: [],
  bootstrap: [AppComponent],
  entryComponents: []
})
export class AppModule { }

```

## 6. Add Browser Storage Module

In this example, I'll use `ngx-webstorage` module
you can use the installation guide [https://www.npmjs.com/package/ngx-webstorage](https://www.npmjs.com/package/ngx-webstorage)

```shell
npm install --save ngx-webstorage
```
Change your `app.module.ts` like this

```js
import { NgModule } from '@angular/core';

import { BrowserModule } from '@angular/platform-browser';
import { CommonModule } from '@angular/common';
import { HttpClientModule } from '@angular/common/http';
import { FormsModule, ReactiveFormsModule } from '@angular/forms';
import { AppRoutingModule } from './app-routing.module';
import { BrowserAnimationsModule } from '@angular/platform-browser/animations';
import { MatAutocompleteModule, MatBadgeModule, MatBottomSheetModule, MatButtonModule, MatButtonToggleModule,
  MatCardModule, MatCheckboxModule, MatChipsModule, MatDatepickerModule, MatDialogModule, MatDividerModule,
  MatExpansionModule, MatGridListModule, MatIconModule, MatInputModule, MatListModule, MatMenuModule,
  MatNativeDateModule, MatPaginatorModule, MatProgressBarModule, MatProgressSpinnerModule, MatRadioModule,
  MatRippleModule, MatSelectModule, MatSidenavModule, MatSliderModule, MatSlideToggleModule, MatSnackBarModule,
  MatSortModule, MatStepperModule, MatTableModule, MatTabsModule, MatToolbarModule, MatTooltipModule, MatTreeModule}
  from '@angular/material';
import { Ng2Webstorage } from 'ngx-webstorage';
import { AppComponent } from './app.component';


@NgModule({
  imports: [
    BrowserModule,
    CommonModule,
    HttpClientModule,
    FormsModule, ReactiveFormsModule,
    AppRoutingModule,
    BrowserAnimationsModule,
    CdkTableModule, MatAutocompleteModule, MatBadgeModule, MatBottomSheetModule, MatButtonModule,
    MatButtonToggleModule, MatCardModule, MatCheckboxModule, MatChipsModule, MatStepperModule,
    MatDatepickerModule, MatDialogModule, MatDividerModule, MatExpansionModule, MatGridListModule,
    MatIconModule, MatInputModule, MatListModule, MatMenuModule, MatNativeDateModule, MatPaginatorModule,
    MatProgressBarModule, MatProgressSpinnerModule, MatRadioModule, MatRippleModule, MatSelectModule,
    MatSidenavModule, MatSliderModule, MatSlideToggleModule, MatSnackBarModule, MatSortModule,
    MatTableModule, MatTabsModule, MatToolbarModule, MatTooltipModule, MatTreeModule,
    Ng2Webstorage
  ],
  declarations: [
    AppComponent
  ],
  providers: [],
  bootstrap: [AppComponent],
  entryComponents: []
})
export class AppModule { }
```

**Move your root component to root directory**
Create `root` directory
and move `app.component.*` to root directory then fix path errors.


## 7. Add Configuration Service

If you want to load front-end configuration from server, follow these steps/

Generate service in `services` directory

```shell
ng generate service services/config
```

Then insert following code

```js
import { Injectable, EventEmitter, Output, Injector } from '@angular/core';

@Injectable({
  providedIn: 'root'
})
export class ConfigService {

  // tslint:disable-next-line:no-output-on-prefix
  @Output() onConfigurationLoaded: EventEmitter<boolean> = new EventEmitter<boolean>();

  config: any;  

  constructor() { }

  async loadConfig(configUrl: string) {

    try {
      await this.loadAPIConfig(configUrl);
      // load other configurations
      this.onConfigurationLoaded.emit(true);
    } catch (err) {
      console.error(`ConfigService threw an error on calling ${configUrl}`, err);
      this.onConfigurationLoaded.emit(false);
    }
  }

  private async loadAPIConfig(configUrl: string) {

    const response = await fetch(configUrl);

    if (!response.ok) {
      throw new Error(response.statusText);
    }

    this.config = await response.json();
  }

}

```

Change `app.module.ts` code like as

```js
import { NgModule, APP_INITIALIZER } from '@angular/core';

import { BrowserModule } from '@angular/platform-browser';
import { CommonModule } from '@angular/common';
import { HttpClientModule } from '@angular/common/http';
import { FormsModule, ReactiveFormsModule } from '@angular/forms';
import { AppRoutingModule } from './app-routing.module';
import { BrowserAnimationsModule } from '@angular/platform-browser/animations';
import { MatAutocompleteModule, MatBadgeModule, MatBottomSheetModule, MatButtonModule, MatButtonToggleModule,
  MatCardModule, MatCheckboxModule, MatChipsModule, MatDatepickerModule, MatDialogModule, MatDividerModule,
  MatExpansionModule, MatGridListModule, MatIconModule, MatInputModule, MatListModule, MatMenuModule,
  MatNativeDateModule, MatPaginatorModule, MatProgressBarModule, MatProgressSpinnerModule, MatRadioModule,
  MatRippleModule, MatSelectModule, MatSidenavModule, MatSliderModule, MatSlideToggleModule, MatSnackBarModule,
  MatSortModule, MatStepperModule, MatTableModule, MatTabsModule, MatToolbarModule, MatTooltipModule, MatTreeModule } from '@angular/material';
import { Ng2Webstorage } from 'ngx-webstorage';
import { AppComponent } from './root/app.component';
import { ConfigService } from './services/config.service';

export function loadConfig(configService: ConfigService) {
  console.log('APP_INITIALIZER STARTING');  
  return () => configService.loadConfig(`http://localhost:5001/api/js/json/config.js`);
}

@NgModule({
  imports: [
    BrowserModule,
    CommonModule,
    HttpClientModule,
    FormsModule, ReactiveFormsModule,
    AppRoutingModule,
    BrowserAnimationsModule,
    CdkTableModule, MatAutocompleteModule, MatBadgeModule, MatBottomSheetModule, MatButtonModule,
    MatButtonToggleModule, MatCardModule, MatCheckboxModule, MatChipsModule, MatStepperModule,
    MatDatepickerModule, MatDialogModule, MatDividerModule, MatExpansionModule, MatGridListModule,
    MatIconModule, MatInputModule, MatListModule, MatMenuModule, MatNativeDateModule, MatPaginatorModule,
    MatProgressBarModule, MatProgressSpinnerModule, MatRadioModule, MatRippleModule, MatSelectModule,
    MatSidenavModule, MatSliderModule, MatSlideToggleModule, MatSnackBarModule, MatSortModule,
    MatTableModule, MatTabsModule, MatToolbarModule, MatTooltipModule, MatTreeModule,
    Ng2Webstorage
  ],
  declarations: [
    AppComponent
    
  ],
  providers: [
    ConfigService,
    {
      provide: APP_INITIALIZER,
      useFactory: loadConfig,
      multi: true,
      deps: [ConfigService]
    }
  ],
  bootstrap: [AppComponent],
  entryComponents: []
})
export class AppModule {

  constructor(
    private configService: ConfigService,
  ) {
    console.log('APP STARTING');

    this.configService.onConfigurationLoaded.subscribe(() => {
      // do something, after configuration load
      console.log('Configuration loaded.');
    });

  }
}

```

## 8. Add Authentication 

In this example, I'll use "[IdentityServer4](http://identityserver.io/)" on server-side and I'll use "[angular-auth-oidc-client](https://github.com/damienbod/angular-auth-oidc-client)" angular module on client-side.

```shell
npm install angular-auth-oidc-client --save
```
Change your `app.module.ts` like this

```js
import { NgModule, APP_INITIALIZER } from '@angular/core';

import { BrowserModule } from '@angular/platform-browser';
import { CommonModule } from '@angular/common';
import { HttpClientModule } from '@angular/common/http';
import { FormsModule, ReactiveFormsModule } from '@angular/forms';
import { AppRoutingModule } from './app-routing.module';
import { BrowserAnimationsModule } from '@angular/platform-browser/animations';
import { MatAutocompleteModule, MatBadgeModule, MatBottomSheetModule, MatButtonModule, MatButtonToggleModule,
  MatCardModule, MatCheckboxModule, MatChipsModule, MatDatepickerModule, MatDialogModule, MatDividerModule,
  MatExpansionModule, MatGridListModule, MatIconModule, MatInputModule, MatListModule, MatMenuModule,
  MatNativeDateModule, MatPaginatorModule, MatProgressBarModule, MatProgressSpinnerModule, MatRadioModule,
  MatRippleModule, MatSelectModule, MatSidenavModule, MatSliderModule, MatSlideToggleModule, MatSnackBarModule,
  MatSortModule, MatStepperModule, MatTableModule, MatTabsModule, MatToolbarModule, MatTooltipModule, MatTreeModule  } from '@angular/material';
import { Ng2Webstorage } from 'ngx-webstorage';

import { AppComponent } from './root/app.component';
import { ConfigService } from './services/config.service';
import { AuthModule, OidcSecurityService, OpenIDImplicitFlowConfiguration, AuthWellKnownEndpoints } from 'angular-auth-oidc-client';

export function loadConfig(configService: ConfigService) {
  console.log('APP_INITIALIZER STARTING');  
  return () => configService.loadConfig(`http://localhost:5001/api/js/json/config.js`);
}

@NgModule({
  imports: [
    BrowserModule,
    CommonModule,
    HttpClientModule,
    FormsModule, ReactiveFormsModule,
    AppRoutingModule,
    BrowserAnimationsModule,
    CdkTableModule, MatAutocompleteModule, MatBadgeModule, MatBottomSheetModule, MatButtonModule,
    MatButtonToggleModule, MatCardModule, MatCheckboxModule, MatChipsModule, MatStepperModule,
    MatDatepickerModule, MatDialogModule, MatDividerModule, MatExpansionModule, MatGridListModule,
    MatIconModule, MatInputModule, MatListModule, MatMenuModule, MatNativeDateModule, MatPaginatorModule,
    MatProgressBarModule, MatProgressSpinnerModule, MatRadioModule, MatRippleModule, MatSelectModule,
    MatSidenavModule, MatSliderModule, MatSlideToggleModule, MatSnackBarModule, MatSortModule,
    MatTableModule, MatTabsModule, MatToolbarModule, MatTooltipModule, MatTreeModule,
    Ng2Webstorage,
    AuthModule.forRoot(),
  ],
  declarations: [
    AppComponent    
  ],
  providers: [
    ConfigService,
    {
      provide: APP_INITIALIZER,
      useFactory: loadConfig,
      multi: true,
      deps: [ConfigService]
    },
    OidcSecurityService
  ],
  bootstrap: [AppComponent],
  entryComponents: []
})
export class AppModule {

  constructor(
     private oidcSecurityService: OidcSecurityService,
    private configService: ConfigService
  ) {
    console.log('APP STARTING');

    this.configService.onConfigurationLoaded.subscribe(() => {
      // do something, after configuration load
      console.log('Configuration loaded.');
      this.configService.setupSSO(this.oidcSecurityService);
    });

  }
}
```

Then change `app.component.html` like this

```html
<div class="button-row">
 <button mat-raised-button color="primary" *ngIf="!isAuthorized" (click)="login()"><i class="material-icons">exit_to_app</i> Login </button>
  <button mat-raised-button color="primary" *ngIf="isAuthorized" (click)="logout()"><i class="material-icons">power_settings_new</i> Logout</button>
</div>
```

Then change  `app.component.ts` like this

```js
import { Component, OnInit, OnDestroy } from '@angular/core';
import { OidcSecurityService } from 'angular-auth-oidc-client';
import { Subscription } from 'rxjs';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html'
})
export class AppComponent implements OnInit, OnDestroy {

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

  public ngOnDestroy(): void {
    this.oidcSecurityService.onModuleSetup.unsubscribe();
  }

  public login() {
    this.oidcSecurityService.authorize();
  }

  public logout() {
    this.oidcSecurityService.logoff();
  }

}
```

Then if you want to get user information from API, Change your code  like this

```js
import { Component, OnInit, OnDestroy } from '@angular/core';
import { OidcSecurityService } from 'angular-auth-oidc-client';
import { Subscription } from 'rxjs';
import { LocalStorageService, SessionStorageService } from 'ngx-webstorage';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html'
})
export class AppComponent implements OnInit, OnDestroy {

  isCollapsed: Boolean = true;
  isAuthorizedSubscription: Subscription;
  isAuthorized: Boolean = false;
  userData: any;
  userInfo: any;

  constructor(    
    public oidcSecurityService: OidcSecurityService,
    private sessionStorage: SessionStorageService    
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
        if (this.isAuthorized === true) {
          this.saveUserInfo();
        }
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

  saveUserInfo() {
    // GetUserInfo and set sessionStorage
    this.oidcSecurityService.getUserData().subscribe(
      (data) => {
        if (data !== '') {
          this.userData = data;
          const id: number = +this.userData.sub;
          // Get your user informatin from service, then save sessionStorage
          // this.userService.getUser(id).subscribe(serviceResponse => {
          //   if (serviceResponse != null) {
          //     this.userInfo = serviceResponse.Data;
          //     this.sessionStorage.clear('userinfo');
          //     this.sessionStorage.store('userinfo', this.userInfo);
          //   }
          // });
        }
      }
    );
  }

}


```

**Add Http Interceptor for Authentication**

You would intercept any outgoing HTTP request and add an authorization header to http header
The HttpClient allows you to write interceptors
Keep in mind that injecting OidcSecurityService into the interceptor via the constructor results in a cyclic dependency. To avoid this use the injector instead.

Create `auth.interceptor.ts` in the services directory

```js
import { Injectable, Injector } from '@angular/core';
import { HttpInterceptor, HttpRequest, HttpHandler, HttpEvent, HttpResponse } from '@angular/common/http';
import { OidcSecurityService } from 'angular-auth-oidc-client';
import { Observable } from 'rxjs';

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
            const token = this.oidcSecurityService.getToken();
            if (token !== '') {
                const tokenValue = 'Bearer ' + token;
                requestToForward = req.clone({ setHeaders: { 'Authorization': tokenValue } });
            }
        } else {
            console.log('OidcSecurityService undefined: NO auth header!');
        }

        return next.handle(requestToForward);
    }
}

```

Change your `app.module.ts` like this

```js
//...
import { HttpClientModule, HTTP_INTERCEPTORS } from '@angular/common/http';
import { AuthInterceptor } from './services/auth.Interceptor';
//...
@NgModule({
  imports: [
    //..
  ],
  providers: [
    //..  
    {
      provide: HTTP_INTERCEPTORS,
      useClass: AuthInterceptor,
      multi: true
    }
    //..
  ],


```

**Use AuthorizationGuard**

A Common usage of Authorization guard is activating and deactivating components

Create `auth.guard.ts` in the services directory

```js
import { Injectable } from '@angular/core';
import { Router, CanActivate, ActivatedRouteSnapshot, RouterStateSnapshot } from '@angular/router';
import { Observable } from 'rxjs';
import { map } from 'rxjs/operators';

import { OidcSecurityService } from 'angular-auth-oidc-client';

@Injectable()
export class AuthGuard implements CanActivate {

  constructor(
    private router: Router,
    private oidcSecurityService: OidcSecurityService
  ) { }

  public canActivate(route: ActivatedRouteSnapshot, state: RouterStateSnapshot): Observable<boolean> | boolean {
    console.log(route + '' + state);
    console.log('AuthGuard, canActivate');

    return this.oidcSecurityService.getIsAuthorized().pipe(
      map((isAuthorized: boolean) => {
        console.log('AuthGuard, canActivate isAuthorized: ' + isAuthorized);

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

Then add following lines to `app.module.ts`

```js
//..
import { AuthGuard } from './services/auth.guard';
//...
@NgModule({
//..
  declarations: [
    AppComponent
  ],
  providers: [
    //...
    AuthGuard
  ],
})
```

Then add following lines to `app-routing.module.ts`

```js
//...
import { AuthGuard } from './services/auth.guard';

const routes: Routes = [
  { path: '', redirectTo: '/', pathMatch: 'full' },
  { path: 'home', component: HomeComponent, canActivate: [AuthorizationGuard] } 
];

 }

```

**Create "Unauthorized" Component**

`ng generate component unauthorized`

insert following code to `unauthorized.component.html`

```html
<br>
<mat-card>
  <strong>"{"{message"}"}</strong>
  <strong> { {message } }</strong>
  <strong> {{ message }}</strong>
  <strong> \{\{ message \}\}</strong>
  <strong> `{`{ message `}`}</strong>
  <strong> '{'{ message '}'}</strong>
</mat-card>


```

insert following code to `unauthorized.component.ts`

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

Then add routing line to `app-routing.module.ts`

`{ path: 'unauthorized', component: UnauthorizedComponent }`


**Create Home Component**

`ng generate component home`

insert following code to `unauthorized.component.html`

```html
<br>

<div class="alert alert-danger">
  <strong>Home is working</strong>
</div>

```

Then add routing line to `app-routing.module.ts`

`{ path: 'home', component: HomeComponent, canActivate: [AuthorizationGuard] },`

Add following line to `app.component.html`

`<router-outlet></router-outlet>`

Then change your routing configuration like this

```js
const routes: Routes = [
  { path: '', redirectTo: '/home', pathMatch: 'full' },
  { path: 'home', component: HomeComponent, canActivate: [AuthGuard] },
  { path: 'unauthorized', component: UnauthorizedComponent }
];
```

you can see `AuthGuard` usage in above code.

## 8. Add Internationalization

By default, Angular uses the locale en-US, which is English as spoken in the United States of America.

If you use JIT, you also need to define the LOCALE_ID provider in your main module:

```js
// src/app/app.module.ts
import { LOCALE_ID, NgModule } from '@angular/core';
import { registerLocaleData } from '@angular/common';
import localeTr from '@angular/common/locales/tr';

//..
@NgModule({
  imports: [ BrowserModule ],
  declarations: [ AppComponent ],
  providers: [ { provide: LOCALE_ID, useValue: 'en-US' } ],
  bootstrap: [ AppComponent ]
})

constructor() {
registerLocaleData(localeTr, 'tr');
}
```

Then add material `datepicker` component to `app.component.html`
and look int datepicker local month, day names

```html

<mat-form-field>
  <input matInput [matDatepicker]="picker" placeholder="Choose a date">
  <mat-datepicker-toggle matSuffix [for]="picker"></mat-datepicker-toggle>
  <mat-datepicker #picker></mat-datepicker>
</mat-form-field>

```

## 9. Add Application Loading Animation

Add your css file the following code

```css
/* #region loading */

#loading {
  position: absolute;
  left: 50%;
  top: 50%;
  z-index: 1;
  width: 150px;
  height: 150px;
  margin: -75px 0 0 -75px;
  border: 10px solid #f3f3f3;
  border-radius: 50%;
  border-top: 10px solid #3498db;
  width: 100px;
  height: 100px;
  -webkit-animation: spin 2s linear infinite;
  animation: spin 2s linear infinite;
}

@-webkit-keyframes spin {
  0% {-webkit-transform: rotate(0deg);}
  100% {-webkit-transform: rotate(360deg);}
}

@keyframes spin {
  0% {transform: rotate(0deg);}
  100% {transform: rotate(360deg);}
}

/* #endregion loading */
```
Then change your `index.html body` like this.

```html
<body style="margin: 0px;">
  <app-root>
    <div id="loading"></div>
  </app-root>
</body>
```

**Add page view effect bottom to up**

add following style your css file

```css
/* #region Adimate page bottom to up */

.animate-bottom {
  position: relative;
  -webkit-animation-name: animatebottom;
  -webkit-animation-duration: 0.5s;
  animation-name: animatebottom;
  animation-duration: 0.5s;
}

@-webkit-keyframes animatebottom {
  from {bottom: -30px;opacity: 0}
  to {bottom: 0px;opacity: 1}
}

@keyframes animatebottom {
  from {bottom: -30px;opacity: 0}
  to {bottom: 0;opacity: 1}
}

/* #endregion*/
```
Then change your page html `user.component.html` like this

```html
<div class="animate-bottom">
<!-- //.... -->
</div>
```

## 10. Add Menu

Add following code to `app.component.html`

```html
<div *ngIf="loading">
  <mat-progress-bar mode="indeterminate"></mat-progress-bar>
</div>

<mat-toolbar color="primary">
  <button mat-icon-button routerLink="/home">
    <mat-icon>home</mat-icon>
  </button>
  <button mat-button routerLink="/home">Home</button>
  <button mat-button routerLink="/contact">Contact</button>
  <button mat-button [matMenuTriggerFor]="menu">Languages</button>
  <mat-menu #menu="matMenu">
    <button mat-menu-item>English</button>
    <button mat-menu-item>Turkce</button>
  </mat-menu>
  <button mat-button  *ngIf="!isAuthorized" (click)="login()">
    <i class="material-icons">exit_to_app</i> Login </button>
  <button mat-button *ngIf="isAuthorized" (click)="logout()">
    <i class="material-icons">power_settings_new</i> Logout</button>
</mat-toolbar>
 

<div class="animate-bottom">
  <router-outlet></router-outlet>
</div>
```

Add contact component
```shell
ng generate component contact
```
Change your routing configuration like this

```js
const routes: Routes = [
  { path: '', redirectTo: '/home', pathMatch: 'full' },
  { path: 'home', component: HomeComponent, canActivate: [AuthGuard] },
  { path: 'unauthorized', component: UnauthorizedComponent },
  { path: 'contact', component: ContactComponent, canActivate: [AuthGuard] }
];
```

## 11. Add Progress Bar for navigatin

Add following code your `app.component.ts` 

```js
//app.component.ts
//...
import { Router, Event as RouterEvent, NavigationStart, NavigationCancel, NavigationEnd, NavigationError } from '@angular/router';
//...
export class AppComponent{

  loading = true;

  constructor(
    router: Router
  ) {
    router.events.subscribe(event => {
      if (event instanceof NavigationStart) {
        this.loading = true;
      } else {
        this.loading = false;
      }
    });
  }
}
//....

```

Then add following code to `app.component.html`

```html
// app.component.html
<div *ngIf="loading">  
  <mat-progress-bar mode="indeterminate"></mat-progress-bar>
</div>
```
If you want to see animation, you can add `debugger;` like this

```js
// app.component.ts
router.events.subscribe(event => {
      if (event instanceof NavigationStart) {
        debugger;
        this.loading = true;
      } else {
        this.loading = false;
      }
    });
```


## 12. Add Dialog Component

We will user `MatDialogModule` in `contact` component
Add follogin lines to `contact.component.html`

```html
<button mat-raised-button (click)="openDialog()">Pick one</button>
<p>
 You chose: <i>&123;&123;animal&125;&125;</i>
</p>
```

Change  `contact.component.ts` like this

```js
import { Component, OnInit, Inject } from '@angular/core';
import { MatDialog, MatDialogRef, MAT_DIALOG_DATA } from '@angular/material';

@Component({
  selector: 'app-contact',
  templateUrl: './contact.component.html'
})
export class ContactComponent implements OnInit {

  animal: string;

  constructor(public dialog: MatDialog) { }

  ngOnInit() {
  }

  openDialog(): void {
    const dialogRef = this.dialog.open(ExampleDialogComponent, {
      width: '250px',
      data: { animal: this.animal }
    });

    dialogRef.afterClosed().subscribe(result => {
      console.log('The dialog was closed');
      this.animal = result;
    });
  }
}

@Component({
selector: 'app-example-dialog-component',
  template: `
  <h1 mat-dialog-title>Hi</h1>
  <div mat-dialog-content>
    <p>What's your favorite animal?</p>
    <mat-form-field>
      <input matInput [(ngModel)]="data.animal">
    </mat-form-field>
  </div>
  <div mat-dialog-actions>
    <button mat-button (click)="onNoClick()">No Thanks</button>
    <button mat-button [mat-dialog-close]="data.animal" cdkFocusInitial>Ok</button>
  </div>
  `
})
export class ExampleDialogComponent {

  constructor(
    public dialogRef: MatDialogRef<ExampleDialogComponent>,
    @Inject(MAT_DIALOG_DATA) public data: any) { }

  onNoClick(): void {
    this.dialogRef.close();
  }

}

```
Add following lines to `app.module.ts`

```js
//...
import { ContactComponent, ExampleDialogComponent } from './contact/contact.component';
//...

@NgModule({
  imports: [
  //...
  ],
  declarations: [
    //..
    ExampleDialogComponent
    //..
  ],
   entryComponents: [ExampleDialogComponent]
}

```

## 13. Add Toast Component

In this example, I'll use `ngx-toastr` package, which has the most on github

```shell
npm install ngx-toastr --save
```

@angular/animations package is a required dependency for the default toast

```shell
npm install @angular/animations --save
```

copy `toastcss` to your project [https://github.com/scttcper/ngx-toastr/blob/master/src/lib/toastr.css](https://github.com/scttcper/ngx-toastr/blob/master/src/lib/toastr.css)

and add the following line to `angular.json`

```js
 "architect": {
        "build": {
            //....
            "styles": [
              "src/styles.css",
              "src/assets/custom.css",
              "src/assets/toastr.css"
            ]
          }
        }
 }
```
Then add ToastrModule to app NgModule

```js
import { CommonModule } from '@angular/common';
import { BrowserAnimationsModule } from '@angular/platform-browser/animations';

import { ToastrModule } from 'ngx-toastr';

@NgModule({
  imports: [
    CommonModule,
    BrowserAnimationsModule, // required animations module
   ToastrModule.forRoot({ closeButton: true, timeOut: 2000 }) // ToastrModule added
  ],
  bootstrap: [App],
  declarations: [App],
})
class MainModule {}
```

Then use in `contact` component

```js
import { ToastrService } from 'ngx-toastr';

@Component({...})
export class ContactComponent {
  constructor(private toastr: ToastrService) {}

  showSuccess() {
   setTimeout(() => this.toastr.success('Hello world!', 'sdfasdfasd'));
  }
}
```


## 14. Create Common Back-End and Front-End Classes

Following classes used in Back-End services
Create `code/dto.ts` file and paste following code

```js
// dto.ts
export class ServiceResponse<T> {

    public IsSuccess: boolean;

    public ResultType: ResultType;

    public Message: string;

    public TotalCount: number;

    public Data: T;
}

export enum ResultType {

    Information = 1,

    Validation = 2,

    Success = 3,

    Warning = 4,

    Error = 5,
}

export class BaseDto {

    public Id: number;

    public CreateDate: Date;

    public CreatedBy: number;

    public UpdateDate: Date;

    public UpdatedBy: number;

    public IsActive: boolean;
}

export class PagingDto {

    constructor() {
        this.pageNumber = 1;
        this.pageSize = 10; // TODO: Get from config.service
        this.orderBy = 'Id';
        this.order = 'desc';
        this.count = 0;
    }


    public pageNumber: number;

    public pageSize: number;

    public orderBy: string;

    public order: string;

    public count: number;
}

```

## 15. Create CRUD operation Component

We will create one service for CRUD operations then we will create Angular Component 

**Create crud.service.ts**

```shell
ng generate service services/crud
```

Then paste following code

```js
import { Injectable } from '@angular/core';
import { HttpClient, HttpHeaders } from '@angular/common/http';
import { Observable, of } from 'rxjs';
import { catchError, map, tap } from 'rxjs/operators';
import { ServiceResponse, PagingDto, BaseDto, ResultType } from '../code/dto';

const httpOptions = {
  headers: new HttpHeaders({ 'Content-Type': 'application/json' })
};

@Injectable({
  providedIn: 'root'
})
export class CrudService {

  constructor(private http: HttpClient) { }

  //#region BaseMethods

  // Create
  post(dto: BaseDto, apiPath: string): Observable<ServiceResponse<number>> {
    return this.http.post<ServiceResponse<number>>(apiPath, dto, httpOptions).pipe(
      tap((id: ServiceResponse<number>) => this.log(`post dto w/ id=${id}`)),
      catchError(this.handleError<ServiceResponse<number>>('postModel'))
    );
  }

  // Read
  get(id: number, apiPath: string): Observable<ServiceResponse<BaseDto>> {
    return this.http.get<ServiceResponse<BaseDto>>(`${apiPath}/${id}`).pipe(
      tap(_ => this.log(`fetched dto id=${id}`)),
      catchError(this.handleError<ServiceResponse<BaseDto>>(`getModel id=${id}`))
    );
  }

  // Update
  put(dto: BaseDto, apiPath: string): Observable<BaseDto> {
    return this.http.put(`${apiPath}/${dto.Id}`, dto, httpOptions).pipe(
      tap(_ => this.log(`updated dto id=${dto.Id}`)),
      catchError(this.handleError<any>('putModel'))
    );
  }

  // Delete
  delete(dto: BaseDto | number, apiPath: string): Observable<BaseDto> {
    const id = typeof dto === 'number' ? dto : dto.Id;
    const url = `${apiPath}/${id}`;
    return this.http.delete<BaseDto>(url, httpOptions).pipe(
      tap(_ => this.log(`deleted dto id=${id}`)),
      catchError(this.handleError<any>('deleteModel'))
    );
  }

  // List
  list(searchDto: BaseDto, pagingDto: PagingDto, apiPath: string): Observable<ServiceResponse<BaseDto[]>> {

    const dictionary = {};
    dictionary['searchDto'] = searchDto;
    dictionary['pagingDto'] = pagingDto;

    return this.http.post<ServiceResponse<BaseDto[]>>(apiPath, dictionary, httpOptions).pipe(
      tap((serviceResponse: ServiceResponse<BaseDto[]>) => this.log(`fetched dtos:` + serviceResponse.Data.length)),
      catchError(this.handleError<ServiceResponse<BaseDto[]>>(`getModels`)));
  }

  //#endregion BaseMethods

  /**
   * Handle Http operation that failed.
   * Let the app continue.
   * @param operation - name of the operation that failed
   * @param result - optional value to return as the observable result
   */
  private handleError<T>(operation = 'operation', result?: T) {
    return (error: any): Observable<T> => {

      // TODO: send the error to remote logging infrastructure
      console.error(error); // log to console instead

      // TODO: better job of transforming error for user consumption
      this.log(`${operation} failed: ${error.message}`);

      // Let the app keep running by returning an empty result.
      return of(result as T);
    };
  }

  /** Log a HeroService message with the MessageService */
  private log(message: string) {
    // this.messageService.add('HeroService: ' + message);
    console.log(message);
  }
}

```

Then create component

```shell
ng generate component user
```

Add routing config
```js
{ path: 'user', component: UserComponent, canActivate: [AuthGuard] }
```

Then insert following code

```js
import { Component, OnInit, Input } from '@angular/core';
import { CrudService } from '../services/crud.service';
import { PagingDto, ServiceResponse, BaseDto, ResultType } from '../code/dto';
import { ActivatedRoute } from '@angular/router';
import { Location, getLocaleDateTimeFormat } from '@angular/common';

@Component({
  selector: 'app-user',
  templateUrl: './user.component.html'
})
export class UserComponent implements OnInit {

  private url = 'http://localhost:5001/api/example'; // config servis ten gelecek.

  dtoList: any = [];
  entryDto: any = {};
  serarchDto: BaseDto = new BaseDto();
  pagingDto: PagingDto = new PagingDto();

  constructor(
    private crudService: CrudService,
    private route: ActivatedRoute,
    private location: Location
  ) {
    this.list();
  }

  ngOnInit() {

  }

  //#region CRUD Operations

  postOrPut(): void {
    if (!this.isValid(this.entryDto)) { return; }
    if (this.entryDto.Id == null) {
      this.crudService.post(this.entryDto, `${this.url}/postuser`).subscribe(serviceResponse => {
        this.entryDto.Id = serviceResponse.Data;
        this.dtoList.push(this.entryDto);
        this.resetEntry();
      });
    } else {
      this.crudService.put(this.entryDto, `${this.url}/putuser`).subscribe(serviceResponse => {
        const i = this.dtoList.findIndex((obj => obj.Id === this.entryDto.Id));
        this.dtoList[i] = this.entryDto;
        this.resetEntry();
      });
    }
  }

  get(dto: BaseDto): void {
    this.crudService.get(dto.Id, `${this.url}/getuser`).subscribe(serviceResponse => {
      this.entryDto = Object.assign({}, serviceResponse.Data);
    });
  }

  delete(dto: BaseDto): void {
    this.crudService.delete(dto.Id, `${this.url}/deleteuser`).subscribe(serviceResponse => {
      this.dtoList = this.dtoList.filter(h => h !== dto);
    });
  }

  list(): void {
    this.crudService.list(this.serarchDto, this.pagingDto, `${this.url}/listuser`).subscribe(
      serviceResponse => {
        this.dtoList = serviceResponse.Data;
      }
    );
  }

  // #endregion CRUD

  isValid(obj) {
    if (obj.Name == null) {
      alert('Lutfen zorunlu alanlari doldurunuz!');
      return false;
    } else {
      return true;
    }
  }

  resetEntry() {
    this.entryDto = new BaseDto();
    this.entryDto.UpdatedBy = 0;
    this.entryDto.UpdateDate = new Date();
  }

  goBack(): void {
    this.location.back();
  }

}

```

Then insert following code to `user.component.html`

```html
<h2>Users</h2>

<!-- Entry -->
<div class="entryDto w-75">
  <form (ngSubmit)="postOrPut()">
    <!-- form-group seperator -->
    <div class="form-group row">
      <label for="Name" class="col-2 col-form-label-sm">Name</label>
      <div class="col-10">
        <input class="form-control form-control-sm" type="text" [(ngModel)]="entryDto.Name" name="Name" id="Name"
          placeholder="Name">
      </div>
    </div>
      <!-- form-group seperator -->
      <div class="form-group row">
        <label for="LastName" class="col-2 col-form-label-sm">Last Name</label>
        <div class="col-10">
          <input class="form-control form-control-sm" type="text" [(ngModel)]="entryDto.LastName" name="LastName" id="LastName"
            placeholder="LastName">
        </div>
      </div> 
    <!-- form-group seperator -->
    <div class="text-right">
      <button type="submit" class="btn btn-success btn-sm" ngbTooltip="Save"><i class="material-icons" >save</i></button>&nbsp;
      <button type="button" class="btn btn-primary btn-sm" ngbTooltip="Cancel" (click)="resetEntry()"><i class="material-icons">refresh</i></button>
    </div>
  </form>
</div>
<!-- Entry -->
<br>


<!-- List -->
<div class=”container”>
  <table class="table table-bordered table-sm m-0">
    <thead style="background-color:#b4cff1">
      <tr>
        <th>#</th>
        <th>Name</th>
        <th>Last Name</th>
        <th></th>
      </tr>
    </thead>
    <tbody>
      <tr *ngFor="let dto of dtoList; let i = index">
        <th scope="row">>&123;&123; i ++ &125;&125;</th>
        <td>>&123;&123;dto.Name&125;&125;</td>     
        <td>&123;&123; dto.LastName &125;&125;</td>     
        <td>
          <button type="button" class="btn btn-sm btn-outline-primary" (click)="get(dto)" ngbTooltip="Edit row"><i class="material-icons">border_color</i></button>&nbsp;
          <button type="button" class="btn btn-sm btn-outline-danger" (click)="delete(dto)" ngbTooltip="Delete row"><i class="material-icons">cancel</i></button>
        </td>
      </tr>
    </tbody>
  </table>
</div>
<!-- List -->
```


## 16. Add Interceptor for API Response Messages

Create interceptor `api.interceptor.ts` in services folder

```js
import { Injectable, Injector } from '@angular/core';
import { HttpInterceptor, HttpRequest, HttpHandler, HttpEvent, HttpResponse } from '@angular/common/http';
import { Observable } from 'rxjs';
import { catchError, tap } from 'rxjs/operators';
import { SessionStorageService } from 'ngx-webstorage';
import { ConfigService } from './config.service';
import { ToastrService } from 'ngx-toastr';
import { ServiceResponse } from '../code/dto';
import { TranslateService } from '@ngx-translate/core';


@Injectable()
export class ApiInterceptor implements HttpInterceptor {

    private sessionStorage: SessionStorageService;
    private configService: ConfigService;
    private toastr: ToastrService;
    private translate: TranslateService;

    constructor(
        private injector: Injector
    ) {
    }

    intercept(request: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {

        const requestTimestamp = new Date().getTime();
        this.sessionStorage = this.injector.get(SessionStorageService);
        this.configService = this.injector.get(ConfigService);
        this.toastr = this.injector.get(ToastrService);
        this.translate = this.injector.get(TranslateService);
        let clonedRequest = request;

        const userLanguage = sessionStorage.getItem('ng2-webstorage|current_language');
        if (userLanguage != null) {
            clonedRequest = request.clone({ setHeaders: { 'Accept-Language': userLanguage.substring(1, 3) } });
        } else {
            if (this.configService.config != null) {
                const defLang = this.configService.config.DefaultLanguage.substring(1, 3);
                clonedRequest = request.clone({ setHeaders: { 'Accept-Language': defLang } });
            }
        }

        return next.handle(clonedRequest).pipe(
            tap(response => {

                if (response instanceof HttpResponse) {
                    const responseTimestamp = new Date().getTime();
                    const elapsed_ms = responseTimestamp - requestTimestamp;
                    console.log(response.url + ' --> ' + elapsed_ms + ' ms');

                    this.handleResponseMessage(response);
                    console.log(response);
                }
            }),
            catchError(err => {
                console.log('Caught error', err);
                return Observable.throw(err);
            })
        );
    }

    private handleResponseMessage(response) {
        if (response != null && response.body != null) {
            const serviceResponse: ServiceResponse<any> = response.body;

            if (response.status !== 200) {

                this.translate.get('MSG_ERROR').subscribe((res: string) => {
                    this.toastr.error(res, 'Error');
                    console.log(response.statusText);
                });
            }

            if (serviceResponse != null &&
                serviceResponse.IsSuccess != null &&
                serviceResponse.Message != null &&
                serviceResponse.Message.length > 0) {

                if (!serviceResponse.IsSuccess) {
                    this.translate.get(serviceResponse.Message).subscribe((res: string) => {
                        setTimeout(() => this.toastr.error(res, 'Error'));
                        console.log(serviceResponse.Message);
                    });
                } else {

                    switch (serviceResponse.ResultType) {
                        case 1:
                            this.translate.get(serviceResponse.Message).subscribe((res: string) => {
                                this.toastr.info(res);
                            });
                            break;
                        case 2:
                            this.translate.get(serviceResponse.Message).subscribe((res: string) => {
                                this.toastr.warning(res);
                            });
                            break;
                        case 3:
                            this.translate.get(serviceResponse.Message).subscribe((res: string) => {
                                this.toastr.success(res);
                            });
                            break;
                        case 4:
                            this.translate.get(serviceResponse.Message).subscribe((res: string) => {
                                this.toastr.warning(res);
                            });
                            break;
                        case 5:
                            this.translate.get(serviceResponse.Message).subscribe((res: string) => {
                                this.toastr.error(res);
                            });
                            break;
                        default:
                            break;
                    }
                    console.log(serviceResponse.Message);
                }
            }
        }
    }

}


```

Add following lines to `app.module.ts`

```js
    {
      provide: HTTP_INTERCEPTORS,
      useClass: ApiInterceptor,
      multi: true
    },
```

We will run correctly above code after `TranslateService` 

## 17. Create TranslaterService

We will use `ngx-translate/core` for translation
First, you need to install the npm module:

```shell
npm install @ngx-translate/core --save
npm install @ngx-translate/http-loader --save
```

Modify your `app.module.ts` like this

```js
import {NgModule} from '@angular/core';
import {BrowserModule} from '@angular/platform-browser';
import {HttpClientModule, HttpClient} from '@angular/common/http';
import {TranslateModule, TranslateLoader} from '@ngx-translate/core';
import {TranslateHttpLoader} from '@ngx-translate/http-loader';
import {AppComponent} from './app';

export function loadTranslate(http: HttpClient) {
  return new TranslateHttpLoader(http, 'http://localhost:5001/api/js/json/languages/', '.js');
}

@NgModule({
    imports: [
        BrowserModule,
        HttpClientModule,
        TranslateModule.forRoot({
            loader: {
                provide: TranslateLoader,
                useFactory: loadTranslate,
                deps: [HttpClient]
            }
        })
    ],
    bootstrap: [AppComponent]
})
export class AppModule {

  constructor(
    private oidcSecurityService: OidcSecurityService,
    private configService: ConfigService,
    private translate: TranslateService
  ) {
    console.log('APP STARTING');

    this.configService.onConfigurationLoaded.subscribe(() => {
      console.log('Configuration loaded.');
      this.configService.setupSSO(this.oidcSecurityService);

      this.translate.setDefaultLang(this.configService.config.DefaultLanguage);
      this.translate.use(this.configService.config.DefaultLanguage);
    });
  }
}
```



Then test it in `home.component.html`

```html
// home.component.html
<p>
  &123;&123; 'YOUR_TRANSLATION_KEY' | translate &125;&125;
</p>
```

```js
// home.component.ts
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-home',
  templateUrl: './home.component.html'
})
export class HomeComponent implements OnInit {

  constructor() {
  }

  ngOnInit() {
  }

}
```

Then Change your `api.interceptor.ts` for server messages

```js
import { Injectable, Injector } from '@angular/core';
import { HttpInterceptor, HttpRequest, HttpHandler, HttpEvent, HttpResponse } from '@angular/common/http';
import { Observable } from 'rxjs';
import { catchError, tap } from 'rxjs/operators';
import { SessionStorageService } from 'ngx-webstorage';
import { ConfigService } from './config.service';
import { ToastrService } from 'ngx-toastr';
import { ServiceResponse } from '../code/dto';
import { TranslateService } from '@ngx-translate/core';


@Injectable()
export class ApiInterceptor implements HttpInterceptor {

    private sessionStorage: SessionStorageService;
    private configService: ConfigService;
    private toastr: ToastrService;
    private translate: TranslateService;

    constructor(
        private injector: Injector
    ) {
    }

    intercept(request: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {

        const requestTimestamp = new Date().getTime();
        this.sessionStorage = this.injector.get(SessionStorageService);
        this.configService = this.injector.get(ConfigService);
        this.toastr = this.injector.get(ToastrService);
        this.translate = this.injector.get(TranslateService);
        let clonedRequest = request;

        const userLanguage = sessionStorage.getItem('ng2-webstorage|current_language');
        if (userLanguage != null) {
            clonedRequest = request.clone({ setHeaders: { 'Accept-Language': userLanguage.substring(1, 3) } });
        } else {
            if (this.configService.config != null) {
                const defLang = this.configService.config.DefaultLanguage.substring(1, 3);
                clonedRequest = request.clone({ setHeaders: { 'Accept-Language': defLang } });
            }
        }

        return next.handle(clonedRequest).pipe(
            tap(response => {

                if (response instanceof HttpResponse) {
                    const responseTimestamp = new Date().getTime();
                    const elapsed_ms = responseTimestamp - requestTimestamp;
                    console.log(response.url + ' --> ' + elapsed_ms + ' ms');

                    this.handleResponseMessage(response);
                    console.log(response);
                }
            }),
            catchError(err => {
                console.log('Caught error', err);
                return Observable.throw(err);
            })
        );
    }

    private handleResponseMessage(response) {
        if (response != null && response.body != null) {
            const serviceResponse: ServiceResponse<any> = response.body;

            if (response.status !== 200) {

                this.translate.get('MSG_ERROR').subscribe((res: string) => {
                    this.toastr.error(res, 'Error');
                    console.log(response.statusText);
                });
            }

            if (serviceResponse != null &&
                serviceResponse.IsSuccess != null &&
                serviceResponse.Message != null &&
                serviceResponse.Message.length > 0) {

                if (!serviceResponse.IsSuccess) {
                    this.translate.get(serviceResponse.Message).subscribe((res: string) => {
                        setTimeout(() => this.toastr.error(res, 'Error'));
                        console.log(serviceResponse.Message);
                    });
                } else {

                    switch (serviceResponse.ResultType) {
                        case 1:
                            this.translate.get(serviceResponse.Message).subscribe((res: string) => {
                                this.toastr.info(res);
                            });
                            break;
                        case 2:
                            this.translate.get(serviceResponse.Message).subscribe((res: string) => {
                                this.toastr.warning(res);
                            });
                            break;
                        case 3:
                            this.translate.get(serviceResponse.Message).subscribe((res: string) => {
                                this.toastr.success(res);
                            });
                            break;
                        case 4:
                            this.translate.get(serviceResponse.Message).subscribe((res: string) => {
                                this.toastr.warning(res);
                            });
                            break;
                        case 5:
                            this.translate.get(serviceResponse.Message).subscribe((res: string) => {
                                this.toastr.error(res);
                            });
                            break;
                        default:
                            break;
                    }
                    console.log(serviceResponse.Message);
                }
            }
        }
    }

}


```

## 18. Add Change Language Options

If you added `ngx-translate/core` module your project, you can add `app.component.html`
following lines

```html
    <button mat-button [matMenuTriggerFor]="menu">Languages</button>
  <mat-menu #menu="matMenu">
    <button mat-menu-item (click)="langChange('en-US')">English</button>
    <button mat-menu-item (click)="langChange('tr-TR')">Turkce</button>
  </mat-menu>
```

Then add `app.component.ts` the following method

```js
langChange(lang: string) {
  this.translateService.use(lang);
}
```

Then add current user language to sessionStorage
Change `app.module.ts` file
we subscribe `onLangChange` event then we store 'current_language'
`api.interceptor` will use this data for every Request  

```js
export class AppModule {

  constructor(
    private oidcSecurityService: OidcSecurityService,
    private configService: ConfigService,
    private translate: TranslateService,
    private sessionStorage: SessionStorageService
  ) {
    console.log('APP STARTING');

    this.configService.onConfigurationLoaded.subscribe(() => {
      console.log('Configuration loaded.');
      this.configService.setupSSO(this.oidcSecurityService);

      this.translate.setDefaultLang(this.configService.config.DefaultLanguage);
      this.translate.use(this.configService.config.DefaultLanguage);

      this.translate.onLangChange.subscribe((event: LangChangeEvent) => {
        this.sessionStorage.store('current_language', event.lang);
      });

    });
  }
}

```

```js
//api.interceptor.ts
private addLanguageHeader(request: HttpRequest<any>) {

        const userLanguage = sessionStorage.getItem('ng2-webstorage|current_language');
        if (userLanguage != null) {
            request.headers.append('Accept-Language', userLanguage);
        } else {
            if (this.configService.config != null) {
                request.headers.append('Accept-Language', this.configService.config.DefaultLanguage);
            }
        }
    }
```



## 18. Add Delete Confirmation

Create `DeleteConfirmation` component

`ng generate component deleteConfirmation`

Then Paste below html to `delete-confirmation.component.html`

```html
<h1 mat-dialog-title>&123;&123;'LBL_WARNING' | translate&125;&125;</h1>
<div mat-dialog-content>
  <p>&123;&123; 'ARE_YOU_SURE' | translate &125;&125;</p>
</div>
<div mat-dialog-actions>
  <button mat-button (click)="onNoClick(data.dto)" cdkFocusInitial>&123;&123; 'NO' | translate&125;&125;</button>
  <button mat-button (click)="onYesClick(data.dto)">&123;&123; 'YES' | translate &125;&125;</button>
</div>

```

Then Paste below script to `delete-confirmation.component.ts`

```js
import { Component, OnInit, Inject } from '@angular/core';
import { MatDialog, MatDialogRef, MAT_DIALOG_DATA } from '@angular/material';

@Component({
  selector: 'app-delete-confirmation',
  templateUrl: './delete-confirmation.component.html'
})
export class DeleteConfirmationComponent {

  constructor(
    public dialogRef: MatDialogRef<DeleteConfirmationComponent>,
    @Inject(MAT_DIALOG_DATA) public data: any) { }

  onNoClick(dto: any): void {    
    this.data.confirmation = 'NO';
    this.dialogRef.close(this.data);
  }

  onYesClick(dto: any): void {    
    this.data.confirmation = 'YES';
    this.dialogRef.close(this.data);
  }

}

```

Then modify your `app.module.ts` like this

```js
@NgModule({
  imports: [
    //...
  ],
  declarations: [
    //..
    DeleteConfirmationComponent

  ],
  providers: [
    //..
  ],
  //..
  entryComponents: [DeleteConfirmationComponent]
})
```

Then modify your `user.component.html` 

```html
<div class="animate-bottom">
<h2>Users</h2>

<!-- Entry -->
<div class="entryDto w-75">
  <form (ngSubmit)="postOrPut()">
    <!-- form-group separator -->
    <div class="form-group row">
      <label for="Name" class="col-2 col-form-label-sm">&123;&123;'Name' | translate&125;&125;</label>
      <div class="col-10">
        <input class="form-control form-control-sm" type="text" [(ngModel)]="entryDto.Name" name="Name" id="Name"
          placeholder="Name">
      </div>
    </div>
      <!-- form-group separator -->
      <div class="form-group row">
        <label for="LastName" class="col-2 col-form-label-sm">&123;&123;'Last Name' | translate&125;&125;</label>
        <div class="col-10">
          <input class="form-control form-control-sm" type="text" [(ngModel)]="entryDto.LastName" name="LastName" id="LastName"
            placeholder="LastName">
        </div>
      </div> 
    <!-- form-group separator -->
    <div class="text-right">
      <button type="submit" class="btn btn-success btn-sm" ngbTooltip="Save"><i class="material-icons" >save</i></button>&nbsp;
      <button type="button" class="btn btn-primary btn-sm" ngbTooltip="Cancel" (click)="resetEntry()"><i class="material-icons">refresh</i></button>
    </div>
  </form>
</div>
<!-- Entry -->
<br>


<!-- List -->
<div class=”container”>
  <table class="table table-bordered table-sm m-0">
    <thead style="background-color:#b4cff1">
      <tr>
        <th>#</th>
        <th>&123;&123;'Name' | translate&125;&125;</th>
        <th>&123;&123;'Last Name' | translate&125;&125;</th>
        <th></th>
      </tr>
    </thead>
    <tbody>
      <tr *ngFor="let dto of dtoList; let i = index">
        <th scope="row">&123;&123; i + 1 &125;&125;</th>
        <td>&123;&123; dto.Name &125;&125;</td>     
        <td>&123;&123; dto.LastName &125;&125;</td>     
        <td>
          <button type="button" class="btn btn-sm btn-outline-primary" (click)="get(dto)" ngbTooltip="Edit row"><i class="material-icons">border_color</i></button>&nbsp;
          <button type="button" class="btn btn-sm btn-outline-danger" (click)="openDialog(dto)" ngbTooltip="Delete row"><i class="material-icons">cancel</i></button>          
        </td>
      </tr>
    </tbody>
  </table>
</div>
<!-- List -->
</div>
```

Then add below method to `user.component.ts` 

```js
openDialog(dto: any): void {
    const dialogRef = this.dialog.open(DeleteConfirmationComponent, {
      width: '250px',
      data: { dto: dto }
    });

    dialogRef.afterClosed().subscribe(result => {
      if (result.confirmation === 'YES') {
        this.delete(result.dto);
      }
      console.log('The dialog was closed');
    });
  }
```


## 19. Improve Entry and DataGrid 

You can add two type data grid to your project

1. Material `Data Table` [https://material.angular.io/components/table/overview](https://material.angular.io/components/table/overview)
  and Meterial `Paginator` [https://material.angular.io/components/paginator/overview](https://material.angular.io/components/paginator/overview)

2. ag-Grid [https://www.ag-grid.com/best-angular-2-data-grid/](https://www.ag-grid.com/best-angular-2-data-grid/) 

## 20. Add Pagination

[https://material.angular.io/components/paginator/overview](https://material.angular.io/components/paginator/overview)

Add the following line to `app.module.ts` 
```js
import {MatPaginatorModule} from '@angular/material/paginator';
```

Then change your `user.component.ts`

```js
import {PageEvent} from '@angular/material';

list(): void {
  this.crudService.list(this.searchDto, this.pagingDto, `${this.url}/listuser`).subscribe(
    serviceResponse => {
      this.dtoList = serviceResponse.Data;
      this.pagingDto.count = serviceResponse.TotalCount;
    }
  );
}

changePage(pageEvent: PageEvent) : void {
  this.pagingDto.count = pageEvent.length;
  this.pagingDto.pageSize = pageEvent.pageSize;
  this.pagingDto.pageNumber = pageEvent.pageIndex + 1;
  this.list();
}


```

Then change your `user.component.html`

```html
  <mat-paginator [length]="pagingDto.count"
    [pageSize]="pagingDto.pageSize"
    [pageSizeOptions]="[10, 15, 20, 50]"
    (page)="changePage($event)">
  </mat-paginator>
```

## 21. Add Sort Functionality in Current Table Page

Change `user.component.ts` 

```js
import { Sort } from '@angular/material';

  sortData(sort: Sort): void {
    if (!sort.active || sort.direction === '') {
      return;
    }
    // local paging
    this.dtoList = this.dtoList.sort((a, b) => {
      const isAsc = sort.direction === 'asc';
      switch (sort.active) {
        case 'Name': return this.compare(a.Name, b.Name, isAsc);
        case 'LastName': return this.compare(a.LastName, b.LastName, isAsc);
        case 'BirthDate': return this.compare(a.BirthDate, b.BirthDate, isAsc);
        default: return 0;
      }
    });
  }

  compare(a, b, isAsc) {
    return (a < b ? -1 : 1) * (isAsc ? 1 : -1);
  }
```

Then change `user.component.html` data table, like this

```html
<!-- List -->
  <div class=”container”>
    <table class="table table-bordered table-sm m-0" matSort (matSortChange)="sortData($event)">
      <thead style="background-color:#b4cff1">
        <tr>
          <th>#</th>
          <th mat-sort-header="Name">&123;&123;'Name' | translate&125;&125;</th>
          <th mat-sort-header="LastName">&123;&123;'Last Name' | translate&125;&125;</th>
          <th mat-sort-header="BirthDate">&123;&123;'Birth Date' | translate&125;&125;</th>
          <th>-</th>
        </tr>
      </thead>
      <tbody>
        <tr *ngFor="let dto of dtoList; let i = index">
          <th scope="row">&123;&123; i + 1 &125;&125;</th>
          <td>&123;&123; dto.Name &125;&125;</td>
          <td>&123;&123; dto.LastName &125;&125;</td>
          <td>&123;&123; dto.BirthDate | date: 'medium' &125;&125;</td>
          <td>
            <button type="button" matTooltip="&123;&123;'Edit Row' | translate&125;&125;" mat-mini-fab color="primary" (click)="get(dto)">
              <i class="material-icons">border_color</i>
            </button>
            &nbsp;
            <button type="button" matTooltip="&123;&123;'Delete Row' | translate&125;&125;" mat-mini-fab (click)="openDialog(dto)">
              <i class="material-icons">cancel</i>
            </button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
  <!-- List -->
```

## 21. Add Sort Functionality in Database

If  you want to sort data in database query
you can change pagingDto order direction and recall list() method.
```js
  sortData(sort: Sort): void {
    if (!sort.active || sort.direction === '') {
      return;
    }
    // Database paging
    this.pagingDto.order  = sort.direction;
    this.list();
  }
```



## 22. Add Tooltip for icons

```html
<button mat-raised-button
        matTooltip="Info about the action"
        aria-label="Button that displays a tooltip when focused or hovered over">
  Action
</button>
```

Then change `user.component.html` like this

```html
<div class="animate-bottom w-75" style="padding-left:30px;">
  <h2>Users</h2>

  <!-- Entry -->
  <form (ngSubmit)="postOrPut()">
    <!-- form-group separator -->
    <div style="display:flex; flex-direction: column;">
      <mat-form-field>
        <input matInput type="text" placeholder="&123;&123;'Name' | translate&125;&125;" [(ngModel)]="entryDto.Name" name="Name" id="Name" />
        <button mat-button *ngIf="entryDto.Name" matSuffix mat-icon-button aria-label="Clear" (click)="entryDto.Name=''">
          <mat-icon>close</mat-icon>
        </button>
      </mat-form-field>
    </div>
    <!-- form-group separator -->
    <div style="display:flex; flex-direction: column;">
      <mat-form-field>
        <input matInput type="text" placeholder="&123;&123;'Last Name' | translate&125;&125;" [(ngModel)]="entryDto.LastName" name="LastName" id="LastName"
        />
        <button mat-button *ngIf="entryDto.LastName" matSuffix mat-icon-button aria-label="Clear" (click)="entryDto.LastName=''">
          <mat-icon>close</mat-icon>
        </button>
      </mat-form-field>
    </div>
    <!-- form-group separator -->
    <div style="display:flex; flex-direction: column;">
      <mat-form-field>
        <input matInput [matDatepicker]="picker" placeholder="&123;&123;'Choose' | translate&125;&125;" [(ngModel)]="entryDto.BirthDate" name="BirthDate" id="BirthDate">
        <mat-datepicker-toggle matSuffix [for]="picker"></mat-datepicker-toggle>
        <mat-datepicker #picker></mat-datepicker>
      </mat-form-field>
    </div>
    <!-- form-group separator -->
    <div style="text-align: right;">
      <button type="submit" matTooltip="&123;&123;'Save' | translate&125;&125;" mat-raised-button color="primary">
        <i class="material-icons">save</i>
      </button>&nbsp;
      <button type="button" matTooltip="&123;&123;'Clear' | translate&125;&125;" mat-raised-button color="accent" (click)="resetEntry()">
        <i class="material-icons">refresh</i>
      </button>
    </div>
  </form>
  <!-- Entry -->
  <br>


  <!-- List -->
  <div class=”container”>
    <table class="table table-bordered table-sm m-0">
      <thead style="background-color:#b4cff1">
        <tr>
          <th>#</th>
          <th>&123;&123;'Name' | translate&125;&125;</th>
          <th>&123;&123;'Last Name' | translate&125;&125;</th>
          <th>&123;&123;'Birth Date' | translate&125;&125;</th>
          <th>-</th>
        </tr>
      </thead>
      <tbody>
        <tr *ngFor="let dto of dtoList; let i = index">
          <th scope="row">&123;&123; i + 1 &125;&125;</th>
          <td>&123;&123; dto.Name &125;&125;</td>
          <td>&123;&123; dto.LastName &125;&125;</td>
          <td>&123;&123; dto.BirthDate | date: 'medium' &125;&125;</td>
          <td>
            <button type="button" matTooltip="&123;&123;'Edit Row' | translate&125;&125;" mat-mini-fab color="primary" (click)="get(dto)">
              <i class="material-icons">border_color</i>
            </button>
            &nbsp;
            <button type="button" matTooltip="&123;&123;'Delete Row' | translate&125;&125;" mat-mini-fab (click)="openDialog(dto)">
              <i class="material-icons">cancel</i>
            </button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
  <!-- List -->
  <mat-paginator [length]="pagingDto.count"
    [pageSize]="pagingDto.pageSize"
    [pageSizeOptions]="[10, 15, 20, 50]"
    (page)="changePage($event)">
  </mat-paginator>
</div>


```

for more detail follow the link [https://material.angular.io/components/tooltip/overview](https://material.angular.io/components/tooltip/overview)


![/assets/img/ea-interface.PNG](/assets/img/ea-interface.PNG)

Source codes: 
1. Enterprise-Angular-Project [https://github.com/atillatan/Enterprise-Angular-Project](https://github.com/atillatan/Enterprise-Angular-Project)

2. SSO [https://github.com/atillatan/sso-with-identityserver4](https://github.com/atillatan/sso-with-identityserver4)

3. Enterprise WebApi Project [Developing](Developing)