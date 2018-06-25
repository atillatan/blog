---
layout: article
permalink: null
name: null
file_type: null
title: Inheritance with JavaScript, EC6 (ECMAScript 6, ECMAScript 2015)
description: Inheritance with JavaScript, EC6 (ECMAScript 6, ECMAScript 2015)
tags: javascript
category: null
sort_order: 70
rating: 100
changefreq: monthly
priority: 0.5
published: true
create_date: 2017-11-13
modified_date: 2017-11-13
created_by: atilla
modified_by: atilla
comments: true
redirect_url: null
---

# Object oriented javascript and Inheritance


## Inheritance with JavaScript, EC6 (ECMAScript 6, ECMAScript 2015)

- With EC6 the basic class syntax looks like this:

```javascript
class MyClass {
  constructor(...) {
    // ...
  }
  method1(...) {}
  method2(...) {}
  get something(...) {}
  set something(...) {}
  static staticMethod(..) {}
  // ...
}
```
The value of MyClass is a function provided as constructor. If there’s no constructor, then an empty function.

In any case, methods listed in the class declaration become members of its prototype, with the exception of static methods that are written into the function itself and callable as MyClass.staticMethod(). Static methods are used when we need a function bound to a class, but not to any object of that class.

## Inheritance Example
```javascript

class Animal {

  constructor(name){
    this.name=name;
  }

  toString(){
    return "Animal is name " + this.name;
  }

  static getAnimals(){
    return new Animal("No Name")
  }
}


class Dog extends Animal{

  constructor(name, owner){
    super(name);
    this.owner=owner;
  }

  toString(){
    return super.toString() + "<br/>Dog is named " + this.name;
  }
}

var rover = new Dog("Rover", "Paul");

document.write(rover.name + " is owned by " + rover.owner + "<br/>");
document.write(rover.toString() + "<br/>");

var bowser=Animal.getAnimals();
document.write("Bowser info : " + bowser.toString());

document.write("<hr/>");



```
Result:
```bash
Rover is owned by Paul
Animal is name Rover
Dog is named Rover
Bowser info : Animal is name No Name
```
