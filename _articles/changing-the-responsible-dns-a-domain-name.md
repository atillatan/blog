---
layout: article
permalink: null
name: null
file_type: null
title: Changing the Responsible DNS (Name Server) for a Domain Name
description: Changing the Responsible DNS (Name Server) for a Domain Name
tags: System
category: null
sort_order: 120
rating: 100
changefreq: monthly
priority: 0.5
published: true
create_date: 2024-12-15T10:20:00Z
modified_date: 2024-12-15
created_by: atilla
modified_by: atilla
comments: true
redirect_url: null
---

# Changing the Responsible DNS (Name Server) for a Domain Name

**Purpose:** To change the responsible DNS record for a domain name purchased from any provider.

Normally, companies from which we purchase domain names set their own DNS servers as the "Name Server" (NS) records for those domains. However, the purpose of this guide is to ensure that the company we purchased the domain from replaces the responsible "Name Server" records with the IP addresses of our own DNS servers.

## What Does This Process Provide Us?

This process allows us to function as a defined DNS provider on the internet. As a result:

- We can direct all the domains we have purchased to our own "Name Server."
- We can add subdomains and MX records to any domain we own.
- We gain complete control over all domain-related operations.

---

## Example Scenario:

Let’s assume we own three domain names, all purchased from **www.netsol.com**:

| Domain Name     | Name Server (NS)                     |
|-----------------|--------------------------------------|
| sirket1.com :   | ns1.netsol.com, ns2.netsol.com      |
| sirket2.com :   | ns1.netsol.com, ns2.netsol.com      |
| sirket3.com :   | ns1.netsol.com, ns2.netsol.com      |

Now, let’s define a new **Name Server** for one of these domains:

| Name Server      | IP Address            |
|------------------|------------------------|
| ns1.sirket1.com : |  68.78.88.98 (Our static IP address) |
| ns2.sirket1.com : |  68.78.88.98 (Our static IP address) |

---

## Updating the Domain Name NS Records:

Let’s modify the current **NS** records of the three domain names as follows:

| Domain Name     | Name Server (NS)                     |
|-----------------|--------------------------------------|
| sirket1.com   :  |  ns1.sirket1.com, ns2.sirket1.com     |
| sirket2.com   :  |  ns1.sirket1.com, ns2.sirket1.com     |
| sirket3.com   :  |  ns1.sirket1.com, ns2.sirket1.com     |

After these updates, when someone on the internet tries to access **www.sirket2.com**, the DNS query for the domain will proceed as follows:

1. The query is sent to the root DNS servers.
2. Starting from the root DNS servers, the query eventually reaches our DNS server.
3. Since our server is now the responsible DNS, it will be asked for the IP address of the **www** subdomain.
4. Our DNS server will return the IP address defined for the **www** subdomain in our configuration.

![DNS-Name-Server-Process.png]({{site.img}}/DNS-Name-Server-Process.png)
---

## Important Note:

After making these changes, don’t assume, “I made the changes, but it’s not working yet.” Some of these updates may take anywhere from **1 minute to 24 hours** to become active on the internet.

For example, if you set the **NS** record for **sirket2.com** to **ns1.sirket1.com**, it may take up to **24 hours** for this change to propagate and become active.

---

**Date:** 2024-12-15

---

 