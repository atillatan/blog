---
layout: article
permalink:
name:
file_type:
title: Useful Mac OS Apps
description: >-
  Useful Mac OS Apps
tags:  
category:  
sort_order: 100
rating: 300
changefreq: monthly
priority: 0.5
published: true
create_date: 2017-11-23
modified_date: 2017-11-23
created_by: atilla
modified_by: atilla
comments: true
redirect_url:
---

# Useful Mac OS Apps

### 1. Homebrew
Homebrew is the most popular package manager for Mac OS X
intallation:

```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

Run the following command once you’re done to ensure Homebrew is installed and working properly:
```bash
brew doctor
```
updating Homebrew
```bash
brew update
```

upgrade all outdated apps
```bash
brew upgrade
```


### 2 Homebrew cask
Homebrew Cask extends Homebrew with support for quickly installing Mac applications like Google Chrome, VLC, and more. No more dragging and dropping applications!
```bash
brew install caskroom/cask/brew-cask
```


### 3 NodeJS
```bash
brew install node
```

### XQuartz
The XQuartz project is an open-source effort to develop a version of the X.Org X Window System that runs on OS X. Together with supporting libraries and applications, it forms the X11.app that Apple shipped with OS X versions 10.5 through 10.7.

```bash
brew cask install xquartz
```


### 4 Wine, WineTrick
Wine is an open source program for running Windows software on non-Windows operating systems. While it’s most often used on Linux, Wine can run Windows software directly on a Mac
installation:
```bash
brew install wine
brew install winetrick
```
after, you can run windows executables like this.
```bash
$ wine program.exe
```
or you can open windows executables with right click on Mac OS.  
download an install "open with wine" Mac OS context menu from  [here](/open-terminal-here-mac-os-x-service/)
![image](/assets/img/osxservices/4.png)

intall windows program using wine
```bash
wine setup.exe
```

making application shortcut for Mac OS
Open up the Script Editor. You should see a window with a large area you can type in near the top: this is where you write your AppleScript. In that area, type the following text:

```
tell application "Terminal"
    do script "/usr/local/bin/wine ~/.wine/drive_c/Program\\ Files/$PATH_TO_PROGRAM.exe"
end tell
```
You'll need to replace $PATH_TO_PROGRAM with the path from the Program Files directory to your program executable.

Or
you can download "Everything" windows program
