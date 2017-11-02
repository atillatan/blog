---
layout: article
title: Duckdns ile Dinamik IP adresinize Alan adi tanimlayin.
description: Duckdns ile Dinamik IP adresinize Alan adi tanimlayin.
sortorder: 100
---


# Duckdns ile Dinamik IP adresinize Alan adi tanimlayin.
osx
if you are not familiar with using the terminal on OSX consider using the JAR file (from the windows-gui) from http://www.etx.ca/

osx (10.8 or older) by default does have cron installed,
when you open the crontab, a new crontab will be setup for your user
lets get started and make a directory to put your files in, move into it and make our main script
these instructions are for the user administrator change the paths to match your user
open a new terminal, it will be in your home directory
```bash
mkdir duckdns
cd duckdns
vi duck.sh
```
now copy this text and put it into the file (in vi you hit the i key to insert, ESC then u to undo)	The example below is for the domain atilla
if you want the configuration for a different domain, use the drop down box above
you can pass a comma separated (no spaces) list of domains
you can if you need to hard code an IP (best not to - leave it blank and we detect your remote ip)
hit ESC then use use arrow keys to move the cursor x deletes, i puts you back into insert mode
```bash
echo url="https://www.duckdns.org/update?domains=atilla&token=e61a956c-0fe5-498a-945f-7483addfe736&ip=" | curl -k -o /Users/administrator/duckdns/duck.log -K -
```
now save the file (in vi hit ESC then :wq! then ENTER)
this script will make a https request and log the output in the file duck.log
now make the duck.sh file executeable
```bash
chmod 700 duck.sh
```
next we will be using the cron process to make the script get run every 5 minutes
```bash
crontab -e
```
copy this text and paste it at the bottom of the crontab
```bash
*/5 * * * * /Users/administrator/duckdns/duck.sh >/dev/null 2>&1
```

now save the file (CTRL+o then CTRL+x)
lets test the script
```bash
./duck.sh
```
this should simply return to a prompt
we can also see if the last attempt was successful (OK or bad KO)
```bash
cat duck.log
```
if it is KO check your Token and Domain are correct in the duck.sh script

what now?
Well you probably want to setup port forwarding on your router to make use of your new DDNS name
we recommend portforward.com to learn all about this.
