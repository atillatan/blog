---
layout: article
permalink:
name:
file_type:
title: Object oriented javascript, Inheritance
description: >-
  Object oriented javascript, Inheritance
tags: javascript
category:  
sort_order: 30
rating: 100
changefreq: monthly
priority: 0.5
published: true
create_date: 2017-11-13
modified_date: 2017-11-13
created_by: atilla
modified_by: atilla
comments: true
redirect_url:
---
# Object oriented javascript and Inheritance

## How we can define Class in javascript

```javascript
// Object Oriented JavaScript


// 1- We define Class

//Example-1 (Object Literal)
var MyClass = {};
//or
var MyClass = {
  propName1: "val1",
  propName2: "val2",
  myFunc1: function() {
    //...
  },
  myFunc2: function() {
    //...
  },
  SubClass: {
    subProp1: "sp1Val",
    subProp2: "sp2Val"
  }
};


//Example-2 (FunctionConstructor)
function MyClass() { /*....*/ };

//or
function MyClass(param1, param2) {
  this.propName1 = "val1";
  this.propName2 = "val2";
  this.myFunc1 = function() {
    /*....*/
  }
}

// 2- Create Instance
var object = new MyClass();
console.log(typeof obj);//result: object

// Base javascript Object functions
Object.hasOwnProperty();
Object.isPrototypeOf();
Object.propertyIsEnumerable();
Object.toLocaleString();
Object.toString();
Object.valueOf();
Object.constructor();//FunctionConstructor



// 3-  Public and Private properties
function MyClass(param1, param2) {

  this.publicProp1 = "publicProp1";

  var privateProp1 = "privateProp1";

  this.publicFunc1 = function() {
    /*....*/
  }

  var privateFunc1 = function() {
    /*....*/
  }
}

// 3- Add Constructor 1

function MyClass(param1, param2) {

  this.propName1 = "val1";

  this.propName2 = "val2";

  // Constructor
  this.MyClass = function(p1, p2) {
     this.propName1=p1;
     this.propName2=p2;
  }

  //....

  // Call Constructor
  this.myClass(arg1, arg2);
}

// 3- Add Constructor 2

function MyClass(param1, param2) {

  // Constructor Begin
  this.propName1=p1;
  this.propName2=p2;
  // Constructor End

  this.propName1 = "val1";

  this.propName2 = "val2";


}

```

## Inheritance 1

```javascript
"use strict";

// BaseClass defination
function BaseClass() {

  this.prop1 = "prop1";

  this.ShowVal1 = function() {
    console.log('BaseClass: '+this.prop1);
  };

};


// ExtendedClass defination
function ExtendedClass() {

  BaseClass.call(this);//we send this(ExtendedClass) into BaseClass constructor

  this.prop2 = "prop2";

  this.ShowVal2 = function() {
    console.log("ExtendedClass: "+this.prop2);
  };

};

//Run
var obj = new ExtendedClass();
obj.ShowVal1();
obj.ShowVal2();

```
Result:

```bash
BaseClass: prop1
ExtendedClass: prop2
```

## Inheritance 2


```javascript
"use strict";

// BaseClass defination
function BaseClass() {

  this.prop1 = "prop1";

  this.ShowVal1 = function() {
    console.log("BaseClass: " + this.prop1);
  };

};

BaseClass.prototype.ShowVal3 = function() {
  console.log('BaseClass: ' + this.prop1);
}


// ExtendedClass defination
function ExtendedClass() {

  BaseClass.call(this);

  this.prop2 = "prop2";

  this.ShowVal2 = function() {
    console.log("ExtendedClass: " + this.prop2);
  };

};
ExtendedClass.prototype = new BaseClass();

//Run
var obj = new ExtendedClass();
obj.ShowVal1();
obj.ShowVal2();
obj.ShowVal3();

```

Result:

```bash
BaseClass: prop1
ExtendedClass: prop2
BaseClass: prop1
```

## Inheritance 3

```javascript
"use strict";

// BaseClass defination
function BaseClass() {

  this.prop1 = "prop1";

  this.ShowVal1 = function() {
    console.log("BaseClass: " + this.prop1);
  };

};

// ExtendedClass defination
function ExtendedClass() {

  BaseClass.call(this);

  this.prop2 = "prop2";

  this.ShowVal2 = function() {
    console.log("ExtendedClass: " + this.prop2);
  };

  //override BaseClass
  this.ShowVal1 = function() {
    console.log("ExtendedClass: " + this.prop1);
  };

};
ExtendedClass.prototype = new BaseClass();

//Run
var obj = new ExtendedClass();
obj.ShowVal1();
obj.ShowVal2();
```

Result:

```bash
ExtendedClass: prop1
ExtendedClass: prop2
```


## Inheritance 4

```javascript
"use strict";

// BaseClass defination
function BaseClass() {

  this.prop1 = "base prop1";

};

BaseClass.prototype.ShowVal = function() {
  console.log("BaseClass: " + this.prop1);
}

// ExtendedClass defination
function ExtendedClass() {

  BaseClass.call(this);

  this.prop2 = "extended prop2";
};
ExtendedClass.prototype = new BaseClass();

ExtendedClass.prototype.ShowVal = function() {
  console.log("ExtendedClass: " + this.prop2);

  //Call base function
  BaseClass.prototype.ShowVal.call(this);
}

//Run
var obj = new ExtendedClass();
obj.ShowVal();

```
Result:

```bash
ExtendedClass: extended prop2
BaseClass: base prop1
```

Inheritance 5

```javascript
"use strict";

// BaseClass defination
function BaseClass() {

  this.prop1 = "base prop1";

};
BaseClass.prototype.ShowVal = function() {
  console.log("BaseClass: " + this.prop1);
}

// ExtendedClass defination
function ExtendedClass() {

  BaseClass.call(this);

  this.prop2 = "extended prop2";

  //overriding base function
  this.ShowVal = function() {
    console.log("ExtendedClass: " + this.prop2);
    //Call base function
    BaseClass.prototype.ShowVal.call(this);
  }

};
ExtendedClass.prototype = new BaseClass();

var obj = new ExtendedClass();
obj.ShowVal();

```

Result:

```bash
ExtendedClass: extended prop2
BaseClass: base prop1
```
