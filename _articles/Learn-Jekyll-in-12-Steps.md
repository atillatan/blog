---
layout: article
permalink:
name:
file_type:
title: Learn Jekyll in 12 Steps
description: >-
  Learn Jekyll in 12 Steps
tags:  
category:  
sort_order: 100
rating: 100
changefreq: monthly
priority: 0.5
published: true
create_date: 2017-10-23T00:00:00
modified_date: 2017-10-23
created_by: atilla
modified_by: atilla
comments: true
redirect_url:
toc: false
---
{% raw %}
# Learn Jekyll in 12 Steps

Jekyll is a simple, blog-aware, static site generator perfect for personal, project, or organization sites. Think of it like a file-based CMS, without all the complexity. Jekyll takes your content, renders Markdown and Liquid templates, and spits out a complete, static website ready to be served by Apache, Nginx or another web server. Jekyll is the engine behind GitHub Pages, which you can use to host sites right from your GitHub repositories.


## 1. Installation

```bash
# update gem
$ sudo gem update --system
# install jekyll
$ sudo gem install jekyll
```

## 2. Create simple jekyll website and run

```bash
$ touch index.html
$ nano index.html
```
paste into some html.
```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>my title</title>
  </head>
  <body>
    <h1>Test</h1>
  </body>
</html>
```
```bash
# create jekyll configuration file.
$ touch _config.yml

```
content of \_config.yml
```xml
markdown: redcarpet
baseurl: /blog
```
run jekyll
```bash
$ jekyll serve
## further example
## jekyll serve --watch --baseurl ""
# navigate http://127.0.0.1:4000

```
navigate to [http://127.0.0.1:4000/blog/](http://127.0.0.1:4000/blog/)

## 3. Layouts

Create `_layouts` folder in your website
```bash
# this is the special folder for jekyll
$ mkdir _layouts
$ cd _layouts
$ touch default.html
$ nano default.html
```
after paste below html

```html
<html>
  <head>
    <meta charset="utf-8">
    <title>my title</title>
  </head>
  <body>
  {{content}}
  </body>
</html>
```
change your index.html like below

```html
<h1>Test</h1>
```
note: You can extend layouts with sub layouts
## 4. Includes

Create `_includes` folder in your website
```bash
# this is the special folder for jekyll
$ mkdir _includes
$ cd _includes
$ touch nav.html
$ nano nav.html

```

create a new page named nav.html

```html
<ul>
  <li><a href="{{site.baseurl}}/index.html">Ana sayfa</a></li>
  <li><a href="{{site.baseurl}}/news.html">Ana sayfa</a></li>
</ul>
````
and change your `_layouts/default.html` page like bellow

```html
<!DOCTYPE html>
<html>
  <head>                                                                                                                                                                                                                                            
    <meta charset="utf-8">
  <title>my title</title>
  </head>
  <body>
  {% include nav.html %}

  {{content}}

  </body>
</html>
```
you can send variable to included page like below
```html
  {% include nav.html type='active' %}
  # you can catch variable like below
  include.type
```

## 5. Css and if statement

Create `css` folder and add `common.css`
Create `_includes` folder in your website


```html
<ul>
  <li><a href="{{site.baseurl}}/index.html"  class="{% if page.url=='/index.html' %}current{% endif %}">Home</a></li>
  <li><a href="{{site.baseurl}}/news.html"  class="{% if page.url=='/news.html' %}current{% endif %}">News</a></li>
</ul>

# or contains condition
<ul>
  <li><a href="{{site.baseurl}}/index.html"  class="{% if page.url contains 'index.html' %}current{% endif %}">Home</a></li>
  <li><a href="{{site.baseurl}}/news.html"  class="{% if page.url=='/news.html' %}current{% endif %}">News</a></li>
</ul>

```

## 6. Posts
Create `_posts` folder in your website
```bash
# this is the special folder for jekyll
$ mkdir _posts
$ cd _posts
# file name is the special name for jekyll
$ touch 2017-01-01-First-Blog-Post.md
$ nano 2017-01-01-First-Blog-Post.md

```

put the html like below
```html
<ul>
  {% for item in site.posts %}
<li>
  <a href="{{site.baseurl}}{{item.url}}">{{ item.title }}</a>
  <p>{{ item.meta }}</p>
</li>
  {% endfor %}
</ul>
# or specific category loop


<ul>
  {% for item in site.categories.news %}
<li>
  <a href="{{site.baseurl}}{{item.url}}">{{ item.title }}</a>
  <p>{{ item.meta }}</p>
</li>
  {% endfor %}
</ul>

# we can limit for loop like this
<ul>
  {% for item in site.posts limit:1%}
<li>
  <a href="{{site.baseurl}}{{item.url}}">{{ item.title }}</a>
  <p>{{ item.meta }}</p>
</li>
  {% endfor %}
</ul>

note: for collection items have a `.url` property, jekyll sets the `.url` property

```

## 7. Data
Create `_data` folder in your website
```bash
# this is the special folder for jekyll
$ mkdir _data
$ cd _data
# file name is the special name for jekyll
$ touch menu.yml
$ nano menu.yml

```
put the data like below
```yml
- title: menu1
  meta: meta1
  folder: menu
  content: 'Sample **markdown** text1'

- title: menu2
  meta: meta2
  folder: menu
  content: 'Sample **markdown** text2'

- title: menu3
  meta: meta3
  folder: menu
  content: 'Sample **markdown** text3'


```

end loop in your data

```html
<ul>
  {% for item in site.data.news %}
<li>
  <a href="{{site.baseurl}}/menu/{{item.folder}}">{{ item.title }}</a>
  <p>{{ item.meta }}</p>
</li>
  {% endfor %}
</ul>
```

## 8. Pages
we can loop in site.pages

```html
<ul>
{% for page in site.pages %}
{% if page.url contains 'html' and page.publish==true %}
<li><a href="{{site.baseurl}}{{page.url}}">{{page.title}}</a></li>
{% endif %}
{% endfor %}
</ul>

```

## 9. Using site.pages metadata in layouts
if you are using `page` variable in your page, you can use it in layout

page: page1.md

```html
---
layout: default
title: page1 title
meta: page1 meta
publish: true
---

this is **markdown** text
```
layout: default.html
```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>{% if page.title %}{{page.title}} . {% endif %} - Common Title</title>
  <link rel="stylesheet" href="{{site.baseurl}}/css/common.css">
  </head>
  <body>
  {% include nav.html %}
  {{content}}
  </body>
</html>

```

note: If you put this
```
---
---
```
in some file, jekyll takes action for this file.

## 10. SiteMap.xml
sample sitemap.xml:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">

<url>
  <loc>http://....</loc>
  <changefreq>monthly</changefreq>
  <priority>0.5</priority>
</url>

</urlset>  
```
create `_includes/sitemap-entry.xml`
```xml
<url>
  <loc>http://..../{{site.baseurl}}{{include.entry.url}}</loc>
  {% if include.entry.changefreq %}
  <changefreq>{{include.entry.changefreq}}</changefreq>
  {% endif %}
  {% if include.entry.priority %}
  <priority>{{include.entry.priority}}</priority>
  {% endif %}
</url>
```
create your `sitemap.xml` in root path

```xml
---
---
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">

{% for page in site.pages %}
  {% if page.layout %}
    {% include sitemap-entry.xml entry=page %}
  {% endif %}
{% endfor %}

{% for post in site.posts %}
{% include sitemap-entry.xml entry=post %}
{% endfor %}

</urlset>

```


## 11. Pretty url

you can remove `.html` extension from your pages
in the config `_config.yml` you can add `permalink: pretty`

sample config file:
```yml
markdown: redcarpet
baseurl: /blog
permalink: pretty
```

## 12. Collections

Collection is a folder that is contains pages, we can define our collection folder in config file like below

```yml
markdown: redcarpet
baseurl: /blog
permalink: pretty

collections:
  downloads:
    output: true
    permalink: /downloads/:path/


```

create `_downloads` folder in you root folder and put it blow files
item1.md:
```
---
layout: default
title: Download item1
description: item1 description
---
Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```
item2.md:
```
---
layout: default
title: Download item2
description: item2 description
---
Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```
item1.md:
```
---
layout: default
title: Download item3
description: item3 description
---
Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```
and create `downloads.html` and loop these files.

[Download example project](/blog.zip)

[Explore the Jekyll plugins](https://jekyllrb.com/docs/plugins/)

[Useful snippets](https://github.com/mdo/jekyll-snippets)

## Further Steps

folder structure:
```
_data
  authours.yml
  language-en.yml
  language-tr.yml
  top-navigation.yml
  left-navigation.yml
  footer-socialmedia.yml
  footer-netwrok.yml
  dropdowns.yml
_drafsts
_includes
_posts
_layouts
assets
  css
  fonts
  img
  js

pages
feed.xml
sitemap.xml
index.md

```
{% endraw %}
