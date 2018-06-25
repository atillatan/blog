---
layout: article
permalink: null
name: null
file_type: null
title: Singleton Pattern with Javascript
description: Singleton Pattern with Javascript
tags: javascript
category: null
sort_order: 73
rating: 100
changefreq: monthly
priority: 0.5
published: true
create_date: 2017-11-13T00:00:00
modified_date: 2017-11-13
created_by: atilla
modified_by: atilla
comments: true
redirect_url: null
---

# Singleton Pattern with Javascript


```JavaScript

function SingletonClass(name){

  //check if instance exist, we can maintain Single instance with this.
  if(typeof SingletonClass.instance === 'object'){
    return SingletonClass.instance;
  }

  this.name = name;
  SingletonClass.instance = this;
	return this;
}



var mySingletonClass = SingletonClass("Variable");
document.write("My SingletonClass name is " + mySingletonClass.name + "<br />")

var nextSingletonClass = SingletonClass("next");
document.write("My SingletonClass name is " + mySingletonClass.name + "<br />")


```

Another Example

```JavaScript

function AppSettings(){
  if(typeof AppSettings.instance === 'object'){
    return AppSettings.instance;
  }

  this.name = "Application1";
  this.url ="http://www.domain.com";
  this.defaultPageSize=30;
  this.defaultLang='en';

  //.....other application settings

  AppSettings.instance = this;
  return this;
}

```
Usage

```JavaScript

var v1 = AppSettings.url;
console.log(v1);

```
