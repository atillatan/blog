---
layout: article
permalink:
name:
file_type:
title: Make spotlight index markdown or code files
description: >-
  Make spotlight index markdown or code files
tags:  
category:  
sort_order: 100
rating: 100
changefreq: monthly
priority: 0.5
published: true
create_date: 2017-10-23T10:20:00Z
modified_date: 2017-10-23
created_by: atilla
modified_by: atilla
comments: true
redirect_url:
---


# How can I make spotlight index markdown or code files?


Add this to `Info.plist` in `/System/Library/Spotlight/RichText.mdimporter/Contents/` and Spotlight will search for markdown and source code files.



```
<string>public.c-header</string>
<string>public.c-plus-plus-header</string>
<string>public.c-source</string>
<string>public.objective-c-source</string>
<string>public.c-plus-plus-source</string>
<string>public.objective-c-plus-plus-source</string>
<string>com.sun.java-source</string>
<string>public.perl-script</string>
<string>public.python-script</string>
<string>public.csh-script</string>
<string>public.shell-script</string>
<string>public.ruby-script</string>
<string>public.php-script</string>
<string>com.netscape.javascript-source</string>
<string>net.daringfireball.markdown</string>
```

Open terminal and paste above text,
after the `<string>org.openxmlformats.wordprocessingml.document</string>`

```bash
$ sudo vi /System/Library/Spotlight/RichText.mdimporter/Contents/Info.plist
# locate your cursor after <string>org.openxmlformats.wordprocessingml.document</string>
# press key "i" on your keyboard
# press paste above text with pressing CMD+V
# press "esc"
# press ":"
# press "q" and hit "Enter"
```


After adding the desired file types you have to run
```
mdimport -r /System/Library/Spotlight/RichText.mdimporter
```
to update the new file extensions.

To re-index the HD you can run

```
sudo mdutil -E /
```
