---
layout: article
title: Make spotlight index markdown or code files
description: Make spotlight index markdown or code files
comments: true
sortorder: 100
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
sudo vi /System/Library/Spotlight/RichText.mdimporter/Contents/Info.plist
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
