---
layout: article
permalink:
name:
file_type:
title: ASP.NET Core on Linux with Apache
description: >-
  ASP.NET Core on Linux with Apache
tags:  
category:  
sort_order: 100
rating: 100
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



# ASP.NET Core on Linux with Apache

Apache is a very popular HTTP server and can be configured as a proxy to redirect HTTP traffic to kestrel.
We will learn how to set up Apache on CentOS 7 and use it as a reverse proxy to welcome incoming connections and redirect them to the ASP.NET Core application running on Kestrel.
We must install the mod_proxy extension and other related Apache modules.

### 1. Connect your linux server with

```bash
$ ssh root@123.123.123.123
```

### 2. Install Apache

```bash
$ sudo yum update -y
$ sudo yum -y install httpd mod_ssl
```

### 3. Install and enable the .NET SDK
After registering with the Subscription Manager and enabling the .NET Core channel, you are ready to install and enable the .NET SDK.

In your command prompt, run the following commands:

```bash
$ yum install rh-dotnet20 -y
$ scl enable rh-dotnet20 bash
```

### 4. Create your app

```beans
$ mkdir /app/web
$ cd /app/web
$ dotnet new mvc -o dotnet-mvc
$ cd dotnet-mvc
```

### 5. Run your app

```beans
$ dotnet run
```

### 6. Configure Apache for reverse proxy

Create your apache configuration file in this location

```bash
$ cd /etc/httpd/sites-available
$ touch mydomain.com.conf
$ nano mydomain.com.conf
```
insert below text in your configuration file


```xml
<VirtualHost *:80>
  ServerName www.mydomain.com
  ProxyPreserveHost On
  ProxyPass / http://127.0.0.1:5000/
  ProxyPassReverse / http://127.0.0.1:5000/
  ErrorLog /var/log/httpd/mvc-error.log
  CustomLog /var/log/httpd/mvc-access.log common
</VirtualHost>
```
### 7. Run Apache

```bash
$ sudo service httpd configtest
$ sudo systemctl restart httpd
```

if you get an http-503 error, you can run below command

```bash
sudo setsebool -P httpd_can_network_connect on
````
### 8. Monitoring our application
you can see httpd logs with tail

```bash
$ tail -f /var/log/httpd/mvc-access.log   
$ tail -f /var/log/httpd/mvc-error.log
```
