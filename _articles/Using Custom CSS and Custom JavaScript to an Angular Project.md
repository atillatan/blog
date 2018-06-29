---
layout: article
permalink:
name:
file_type:
title: Using Custom CSS and Custom JavaScript to an Angular Project
description: >-
  Using Custom CSS and Custom JavaScript to an Angular Project
tags:  
category:  
sort_order: 100
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

# Using Custom CSS and Custom JavaScript to an Angular Project

### 1. Add Custom CSS file to Angular Project

You can import  your css file to "src/styles.css" file
add following line

```json
// styles.css

@import '~src/assets/custom-styles.css';

```

or you can add angular.json 

```js
// angular.json

"architect": {
    "build": {
      "options": {
      ...
      "styles": [
          "src/assets/custom-styles.css",
          "src/styles.css"
        ],
      ...
      }
    }
}
```

Then add some style to custom-styles.css

```css
// custom-styles.css

.test-style {
    color: red;
}
```

Then add your style to your html file

```html
<body>
 <h1 class="test-style">Test</h1>
 // ...
 
</body>
```

### 2. Add External JavaScript to Angular Project

```js
// angular.json
{
  //..
  "projects": {
    "Enterprise-Angular-Project": {
      //..
      "architect": {
        "build": {
          //..
            "scripts": [    
              "node_modules/jquery/dist/jquery.slim.min.js",
              "node_modules/popper.js/dist/umd/popper.min.js",
              "node_modules/bootstrap/dist/js/bootstrap.min.js",
              "src/assets/external.utils.js"
            ]
          },
          //..
          }
      },
      //..
  }
}
```

Create file  `external.utils.js` and paste below code

```js
// external.utils.js
function testMethod(msg) {
  alert(msg);
}

```

You can use this javascript methods in html file like below

```html
<body  onload="testMethod('test')">
  <app-root></app-root>
</body>
```

If you want to use javascript file in angular components, you can import like this.

```js
import * as util from '../../assets/external.utils.js';
```

Then you must export functions

```js
export function testMethod(msg) {
  alert(msg);
}
```

After that  you can use this in Angular component

```js
import { Component, OnInit, Inject } from '@angular/core';
import * as utils from '../../assets/external.utils.js';

@Component({
  selector: 'app-contact',
  templateUrl: './contact.component.html'
})
export class ContactComponent implements OnInit {
  constructor() {

      utils.testMethod('testMethod');
  }
}

```

### 3. Add Custom ES6 (TypeScript) Module to Angular Project

Create file under `assets` folder `custom-module.ts`  then paste bolow code

```js
// custom-module.ts

export class CustomModule {

    testMethod1(msg) {
      console.log(msg);
    }
  
    testMethod2(msg) { 
      console.log(msg);
    }
  } 

```

Then import this top of angular component

```js
import { Component, OnInit } from '@angular/core';
import { CustomModule } from '../../assets/custom-module';

@Component({
  selector: 'app-contact',
  templateUrl: './contact.component.html'
})
export class ContactComponent implements OnInit {

  animal: string;
  core: CustomModule = new CustomModule();

  constructor() {
    // use your method like this.
    this.core.testMethod1('testMethod1');
  }
}
```

### 4. Add Custom Javascript Module to Angular Project

Create file under `assets` folder `custom-module.js`  then paste bolow code

```js
// custom-module.js

export class CustomModule {

    testMethod1(msg) {
      console.log(msg);
    }
  
    testMethod2(msg) { 
      console.log(msg);
    }
  } 

```

Then import this top of angular component

```js
import { Component, OnInit } from '@angular/core';
import { CustomModule } from '../../assets/custom-module.js';

@Component({
  selector: 'app-contact',
  templateUrl: './contact.component.html'
})
export class ContactComponent implements OnInit {

  animal: string;
  core: CustomModule = new CustomModule();

  constructor() {
    // use your method like this.
    this.core.testMethod1('testMethod1');
  }
}
```

 