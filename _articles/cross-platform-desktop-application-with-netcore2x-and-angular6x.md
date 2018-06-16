---
layout: article
permalink:
name:
file_type:
title:  Cross Platform Desktop Application With .Net Core 2x and Angular 6x
description: >-
   Cross Platform Desktop Application With .Net Core 2x and Angular 6x
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

# Cross Platform Desktop Application With .Net Core 2x and Angular 6x

We will use 4 kind framework for our desktop application
which are;

- **NodeJs:** JavaScript runtime environment, on various platforms (Windows, Linux, Unix, Mac OS X, etc.)
- **Electron:** Electron enables you to create cross platform desktop applications with pure JavaScript by providing a runtime
- **Angular CLI:** Angular CLI is a command line interface to scaffold and build angular apps using nodejs
- **Net Core:** Open source cross platform framework, developed by Microsoft and the community

## 1. Install NodeJS

If you want to create Angular project, you must install nodejs first.
Because Angular uses nodejs development environment.

- Download nodejs from [https://nodejs.org](https://nodejs.org) and install it

After the installation, you will have npm (Node Package Manager) on your terminal/command line

## 2. Install Electron and Create NodeJs Project

```bash
npm i -D electron@latest
```

- Create NodeJs Project

```bash
mkdir electronapp
cd electronapp
npm init
// After above command, it will ask some questions
// response apropriate information for npm init questions
```

In this example it created initial `package.json` then I modified like this

```json
{
  "name": "cross-platform-desktop-app",
  "version": "1.0.0",
  "description": "Cross Platform Desktop Application with .Net Core 2 and Angular 6",
  "main": "main.js",
  "scripts": {
    "start": "electron .",
    "package-mac": "electron-packager . --overwrite --asar=true --platform=darwin --arch=x64 --icon=assets/icons/mac/icon.icns --prune=true --out=release-builds",
    "package-win": "electron-packager . --overwrite --asar=true --platform=win32 --arch=ia32 --icon=assets/icons/windows/icon.ico --prune=true --out=release-builds --version-string.CompanyName='atillatan' --version-string.FileDescription='Cross Platform Desktop App' --version-string.ProductName='Cross Platform Desktop App'",
    "package-linux": "electron-packager . --overwrite --asar=true --platform=linux --arch=x64 --icon=assets/icons/png/1024x1024.png --prune=true --out=release-builds"
},
  "repository": {
    "type": "git",
    "url": "git+https://github.com/atillatan/cross-platform-desktop-application-with-netcore2x-and-angular6x.git"
  },
  "keywords": [
    "Cross",
    "Platform",
    "Desktop",
    "Application",
    "with",
    ".Net",
    "Core",
    "2",
    "and",
    "Angular",
    "6"
  ],
  "author": "atillatan",
  "license": "MIT",
  "dependencies": {},
  "devDependencies": {
    "electron": "^2.0.2"
  },
  "bugs": {
    "url": "https://github.com/atillatan/cross-platform-desktop-application-with-netcore2x-and-angular6x/issues"
  },
  "homepage": "https://github.com/atillatan/cross-platform-desktop-application-with-netcore2x-and-angular6x#readme"
}
```

## 3. Install Angular CLI

```bash
// in root directory
npm install -g @angular/cli
```

install node packages, that is defined in `package.json`

```bash
npm install
```

Create these directories `dist` and `src`

```bash
mkdir src, dist
```

**Editor**
I will use `Visual Studio Code` for editing the project
open project with Visual Studio Code

```bash
code .
```

Create `main.js` and paste below code

```js
```

Create `index.html` and paste below code

```html
```


## 4. Create .Net Core Project

- Install .Net Core

Download latest version of .net core framework from [https://www.microsoft.com/net/download/windows](https://www.microsoft.com/net/download/windows) and install it.
After the installation you will have `dotnet` command environment in you terminal/command prompt

- Open your terminal or, windows PowerShell, then execute following commands

```bash
cd src
dotnet new webapi -n coreapi
cd coreapi
dotnet restore
dotnet build
dotnet run
```

Change `coreapi/Controllers/ValuesController.cs` like this

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Threading.Tasks;
using Microsoft.AspNetCore.Mvc;

namespace coreapi.Controllers
{
    [Route("api/[controller]")]
    public class ValuesController : Controller
    {
        // GET api/values
        [HttpGet]
        public IEnumerable<dynamic> Get()
        {
            return new List<dynamic> {
                new { Name = "Bob", FamilyName = "Smith", Age = 32, email = "test1@mydomain.com" },
                new { Name = "Alice", FamilyName = "Smith", Age = 33, email = "test2@mydomain.com" },
                new { Name = "Amy", FamilyName = "Smith", Age = 32, email = "test3@mydomain.com" },
                new { Name = "Adam", FamilyName = "Smith", Age = 32, email = "test4@mydomain.com" }
             };
        } 

        // GET api/values/5
        [HttpGet("{id}")]
        public string Get(int id)
        {
            return "value";
        }

        // POST api/values
        [HttpPost]
        public void Post([FromBody]string value)
        {
        }

        // PUT api/values/5
        [HttpPut("{id}")]
        public void Put(int id, [FromBody]string value)
        {
        }

        // DELETE api/values/5
        [HttpDelete("{id}")]
        public void Delete(int id)
        {
        }
    }
}

```

Change  `startup.cs` like this

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Threading.Tasks;
using Microsoft.AspNetCore.Builder;
using Microsoft.AspNetCore.Hosting;
using Microsoft.Extensions.Configuration;
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Logging;
using Microsoft.Extensions.Options;

namespace coreapi
{
    public class Startup
    {
        public Startup(IConfiguration configuration)
        {
            Configuration = configuration;
        }

        public IConfiguration Configuration { get; }

        // This method gets called by the runtime. Use this method to add services to the container.
        public void ConfigureServices(IServiceCollection services)
        {
            services.AddCors();
            services.AddMvc();
        }

        // This method gets called by the runtime. Use this method to configure the HTTP request pipeline.
        public void Configure(IApplicationBuilder app, IHostingEnvironment env)
        {
            if (env.IsDevelopment())
            {
                app.UseDeveloperExceptionPage();
            }
            app.UseCors(policy => policy.AllowAnyOrigin()
                                        .AllowAnyHeader()
                                        .AllowAnyMethod());
            app.UseMvc();
        }
    }
}

```

and test it [http://localhost:5000/api/values](http://localhost:5000/api/values)


## 5. Create Angular Project

- Open your terminal or windows PowerShell, then execute following commands

```bash
// go to `src` directory
cd src
npm install -g @angular/cli
ng new angularweb --skip-tests --routing
// --routing : add routing functionality to project
// --skip-test: skip test functionality
cd angularweb
ng serve --open
```

Using the --open (or just -o) option will automatically open your browser on http://localhost:4200/.

You can also read the following tutorial [https://angular.io/guide/quickstart](https://angular.io/guide/quickstart) for Angular installation.

Add  HtmlClientModule to `app.module.ts` like this

```js
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';

import { AppRoutingModule } from './app-routing.module';
import { AppComponent } from './app.component';
import { HttpClientModule } from '@angular/common/http';

@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    AppRoutingModule,
    HttpClientModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }

```

Add Materialize to `index.html` like this

```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>Angularweb</title>
  <base href="/">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <link rel="icon" type="image/x-icon" href="favicon.ico">
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/materialize/1.0.0-beta/css/materialize.min.css">
  <script src="https://cdnjs.cloudflare.com/ajax/libs/materialize/1.0.0-beta/js/materialize.min.js"></script>
</head>
<body>
  <app-root>Loading...</app-root>
</body>
</html>
```

Change `src/app/app.component.ts` like this

```js
import { Component } from '@angular/core';
import { HttpClient } from '@angular/common/http';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {

  head = 'Cross Platform Desktop Application';
  users = null;

  constructor(private http: HttpClient) {
    this.listUsers();
  }

  listUsers(): void {
    this.http.get<any>(`http://localhost:5000/api/values`).subscribe(data => {
      this.users = data;
    });
  }
}
```

Change `src/app/app.component.html` like this

```html
<nav>
  <div class="nav-wrapper">
    <a class="brand-logo center">{{head}}</a>
  </div>
</nav>

<table class="striped responsive-table"> 
  <thead>
    <tr>
      <th>Name</th>
      <th>Family Name</th>
      <th>Age</th>
      <th>Email</th>
    </tr>
  </thead>

  <tbody>
    <tr *ngFor="let user of users">
      <td>{{ user.name }}</td>
      <td>{{ user.familyName }}</td>
      <td>{{ user.age }}</td>
      <td>{{ user.email }}</td>
    </tr>
</table>

```

## 6. Integrate with Electron

