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

We will use 4 framework for our desktop application
which are;

- **Net Core:** Open source cross platform framework, developed by Microsoft and the community
- **Angular CLI:** Angular CLI is a command line interface to scaffold and build angular apps using nodejs
- **Electron:** Electron enables you to create cross platform desktop applications with pure JavaScript by providing a runtime (NodeJS)
- **NodeJs:** JavaScript runtime environment, on various platforms (Windows, Linux, Unix, Mac OS X, etc.)



## 1. Install NodeJS

If you want to create Angular project, you must install nodejs first.
Because Angular and Angular CLI uses nodejs development environment.

- Download nodejs from [https://nodejs.org](https://nodejs.org) and install it

After the installation, you will have npm (Node Package Manager) on your terminal/command line

## 2. Create Project Directories, Install Electron

```bash

// create project directory
mkdir desktopapp

// create src directory
mkdir src

// create project directories
cd src

mkdir angular, netcore, electron

// Create NodeJS Project
npm init
// After above command, it will ask some questions
// response apropriate information for npm init questions

// install electron libraries with nodejs
cd electron
npm i -D electron@latest
```

In this example it created initial `package.json` then I modified like this

```json
{
  "name": "cross-platform-desktop-application-with-netcore2x-and-angular6x",
  "version": "1.0.0",
  "description": "Cross Platform Desktop Application with .Net Core 2 and Angular 6",
  "main": "main.js",
  "scripts": {
    "start": "electron .",
    "build": "build"
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
    "electron": "^2.0.3",
    "electron-builder": "^20.15.1",
    "electron-packager": "12.1.0"
  },
  "bugs": {
    "url": "https://github.com/atillatan/cross-platform-desktop-application-with-netcore2x-and-angular6x/issues"
  },
  "homepage": "https://github.com/atillatan/cross-platform-desktop-application-with-netcore2x-and-angular6x#readme",
  "build": {
    "appId": "Cross-Platform-Desktop-Application-with-Net-Core-Angular",
    "directories": {
      "buildResources": "../../assets",
      "output": "../../dist/electron"
    },
    "extraResources": {
      "from": "../../dist/netcore/",
      "to": "dist/netcore",
      "filter": [
        "**/*"
      ]
    },
    "mac": {
      "category": "Cross Platform Desktop Application with .Net Core 2 and Angular 6"
    },
    "win": {
      "target": [
        "nsis"
      ]
    }
  }
}

```

install node packages, that is defined in `package.json`

```bash
npm install
```

## 3. Install Angular CLI

```bash
// go to angular directory
cd ../angular

// install angular
npm install -g @angular/cli
```

Create `dist` directory

```bash
// go to root directory
cd ../

// create dist, build directories
mkdir dist, build
```

**Editor**
I will use `Visual Studio Code` for editing the project
open project with Visual Studio Code

```bash
code .
```

In the `electron` project directory, Create `main.js` and paste below code
electron application is a nodejs aplication, it's has only single js file `main.js`

```js
const {
    app,
    BrowserWindow,
    Menu
} = require('electron');

const path = require('path');
const url = require('url');
// process.env.NODE_ENV = 'production';

let mainWindow;
const os = require('os');
var apiProcess = null;

// #region Events
app.on('ready', init);

app.on('window-all-closed', function () {
    if (process.platform !== 'darwin') {
        app.quit()
    }
});

app.on('activate', function () {
    if (mainWindow === null) {
        createMainWindow()
    }
});

process.on('exit', function () {
    console.log('Exit electron application..');
    apiProcess.kill();
});
// #endregion

function init() {
    startNetCoreApi();
    createMainWindow();
}

function createMainWindow() {
    console.log('start');
    //create new window
    mainWindow = new BrowserWindow({
        width: 920,
        height: 600,
        frame: true,
        resizable: true
    });

    mainWindow.loadURL('http://localhost:5000/index.html');
    // Quit app when closed
    mainWindow.on('close', function (e) {
        mainWindow = null;
    })
    // Create menu  
    const mainMenuTemplate = [{
        label: 'File',
        submenu: [{
            label: 'Quit',
            accelerator: process.platform == 'darwin' ? 'Command+Q' : 'Ctrl+q',
            click() {
                app.quit();
            }
        }]
    }];

    // if mac, add empty object to menu
    if (process.platform == 'darwin') {
        mainMenuTemplate.unshift({});
    }

    // Add developer tools item if not in production
    if (process.env.NODE_ENV !== 'production') {
        mainMenuTemplate.push({
            label: 'Developer Tools',
            submenu: [{
                    label: 'Toggle Devtools',
                    accelerator: process.platform == 'darwin' ? 'Command+i' : 'Ctrl+i',
                    click(item, focusedWindow) {
                        focusedWindow.toggleDevTools();
                    }
                },
                {
                    role: 'reload'
                }
            ]
        })
    }

    // Build menu from temmplate 
    const mainMenu = Menu.buildFromTemplate(mainMenuTemplate);
    // Insert menu
    Menu.setApplicationMenu(mainMenu);
}


function startNetCoreApi() {
    var spawn = require('child_process').spawn;

    var wokingDirectory = path.join(__dirname, '../../dist/netcore');

    if(process.env.NODE_ENV === 'production'){
        wokingDirectory = path.join(__dirname, '../dist/netcore');
    }

    var apiPath = path.join(wokingDirectory, '/netcore.exe');

    if (os.platform() === 'darwin') {
        apiPath = path.join(wokingDirectory, '//netcore');
    }

    console.log(apiPath);

    apiProcess = spawn(apiPath, {
        cwd: wokingDirectory
    });

    apiProcess.stdout.on('data', (data) => {
        console.log(`stdout: ${data}`);
        if (mainWindow == null) {
            console.log('createMainWindow');
            createMainWindow();
        }
    });
};
```

## 4. Create .Net Core Project

- Install .Net Core

Download latest version of .net core framework from [https://www.microsoft.com/net/download/windows](https://www.microsoft.com/net/download/windows) and install it.
After the installation you will have `dotnet` command environment in you terminal/command prompt

- Open your terminal or, windows PowerShell, then execute following commands

```bash
// Go to netcore project
cd src

dotnet new webapi -n netcore
cd netcore
dotnet restore
dotnet build
dotnet run
```

Add `netcore/Controllers/SpaController.cs` like this

```csharp
using System.Collections.Generic;
using Microsoft.AspNetCore.Mvc;

namespace netcore.Controllers
{
    [Route("[controller]/[action]")]
    public class SpaController : Controller
    {
        // GET spa/getusers
        [HttpGet]
        public IEnumerable<dynamic> GetUsers()
        {
            return new List<dynamic> {
                new { Name = "Bob", FamilyName = "Smith", Age = 32, email = "test1" },
                new { Name = "Alice", FamilyName = "Smith", Age = 33, email = "test2" },
                new { Name = "Amy", FamilyName = "Smith", Age = 32, email = "test3" },
                new { Name = "Adam", FamilyName = "Smith", Age = 32, email = "test4" }
             };
        }
    }
}
```

Add `netcore/Controllers/DefaultController.cs` like this

```csharp
using System.Collections.Generic;
using Microsoft.AspNetCore.Hosting;
using Microsoft.AspNetCore.Mvc;

namespace netcore.Controllers
{
    public class DefaultController : Controller
    {
        public IActionResult Index()
        {
            return File("~/index.html", "text/html");
        }
    }
}
```

Change  `startup.cs` like this

```csharp
using System.Collections.Generic;
using Microsoft.AspNetCore.Builder;
using Microsoft.AspNetCore.Hosting;
using Microsoft.Extensions.Configuration;
using Microsoft.Extensions.DependencyInjection;
using Newtonsoft.Json;

namespace netcore
{
    public class Startup
    {
        public IConfiguration Configuration { get; }
        public Startup(IConfiguration configuration) => Configuration = configuration;

        public void ConfigureServices(IServiceCollection services)
        {
            services
            .AddCors()
            .AddMvc()
            .AddJsonOptions(options =>
             {
                 options.SerializerSettings.ContractResolver = new Newtonsoft.Json.Serialization.DefaultContractResolver();
                 options.SerializerSettings.ReferenceLoopHandling = ReferenceLoopHandling.Serialize;
                 options.SerializerSettings.PreserveReferencesHandling = PreserveReferencesHandling.Objects;
             });
        }

        public void Configure(IApplicationBuilder app, IHostingEnvironment env)
        {
            if (env.IsDevelopment())
            {
                app.UseDeveloperExceptionPage();
            }

            app.UseCors(policy => policy.AllowAnyOrigin().AllowAnyHeader().AllowAnyMethod());

            app.UseStaticFiles();

            app.UseDefaultFiles(new DefaultFilesOptions { DefaultFileNames = new List<string> { "index.html" } });

            app.UseMvc(routes =>
           {
               routes.MapRoute(
                 name: "default",
                 template: "{controller}/{action}/{id?}");

               // Catch all Route - catches anything not caught be other routes
               routes.MapRoute(
                   name: "catch-all",
                   template: "{*url}",
                   defaults: new { controller = "Default", action = "Index" }
               );
           });

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
ng new angular --skip-tests --routing
// --routing : add routing functionality to project
// --skip-test: skip test functionality

cd angular
ng serve --open
```

Using the --open (or just -o) option will automatically open your browser on http://localhost:4200/.

You can also read the following tutorial [https://angular.io/guide/quickstart](https://angular.io/guide/quickstart) for Angular installation.

Add  HtmlClientModule to `app.module.ts` like this

```js
//  angular/src/app/app.module.ts
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
// angular/src/index.html
<!doctype html>
<html lang="en">

<head>
  <meta charset="utf-8">
  <title>Cross Platform Desktop Application</title>
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
    this.http.get<any>(`http://localhost:5000/spa/getusers`).subscribe(data => {
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

<table class="striped"> 
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
      <td>{{ user.Name }}</td>
      <td>{{ user.FamilyName }}</td>
      <td>{{ user.Age }}</td>
      <td>{{ user.email }}</td>
    </tr>
</table>

```

Change output directory from `angular.json`

```js
{
    "projects": {
        "angular": {
            "architect": {
                "build": {
                    ...
                    "options": {
                        ...
                        "outputPath": "../../dist/netcore/win/wwwroot",
                        ...
                    }
                    ...
                }
            }
    }
}

```

## 6. Integrate with Electron

```bash
// run.cmd
@echo off

:: publish netcore project
cd src/netcore
dotnet restore
dotnet build
dotnet publish -r win10-x64 --self-contained --output ../../dist/netcore

:: publish angular project
cd ../angular
:: npm install

cmd /c ng build --base-href ./


:: publish electron project
cd ../electron
::npm install

cmd /c npm start

```

```bash
// run.sh
#!/bin/sh

# publish netcore project
cd src/netcore
dotnet restore
dotnet build
dotnet publish -r osx.10.11-x64 --self-contained --output ../../dist/netcore

# publish angular project
cd ../angular
npm install

ng build --base-href=./ 

# publish electron project
cd ../electron
npm install

npm start
```

project source code: [https://github.com/atillatan/cross-platform-desktop-application-with-netcore2x-and-angular6x](https://github.com/atillatan/cross-platform-desktop-application-with-netcore2x-and-angular6x)

