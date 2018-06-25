---
layout: article
permalink:
name:
file_type:
title: Using CSS and JavaScript to an Angular Project
description: >-
  Using CSS and JavaScript to an Angular Project
tags:  
category:  
sort_order: 100
rating: 300
changefreq: monthly
priority: 0.5
published: true
create_date: 2018-05-25T00:00:00
modified_date: 2018-05-25
created_by: atilla
modified_by: atilla
comments: true
redirect_url:
toc: false
---

# Using CSS and JavaScript to an Angular Project

### 1. Add CSS file to Angular Project

You can import  your css file to "src/styles.css" file
add following line

```json
// styles.css

@import '~src/assets/custom-styles.css';

```

or you can add angular.json 

```js
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


### 2. Add Javascript Module to Angular Project

You can add the javascript file to "angular-cli.json" (Angular 6 and above add to "angular.json")

```json
// angular.json / angular-cli.json
 
"architect": {
  "build": {
	"options": {
	    ...
		"scripts": [
			...
      "src/assets/custom-module.js"
      ],
		...
		}
  }
}
 
```

Then add  some function to your `custom-module.js` file

```js
// custom-module.js
export class CustomModule {

  testMethod1(msg) {
    alert(msg);
  }

  testMethod2(msg) {
    alert(msg);
  }  
}
```

Then add your module to your typescript component

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

### 3. Add Javascript Utility  File to Angular Project (first usage)

You can add the javascript file to "angular-cli.json" (Angular 6 and above add to "angular.json")

```json
// angular.json / angular-cli.json

"scripts": [
  "src/assets/custom-utility.js"  
],
```

Then add some functions to your `custom-utility.js` file

```js
// custom-utility.js

export function testMethod1(msg) {
  alert(msg);
}
export function testMethod2(msg) {
  alert(msg);
}

```
Then add your utility to your typescript component

```js
// app-component.ts
import { Component, OnInit } from '@angular/core';
import { testMethod1, testMethod2 } from '../assets/custom-utility.js'; // <= inserted line 1.

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent implements OnInit {   
 
 ngOnInit() {    
    testMethod1('custom utility'); // <= inserted line 2.
  }

}
```


### 4. Add Javascript Utility  File to Angular Project (second usage)

You can add the javascript file to "angular-cli.json" (Angular 6 and above add to "angular.json")

```json
// angular.json / angular-cli.json

"scripts": [
  "src/assets/custom-utility.js"  
],
```

Then add some function to your `custom-utility.js` file

```js
// custom-utility.js

export function testMethod1(msg) {
  alert(msg);
}
export function testMethod2(msg) {
  alert(msg);
}

```
Then add your utility to your typescript component

```js
// app-component.ts
import { Component, OnInit } from '@angular/core';
import * as util from '../assets/custom-utility.js'; // <= inserted line 1.

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent implements OnInit {   
 
 ngOnInit() {    
    util.testMethod1('custom test'); // <= inserted line 2.
  }

}
```
