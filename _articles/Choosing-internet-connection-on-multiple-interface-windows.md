---
layout: article
permalink: null
name: null
file_type: null
title: Choosing internet connection on multiple interface windows
description: Choosing internet connection on multiple interface windows
tags: batch
category: null
sort_order: 110
rating: 100
changefreq: monthly
priority: 0.5
published: true
create_date: 2007-11-13T10:20:00Z
modified_date: 2007-11-13
created_by: atilla
modified_by: atilla
comments: true
redirect_url: null
---

# Choosing internet connection on multiple interface in windows

Basically, this batch file includes basic and important parameters.
You must change parameters to your own connection pieces of information.
This application configures windows route information (routing table).

```batch
rem ================== CONFITURATIONS =========================
set internetGatewayIPAddress=192.168.2.1
set specialGatewayIpAddress=192.168.200.3

set specialNetwork1=192.168.200
set specialNetwork2=192.168.0



rem ############# STARTING APPLICATION #######################
rem delete all targets
route DELETE 0.0.0.0 mask 0.0.0.0

rem add internet gateway
route add 0.0.0.0 mask 0.0.0.0 %internetGatewayIPAddress% METRIC 20
rem route add 192.168.2.0 mask 255.255.255.0 192.168.2.1 METRIC 20

rem add special network
route add %specialNetwork1%.0 mask 255.255.255.0 %specialGatewayIpAddress% METRIC 20
route add %specialNetwork2%.0 mask 255.255.255.0 %specialGatewayIpAddress% METRIC 20

rem ##########################################################
```
