---
layout: article
permalink:
name:
file_type:
title: front-end projects with nodejs gulp bower yeoman and angularjs
description: >-
  front-end projects with nodejs gulp bower yeoman and angularjs
tags:  
category:  
sort_order: 100
rating: 300
changefreq: monthly
priority: 0.5
published: true
create_date: 2017-11-23T00:00:00
modified_date: 2017-11-23
created_by: atilla
modified_by: atilla
comments: true
redirect_url:
---

# Front-End project with nodejs gulp bower yeoman and angularjs


instal NodeJS

```bash
$ brew install node
```

install bower
```bash
$ npm install bower -g
```

create simple bower projects

```bash
$ mkdir bower-example
$ cd bower-example
$ touch .bowercc
```
and define library directory name

```json
{
  "directory": "lib"
}
```
then  create bower.json
```bash
$ touch bower.json
```
define your front-end javascript libraryes like this.

```json
{
  "name": "core",
  "private": true,
  "dependencies": {
    "jquery": "3.2.1",
    "font-awesome": "4.7.0",
    "bootstrap": "3.3.7"
  }
}
```

create your index.html
```bash
$ touch index.html
```
```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title></title>
     <script type="text/javascript" src="/lib/yourlibs...."></script>
  </head>
  <body>
    <h1>Welcome to example bower web project</h1>
  <h2>front-end package management</h2>
    <article class="container">
      Bower can manage components that contain HTML, CSS, JavaScript, fonts or even image files

    </article>
    <pre>
      # installs the project dependencies listed in bower.json
      $ bower install

      # registered package
      $ bower install jquery


      # Git endpoint
      $ bower install git://github.com/user/package.git

      # URL
      $ bower install http://example.com/script.js


    </pre>
  </body>
```
install bower packages
```bash
$ bower install
```
intall gulp

```bash
$ npm install gulp -g
```

intall yeoman
```bash
$ npm install yo -g
```

install generator

```bash

```
