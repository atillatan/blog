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
create_date: 2017-11-13T00:00:00.000Z
modified_date: 2017-11-13T00:00:00.000Z
created_by: atilla
modified_by: atilla
comments: true
redirect_url: null
---

# Object oriented javascript and Inheritance


## Inheritance with JavaScript, EC6 (ECMAScript 6, ECMAScript 2015)


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
