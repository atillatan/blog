---
layout: article
permalink: 
name: 
file_type: 
title: Google Cloud Fundamentals Core Infrastructure
description: >-
  Core Infrastructure introduces important concepts and terminology for working with Google Cloud. Through videos and hands-on labs, this course presents and compares many of Google Cloud's computing and storage services, along with important resource and policy management tools.
tags: 
category:  
sort_order: 21
rating: 302
changefreq: monthly
priority: 0.5
published: true
create_date: 2025-03-09
modified_date: 2025-03-09
created_by: atilla
modified_by: atilla
comments: true
redirect_url: 
toc: true
---

# Google Cloud Fundamentals: Core Infrastructure



https://markmap.js.org/repl

Resources:

- Training: https://www.cloudskillsboost.google/paths/19/course_templates/60

**Google Cloud Fundamentals:** 

Core Infrastructure introduces important concepts and terminology for working with Google Cloud. Through videos and hands-on labs, this course presents and compares many of Google Cloud's computing and storage services, along with important resource and policy management tools.

*Resources:* 

https://www.cloudskillsboost.google/course_templates/60

[cloud.google.com/training](http://cloud.google.com/training), Qwiklabs

YouTube: https://www.youtube.com/@qwiklabs-courses2043/

**Key Objectives:**

1. Identify the **purpose and value** of Google Cloud products and services
2. Define **how infrastructure is organized** and controlled in Google Cloud.
3. Explain **how to create a basic infrastructure** in Google Cloud.
4. Select and **use Google Cloud storage** options.
5. Describe the **purpose and value of Google Kubernetes Engine**.
6. Identify the **use cases for serverless Google Cloud services**.
7. Combine Google Cloud knowledge with prompt engineering to improve Gemini responses.

**Cloud Console and Google Cloud Shell:**

Both Google Cloud Console and Google Cloud Shell provide interfaces to manage your VPC. The Console gives a user-friendly graphical interface, while Cloud Shell offers direct command-line functionality.

**Google Cloud API**:

- **Overarching API**: Google Cloud API can be thought of as an overarching suite that includes all the APIs provided by Google Cloud Platform. It encompasses APIs for all Google Cloud services, such as Compute Engine, Cloud Storage, BigQuery, Cloud Pub/Sub, and many more.
- **Comprehensive Access**: It provides a unified set of tools and endpoints that allow developers to interact with various Google Cloud services and manage resources across the entire platform.

### **Non-Google Cloud APIs:**

Outside the scope of Google Cloud API, you might find APIs related to other Google products not specifically tied to Google Cloud Platform, such as:  APIs not directly related to core cloud services but covering other functionalities like Google Maps, YouTube, Gmail, etc.

- **Google Maps API**: For location and mapping services.
- **YouTube API**: For interacting with YouTube content and data.
- **Google Sheets API**: To manipulate data within spreadsheets.
- **Google Photos API**: For interacting with photo-sharing services.
- **Google Sign-In API**: For authentication and authorization.

# 1. Overview of cloud computing

## **1.1 What is Cloud Computing:**

- youtube
    
    https://youtu.be/ph5hjgOAf40
    

US National Institute of Standards and Technology created this term. 

Cloud computing is a way of using information technology that has these five equally important traits.

1. Customers get computing resources that are on-demand and self-service
2. Customers get access to those resources over the internet, from anywhere
3. The provider of those resources allocates them to users out of that pool
4. The resources are elastic–which means they’re flexible, so customers can be
5. Customers pay only for **what they use, or reserve as they go**

**The history of cloud computing**

1. **Colocation**: Companies started to rent servers from services provider instead of investing physical space for them
2. **Virtualized Data Center**
3. **Container-based architecture**

## 1.2 IaaS and PaaS

https://youtu.be/C7cb6kFhNmw

**IaaS** - Infrastructure as a service: Require to manage OS and upper level operations.

- **Compute Engine** is an example of a Google Cloud IaaS service.
- Customers pay for the resources they allocate ahead of time;

**CaaS (Serverless)** - Container as a service: Requires management of the runtime and everything above it; users manage containerized applications, while the cloud provider handles the underlying OS and middleware.

**PaaS** - Platform as a service: (Example: IIS hosting) Requires management of application code and configurations; the cloud provider fully manages the underlying infrastructure, runtime, operating system, and middleware, allowing developers to focus on building applications.

- **App Engine** is an example of a Google Cloud PaaS service.
- Customers pay for the resources they actually use.

**FaaS (Serverless)** - Function as a Service: Requires management of individual functions or code snippets; the cloud provider handles everything else, including scaling and execution, allowing developers to run code in response to events without managing servers.

**SaaS** - Software as a Service:  Full fledged application on the Cloud. End users manage only the application itself; the cloud provider manages everything else, including the infrastructure, operating system, and application updates, providing ready-to-use software over the internet. e.g. Google Docs, Google Drive etc.

**Payment Model in GCP:** In the IaaS model, customers pay for the resources they allocate ahead of time; in the
PaaS model, customers pay for the resources they actually use.

<aside>
💡

**App Engine (Like IIS hosting or PHP hosting even Container hosting)**:  fully managed platform as a service (PaaS) designed to simplify the development and deployment of applications. It allows you to focus on writing code without the need to manage the underlying infrastructure.  

- Automatic Scaling
- Supported Languages: including Python, Java, Go, Node.js, PHP, and others.
- Built-in Services: authentication, storage, and data queries, enabling rapid development.
- Versioning: Allows multiple versions of an application to be deployed simultaneously.

**Standard Environment**: Offers predefined language runtimes and automatic scaling. Great for simple applications needing quick deployment.
**Flexible Environment:** Provides more customization, supporting Docker containers and allowing greater control over the runtime and software stacks.

**Ideal Use Cases:**

- **Web Applications:** Perfect for creating scalable web apps such as e-commerce sites, content management systems, and social applications.
- **APIs:** Can be used to deploy APIs with automatic scaling to handle varying loads.
- **Batch Processing:** Suitable for applications needing to perform batch processing tasks or background work.
</aside>

<aside>
💡

**Virtualization hardware layer:** Depending on CPU support. The following CPUs includes more efficient environment to VMs Intel VT-x, AMD-V

**Hypervisors**: are the software that manage these virtual environments.

**Type 1 (Bare-metal hypervisors):** These run directly on the physical hardware. Type 1 hypervisors do not require a  full fledged host operating system (bare-metal hypervisors uses lightweight operating system  with purpose is to host and manage virtual machines) Examples include:

 **- VMware ESXi**, 

 **- Microsoft Hyper-V**, 

  **- Xen**. 

**Type 2 (Hosted hypervisors):** These run on top of an operating system. Examples include **Oracle VirtualBox** and **VMware Workstation**. In this case, the hypervisor operates within the context of the host OS.

VMs depending on hypervisors drivers, we cannot install real driver to VM.  VMware ESXi, Microsoft Hyper-V, and others are designed primarily for server environments and data centers. As such, they may not support consumer-grade graphics cards commonly found in personal computers

Note: few layers missing in the following chart such as hypervisor and middleware.

**Middleware**: is software that helps different applications communicate with each other and share data. It acts as a bridge that connects different systems or services, making it easier for them to work together. Examples: Application Servers, Message Brokers, API Gateways

</aside>

![image.png](attachment:d1a43ea8-e4f4-4fa1-92e0-0224b08c563f:image.png)

**Serverless Computing**: Serverless computing allows developers to concentrate on their code, rather than on server configuration, by eliminating the need for any infrastructure management. Serverless technologies offered by Google include Cloud Functions which manages event-driven code as a pay-as-you-go service, and Cloud Run, which allows customers to deploy their containerized microservices based application in a fully-managed environment.

- **Cloud Functions:** is focused on single-purpose (only single function), stateless functions that respond to specific events
    - On-Demand (Auto-scaling)
    - Cloud Functions designed to handle one function per deployment. This means that each cloud function deployment is typically associated with a single entry point, or function, in your codebase
- **Cloud Runs:** Google Cloud Run allows you to deploy and manage containerized applications, providing flexibility for more complex applications and supporting concurrent requests
    - On-Demand (Auto-scaling)
    - Always-On (Auto-scaling)
    - Can include multiple functions, such as a RESTful API with multiple endpoints.

✅ **Use Cloud Run** when you need a **full microservice** or API.

✅ **Use Cloud Functions** when you need **small, event-driven serverless functions** without managing containers.

| **Feature** | **Cloud Run** | **Cloud Functions** |
| --- | --- | --- |
| **Execution Model** | Runs **full containerized applications** | Runs **single functions** triggered by events |
| **Scalability** | Auto-scales, can handle **HTTP requests, background tasks, and event-driven processing** | Auto-scales but is **designed for event-driven functions** |
| **Stateful vs. Stateless** | Can handle **stateful workloads** | Always **stateless** |
| **Triggers** | HTTP requests (REST APIs,  etc.), Pub/Sub, Task Queues | HTTP requests, Pub/Sub, Cloud Storage events, Firestore triggers, etc. |
| **Deployment** | Deploys a **full container image** | Deploys **individual function code** (without full container management) |
| **Use Case** | **Microservices, APIs, Background Processing** | **Event-driven functions, serverless logic, lightweight processing** |

**Choose Cloud Run instead of GKE when your application is** 

- **stateless**,
- needs to **scale rapidly without manual intervention**,
- and you prefer **minimal infrastructure management**,
- making it ideal for quick deployments and **cost-efficient operation**s with a**utomatic scaling based on request load**.

**Choose GKE** 

- requires advanced orchestration features,
- multi-service architecture,
- custom networking or scaling policies,
- and where you need comprehensive control over the deployment and management environment

## 1.3 The Google Cloud Network

https://youtu.be/0LIJioph_nY

Geographic [locations](https://www.notion.so/Google-Cloud-Fundamentals-Core-Infrastructure-1a4fa02451bc80fc95a0f1d0b82a9966?pvs=21) contains

- Geographic Locations (5)
    - Regions (41)
        - Zones (124)
        - Zone 1 - europe-west10-a
        - Zone 2 - europe-west10-b

Google has 100+ content caching nodes world wide

Zones are lower levels and  where Cloud resources are deployed.

![image.png](attachment:774410ab-38f3-47bf-b120-4f1face0d676:b438a943-32e2-46d0-8685-0191294d7efe.png)

Resources can run in different regions:

![image.png](attachment:9dd602f9-bc15-4bd2-a6bc-3d781338003d:image.png)

Using several regions provide us: improve fault tolerance

Google Cloud’s services support placing resources in what we call a multi-region (Latency measures)

**GKE:** Google Kubernates Engine

**GCP:** Google Cloud Platform

**Google Cloud’s operations suite** lets customers monitor workloads across multiple cloud providers

**Google Compute Engine (GCE)** is a core component of Google Cloud Platform (GCP) that provides Infrastructure as a Service (IaaS). It allows users to run virtual machines (VMs) on Google's infrastructure. 

## 1.4 Environmental impact

https://youtu.be/yOoOz6umhz0

Just like our customers, Google is trying to do the right things for the planet.

Therefore, it’s useful to note that Google's data centers were the first to achieve **ISO 14001 certification**, which is a standard that maps out a framework for an organization to enhance its environmental performance through improving resource efficiency and reducing waste.

As an example of how this is being done, here’s Google’s data center in Hamina, Finland.

Its cooling system, which uses sea water from the Bay of Finland, reduces energy use and is the first of its kind anywhere in the world.

By 2030, we aim to be the first major company to operate completely carbon free.

## 1.5 Security

https://youtu.be/BggWZl8qTzk

The security infrastructure can be explained in progressive layers, starting from the physical security of our data centers, continuing on to how the hardware and software that underlie the infrastructure are secured, and finally, describing the technical constraints and processes in place to support operational security.

**GCP Security Layers:**

- [Low-level infrastructure](https://cloud.google.com/docs/security/infrastructure/design?hl=en#secure-low-level) **physical premises**
- [Service deployment](https://cloud.google.com/docs/security/infrastructure/design?hl=en#secure-service)
- User Identity
- [Data storage](https://cloud.google.com/docs/security/infrastructure/design?hl=en#secure-data)
- [Internet communication](https://cloud.google.com/docs/security/infrastructure/design?hl=en#secure-internet)
- [Operations](https://cloud.google.com/docs/security/infrastructure/design?hl=en#operational-security)

The infrastructure automatically encrypts all infrastructure RPC traffic that goes between data centers.

- Google using hardware cryptographic accelerators that allow extend this default encryption to all infrastructure RPC traffic inside Google data centers.
- Google services that are being made available on the internet, register themselves with an infrastructure service called the **Google Front End (GFE)** , which ensures that all TLS connections
- The GFE additionally applies protections against (DoS) Denial of Service attacks.
- Google Operational security layer
    1. intrusion detection: Rules and machine intelligence give Google’s operational security teams warnings of possible incidents.
    2. reducing insider risk
    3. employee Universal Second Factor U2F use
    4. Software development practices

## 1.6 Open Source Ecosystems

https://youtu.be/gYZGSrNffF8

Some organizations are afraid to bring their workloads to the cloud because they're afraid they'll get locked into a particular cloud vendor.

for whatever reason, a **customer decides that Google is no longer the best provider for their needs**, we provide them with the ability to run their applications elsewhere.

Google publishes key elements of technology using open source licenses to create ecosystems that provide customers with options other than Google.

For example, TensorFlow, an open source software library for machine learning developed inside Google, is at the heart of a strong open source ecosystem.

Google provides interoperability at multiple layers of the stack.

Kubernetes and Google Kubernetes Engine give customers the ability to mix and match microservices running across different clouds, while Google Cloud Observability lets customers monitor workloads across multiple cloud providers.

## 1.7 Pricing and billings

Google Compute products are billed per-second

https://youtu.be/PRRf8y-Y5Bo

**Online Pricing Calculator**: https://cloud.google.com/products/calculator?hl=en

Billing Tools:

- Budgets: budget can be a fixed limit
- Alerts: Alerts are generally set at 50%
- Reports
- Quotas:
    - Traffic quota,
    - Allocation quota

**Compute Engine Discounts and Customization:**

- **Sustained-Use Discounts:**
    - You get automatic cost savings when your virtual machine runs for more than 25% of the month.
    - The longer you run the instance, the bigger the discount on usage charges for each additional minute.
- **Custom VM Types:**
    - You can choose specific amounts of CPU and memory for your virtual machines.
    - This customization lets you tailor the setup to fit your application needs, optimizing both performance and costs.

---

# 2. Resources and Access in the Cloud

## 2.1 Google Cloud Resource Hierarchy:

https://youtu.be/zdxQZh2iOFE

To use folders, you must have an organization node, which is the very topmost
resource in the Google Cloud hierarchy.

```java
Organization
   └── Folder (even sub-folders)
       └── Project
           └── Resource
```

![image.png](attachment:e0ac5910-80c5-476b-929b-73b42aae2a9b:image.png)

Folders could have sub folder, and folders facilitate policy inheritance.

Special roles are associated with the Organization Node:  Project Creator etc.

Project is the base for enabling and using Cloud services and resources

each resources belongs to just one project.

Each Google Cloud project has three identifying attributes: 

- a project ID, Globally unique identifier, can’t be changed means immutable
- a project name,
- a project number. Globally unique

Projects are billed and managed separately

Policies applied to: Projects, Folders and Organization node levels. Some Google Cloud services allow policies to be applied to individual resources too.

***** Resource Manager Tool:**  Provides project management.

**Resources are hierarchical:**

![image.png](attachment:10a657b2-9399-4811-9c24-441bdfe0ef7a:dd45416e-130c-4286-a988-6a12e7091e64.png)

**Resource hierarchy determines policies:**

![image.png](attachment:c364c3dc-4511-4ad1-afde-9fe3c142d08e:418a0466-c580-422a-a479-b8819d9eb240.png)

Folders let you assign policies to resources at a level of granularity you choose. The projects and subfolders in a folder contain resources that inherit policies and permissions assigned to that folder.

There are some special roles associated with this top level organization node. For example, you can designate an organization policy administrator, so that only people with privilege can change policies. You can also assign a project creator role, which is a great way to control who can create projects and, therefore, who can spend money.

Special roles for top levels organization node: **Policy administrator, Project creator**

## 2.2 Identity and Access Management - (IAM)

https://youtu.be/Di1T4RyO9yg

configures user role and policies.

- **Basic IAM roles:** Project Owner, Project Editor, Project Viewer and Project Billing Admin
- **Predefined IAM roles:** Instance Admin
- **Custom IAM role:** Instance Operator, cannot be applied to the folder level. it can be applied to organizational node and project level

Roles applied to projects and organizations

- **Cloud Identity:** mange's team and organization access. Cloud Identity defines user and group policies. With a tool called Cloud Identity, organizations can define policies and manage their users and groups using the **Google Admin console**
    
    ![image.png](attachment:c3c69472-479c-4744-817d-6854a36628e9:image.png)
    

- A **deny** policy **overrides** any existing **allow** policy regardless of the IAM role granted.
    - IAM always check **deny** policies before checking **allow** policies
- Normally policies inherited but in case of any deny policy in sub-level will override upper level allow policies.
- Differentiate IAM and Cloud Identity
    - IAM: Manages who can do what on Google Resources. Assigns permissions to users so they can access and manage GCP services (like Compute Engine, Cloud Storage)
    - Manages users and their access to applications. Provide Identity management features like SSO and MFA
    - **Integration**: Cloud Identity users can get permissions to use GCP resources via IAM.

![image.png](attachment:a96c6a43-c54a-4a58-9b03-1011e93b1503:image.png)

**Policies are managed and applied by IAM**

![image.png](attachment:8cb64155-db8c-4b56-87d2-91d95304418b:b6350874-beab-49b6-b3b0-2efd0d8710e4.png)

Applications in the GCP for users

- **Google Cloud Console:** deploy, scale, and diagnose resources.
- Cloud SDK and Cloud Shell
    - **Cloud SDK** is a set of tools that you can use to manage resources and
    applications hosted on Google Cloud. includes **gcloud CLI (Google Cloud CLI),**
    - **bq**: A command line tool for BigQuery
    - **Cloud Shell** provides command-line access to cloud resources directly from a
    browser is a debian based virtual machines.
        - Cloud Shell is a lightweight, **temporary virtual machine (Compute Engine VM)** that provides a command-line environment to manage Google Cloud resources using **Cloud APIs and CLI tools.**
- **APIs:** The third way to access Google Cloud is through application programming interfaces,
or APIs.
- **Google Cloud App:** which can be used to start,
stop, and use ssh to connect to Compute Engine instances, and to see logs from each
instance. It also lets you stop and start Cloud SQL instances.

## 2.3 Service Accounts

https://youtu.be/xoo5NfLqePY

Imagine you have a Compute Engine virtual machine running a program that needs to access other cloud services regularly.

Instead of requiring a person to manually grant access each time the program runs, you can give the virtual machine itself the necessary permissions.

- **Service accounts:** These are not user but these are services or automations that needs to use GCP resources. e.g. technical users.

## 2.4 Cloud Identity

https://youtu.be/EZccX9nFaiI

Cloud Identity's primary purpose is to provide organizations with a **centralized tool to manage user identities** and groups within Google Cloud. It addresses challenges such as efficiently removing access to cloud resources when someone leaves the organization. Through the **Google Admin Console,** administrators can define policies, manage users and groups, and seamlessly integrate with existing systems like Active Directory or LDAP. Cloud Identity also offers functionalities to disable accounts quickly and manage mobile devices, available in both free and premium editions. For Google Cloud customers using Google Workspace, these capabilities are already integrated.

## 2.5 Interacting with Google Cloud

https://youtu.be/KJS0FnXF7Kg

You can interact with Google Cloud in four ways

![image.png](attachment:38d00f6a-1722-4af0-bbc4-664c0ce780a1:28a0c222-dd21-4f7d-9233-c71f3695cffd.png)

**LAMP** stack: Linux, Apache, MySql and PHP 

**Bitnami**: Provide ready to use applications

**Google Cloud Marketplace**: Online store where users can find, deploy, and manage third-party applications, services

---

# 3. Virtual Machines and Networks in the Cloud

**VPC: Virtual Private Cloud is your cloud within the Cloud**

![image.png](attachment:110b5261-7e7e-4dce-a379-0c203296bc11:image.png)

VPC in google cloud is global. It spans all over the world and all of the regions.

## 3.1 Virtual Private Cloud networking

https://youtu.be/SFRCZvJN650

**First thing you need to do on Google Cloud**

Subnets is regional. We can have in subnet machines in different zones.

Zone: represent distinct physical locations withing a geographic region. 

Subnets: Subnets are defined at the regional level, which allows them to span multiple zones within the same region.

Its actually overlay network between zones under region.

- When you create a subnet, it is available to VMs in any of the zones of that region. This means you don't create separate subnets for each zone; instead, you utilize the same regional subnet for resources across different zones
- You can have VM instances in different zones of the same region that are part of the same subnet.
- When you create a subnet, it applies consistently across all zones within that region. This enables seamless communication between VM instances in different zones without needing separate IP address configurations for each zone.

**VPC subnets connect resources in different zones**

Tanrikulu VPC - global

- US East-1 Region
    - Zone-1
    - Zone-2
    - Subnet 1: 10.0.0/24
        - VM1-from Zone-1
        - VM2-from Zone-2
        - VM3-from Zone-2

Like follows, computers in the subnet placed in different zones. this provides resilient to distruptions

![image.png](attachment:0c5e2e5c-5b27-48c1-90da-4f5e307b12cb:image.png)

- Create your network.
    - Subnet is regional
    - VM belongs to Zone
    - Zone belong to Region

1- In the Cloud Console, on the **Navigation menu** (), click **VPC network** > **VPC networks**.

2- Click **default**.

3- Click **Subnets**.

4- In the left pane, click **Routes**.

5- In **Effective Routes** click **Network**, and then select **default**.

6- Click **Region** and select the Lab Region assigned to you by Qwiklabs.

## 3.2 Compute Engine

https://youtu.be/Oxwz5HbYUF8

With Compute Engine, users can create and run **virtual machines** on Google infrastructure. 

There are no upfront(onceden) investments, and thousands of virtual CPUs can run on a system that is designed to be fast and offer consistent performance.

**Compute Engine Pricing:**

![image.png](attachment:d7b9af8b-5986-411c-9e73-dc424fd40e05:image.png)

1. **Pay-as-You-Go Pricing:**
Compute Engine bills for virtual machines (VMs) by **the second**, with a one-minute minimum charge. This allows for flexible, granular billing based on actual usage rather than hourly rates.
2. **Sustained-Use Discounts:**
Automatically applied discounts for VMs that run for more than 25% of a month. The longer a VM runs, the greater the discount for every additional minute, making it cost-effective for long-running workloads.
3. **Committed-Use Discounts:**
Significant discounts (up to 57%) for customers who commit to using a specific amount of vCPUs and memory for one or three years. This option is ideal for stable and predictable workloads, providing cost savings for long-term planning.
4. **Preemptible VMs:**
Cost-saving options **for batch jobs** or workloads that can handle interruptions. Preemptible VMs can provide savings of up to 90%, but they can be terminated by Compute Engine if resources are needed elsewhere, so jobs must be designed to handle such interruptions.
5. **Spot VMs:**
Similar to Preemptible VMs but offer additional features. Spot VMs are also subject to being terminated when resources are needed but might provide more flexibility and options compared to Preemptible VMs.

## 3.3 Scaling virtual machines

https://youtu.be/YQK8u563me4

**1. Machine Types: Choosing the Right Resources**

- **Predefined Machine Types:** GCE offers a variety of pre-configured VM types. These are like pre-built computer configurations with a specific number of virtual CPUs (vCPUs) and a set amount of memory (RAM). You pick the one that best fits your workload's needs right out of the box. Examples include general-purpose, compute-optimized, memory-optimized, and accelerated-computing machine types.
- **Custom Machine Types:** Need something specific? GCE lets you create *custom* machine types. This means you can define the exact number of vCPUs and the amount of memory your VM has. This is useful for fine-tuning costs and performance if the predefined options don't quite match your requirements.

**2. Autoscaling: Dynamic Scaling Based on Demand**

- **What is Autoscaling?** Autoscaling is a GCE feature that automatically adjusts the number of VM instances running your application based on the current demand (load).
- **How it Works:**
    1. **Load Metrics:** Autoscaling monitors metrics like CPU utilization, memory usage, or network traffic.
    2. **Scaling Rules:** You define rules (thresholds) that trigger scaling events. For example, if CPU utilization exceeds 70%, scale up (add more VMs). If it drops below 30%, scale down (remove VMs).
    3. **Instance Groups:** Autoscaling works with Managed Instance Groups (MIGs). MIGs are collections of identical VMs that are managed as a single entity.
- **Load Balancing:** When you scale *out* (add more VMs), you need a way to distribute incoming traffic evenly across all those VMs. This is where Google Cloud Load Balancing comes in. Google Cloud offers various load balancers (HTTP(S), TCP, UDP, Internal) to efficiently distribute traffic to your VMs.

**3. Vertical vs. Horizontal Scaling**

- **Vertical Scaling (Scaling Up):** This means increasing the resources of a *single* VM. You're making it bigger. For example, you might increase the number of vCPUs and the amount of memory on an existing VM.
    - **Use Cases:** Vertical scaling is good for workloads that require a lot of resources on a single machine, such as in-memory databases or CPU-intensive analytics.
    - **Limitations:** There are limits to how large you can vertically scale a VM. The maximum number of vCPUs per VM is determined by its *machine family* (the type of underlying hardware) and the quota available in the zone where you're deploying the VM. Also, there is downtime involved, but you can decrease the downtime using live migration.
- **Horizontal Scaling (Scaling Out):** This means adding *more* VMs to handle the load. Instead of making one VM bigger, you're creating more VMs.
    - **Best Practice:** Horizontal scaling is generally the preferred approach in Google Cloud, especially for web applications and other distributed workloads. It provides better fault tolerance and scalability than vertical scaling.
    - **Example:** Imagine your website traffic suddenly spikes. With horizontal scaling, Autoscaling can automatically add more VMs to your Managed Instance Group to handle the increased traffic.

**In summary:** Google Compute Engine provides flexibility in scaling VMs. You can choose machine types that fit your needs, use autoscaling to adjust the number of VMs dynamically, and select between vertical and horizontal scaling strategies based on your workload requirements. Horizontal scaling is generally the recommended approach for cloud-native applications.

**GCE Scaling Explained:**

- **Machine Types:** Choose pre-defined or custom VM configurations (vCPUs, Memory).
- **Autoscaling:** Dynamically adjusts VM count based on load metrics. Requires Managed Instance Groups (MIGs) and Google Cloud Load Balancing.
- **Vertical Scaling (Scale Up):** Increase resources of a single VM. Limited by machine family and quotas.
- **Horizontal Scaling (Scale Out):** Add more VMs. Preferred for fault tolerance and scalability.
- **Key takeaway:** Horizontal scaling with autoscaling is the best practice for cloud-native applications on GCP.

## 3.4 Important Google Cloud VPC Capabilities

https://youtu.be/UtNlJbm8s2Q

Think like: VPC is your organizations Virtual Private Cloud that contains your Organization network, and you need to define Routing, Firewall, and VPC peering edge configuration between external world and your network

Virtual Private Cloud (VPC) is key to managing your cloud network. Understanding its routing, firewall, and peering capacities can optimize network security and performance.

**2. Routing Tables:** PCs do not require a router to be provisioned. They are used to forward traffic from one instance to another within the same network, **across subnetworks,** or even between Google Cloud zones, without requiring an external IP address.

- **Built-in Capability:** VPC routing tables are inherent within Google Cloud; no need for separate routers.
- **Functionality:** They direct traffic within networks, subnetworks, and zones without external IPs.

Example Use Case:

Sending data across regions efficiently without additional infrastructure setup.

**3. Firewall**

- **Global Distributed Firewall:** No explicit provisioning needed; control traffic in/out of instances.
- **Rule Definition:** Use network tags like "WEB" to manage access to instances consistently.

Quick Steps:

Access via **Navigation Menu** > **VPC network** > **Firewall Rules**.

Default rules include ICMP, RDP, SSH allowances; deny-all-ingress and allow-all-egress rules apply by default.

**4. VPC Peering**

- **Project Interconnectivity:** Facilitates traffic exchange between VPCs of different Google Cloud projects.
- **Shared VPC:** Leverage IAM for controlled cross-project interactions.

**Routing Tables:**

VPCs do not require a router to be provisioned.

Much like physical networks, VPCs have routing tables. **VPC routing tables are built-in** so you don’t have to provision or manage a router. They are used to forward traffic from one instance to another within the same network, **across subnetworks,** or even between Google Cloud zones, without requiring an external IP address.

**Firewall:**

VPCs also do not require a firewall to be provisioned.

Another thing you don’t have to provision or manage for Google Cloud is a firewall.

VPCs provide a global distributed firewall, which can be controlled to restrict access to instances through both incoming and outgoing traffic. 

Firewall rules can be defined through **network TAGS** on Compute Engine instances, which is really convenient. For example, you can tag all your web servers with, say, “WEB,” and write a **firewall rule** saying that traffic on ports 80 or 443 is allowed into all VMs with the **“WEB”** tag, no matter what their IP address happens to be

**Navigation menu** (), click **VPC network** > **VPC networks**.

1. In the left pane, click **Firewall**
2. there are 4 ingress firewall rules for the default network
    - default-allow-icmp
    - default-allow-rdp
    - default-allow-ssh
    - default-allow-internal

1. For **Firewall rules**, select all available rules. These are the same standard firewall rules that the default network had. The **deny-all-ingress** and **allow-all-egress** rules are also displayed, but you cannot check or uncheck them because they are implied. These two rules have a lower **Priority** (higher integers indicate lower priorities) so that the allow ICMP, custom, RDP and SSH rules are considered first.

you cannot create a VM instance without a VPC network.

**VPC Peering:**

You’ll remember that VPCs belong to Google Cloud projects, but what if your company has several Google Cloud projects and the VPCs need to talk to each other?

With VPC Peering, a relationship between two VPCs can be established to exchange traffic.

Alternatively, to use the full power of identity access management (IAM) to control who and what in one project can interact with a VPC in another, then you can configure a Shared VPC.

## 3.5. Cloud Load Balancing

https://youtu.be/HWJQ3LNagXc
**Cloud Load Balancing** can automatically scale your application behind a single anycast IP address, meaning it can distribute HTTP(S) traffic across multiple Compute Engine(VMs) regions worldwide. 

It's designed to improve application availability and reliability by spreading the traffic not just within a single region but across multiple regions if needed, adapting to changing traffic conditions and providing high availability.

You can put Cloud Load Balancing in front of all of your traffic: HTTP(S), TCP, SSL traffic, UDP traffic

Cloud Load Balancing includes, failover

quickly to changes in users, **traffic**, **network**, **backend health**, and other related conditions.

![image.png](attachment:c8f91263-a9a5-4b7c-bc93-9955641d74ee:image.png)

In summary, GCP manages load balancing for VMs by using **Managed Instance Groups** that automatically scale and distribute traffic among multiple instances based on a template. 

- This is similar to container orchestration, where new container instances are created to balance the load.

Google Cloud offers a range of load balancing solutions that can be classified based on the OSI model layer they operate at and their specific functionalities.

- **Application load balancers - Layer 7**: http, https TLS termination (Operate as Reverse Proxy)
    
    ![image.png](attachment:ab6ab923-205a-459e-9659-0cb60bccddbf:image.png)
    
- **Hardware load balancers Layer 4**: TCP, UDP
    - Network load balancers: Operate as Reverse Proxy
        
        ![image.png](attachment:30c88115-f026-41a6-9532-7db3ceec0a71:image.png)
        
    - Passthrough Network Load Balancers:
        
        Do not modify or terminate connections. Instead, they directly forward traffic to the backend while preserving the original source IP address.
        
        ![image.png](attachment:5a8c8f8f-2529-48db-b7b6-e81ea5cc70a8:image.png)
        
    

<aside>
💡

**Another Way for balancing load: Increase number of services automatically**

**Load Balancing for VMs:**

- **MIG - Managed Instance Groups:**
- **Scaling and Load Balancing:**
    - **Horizontal Scaling:** You can configure the MIG to automatically scale the number of VMs up or down based on demand. When traffic increases, the group can create additional VM instances to handle the load.
    - **Load Balancer:** GCP uses an external load balancer that distributes incoming traffic across all VM instances in the managed group. If one instance becomes heavily loaded, the load balancer routes traffic to other available instances.
        
        ![image.png](attachment:dce71590-ecda-4455-911f-045176cd78ea:image.png)
        
    - **VM Duplication:**
        - You can **duplicate VMs** by creating instances from a pre-defined instance template in a **Managed Instance Group**. This allows you to quickly spin up additional instances, similar to how containers are scaled.
        - **Instance Templates** define the settings for your VM instances (like machine type, boot disk image, and labels), allowing for consistent replication.
</aside>

<aside>
💡

**1- Unicast:
 A unicast** IP address is assigned to a single network interface or host. Data sent to a **Unicast** address is delivered to the specific machine identified by that address. It's the most common type of IP address used for direct communication between two devices over a network.

**2- Multicast**:

A Multicast IP address allows data to be transmitted to more than one hosts simultaneously. Devices interested in receiving the data join a specific Multicast group (by executing IGMP command), identified by a unique Multicast address. This is useful for applications such as streaming media where the same data must be delivered to many receivers.

> *Note: Multicast IP packets are structured in a way that distinguishes them from unicast packets. switches/routers understand multicast group*
> 

**3- Anycast**:

An Anycast IP address is assigned to multiple network interfaces or hosts. Data sent to an Anycast address is routed to the

**closest/nearest** host (shortest path, minimum latency)

in terms of network topography. Anycast is often used for load balancing and fault tolerance, as it allows the same service to be provisioned **from multiple locations,** providing the most efficient route to the data requester.

Proximity always updated with BGP

1.  Useful if you have multiple geographic location nodes. Load balancing utilized with requester location.

2. Failover and Redundancy: While not traditional load balancing, Anycast inherently provides failover capabilities. If one node is overwhelmed or offline, traffic is rerouted to the next nearest node, lending robustness to service availability.

3. Combining with DNS Load Balancing: Some implementations combine Anycast with DNS load balancing where DNS can round-robin or use other criteria to distribute awareness of which nodes to consider as viable Anycast endpoints.

4. Application-Level Adjustments:

</aside>

## 3.6 Cloud DNS and Cloud CDN

https://youtu.be/TYB1cur47mk

8.8.8.8 is one of the famous DSN server

**Cloud DNS**
Google Cloud offers Cloud DNS to help the world find them. 

- It’s a managed DNS service that runs on the same infrastructure as Google.
- It has low latency and high availability, and it’s a cost-effective way to make your applications and services available to your users. The DNS information you publish is served from redundant locations around the world.

**Cloud CDN (Content Delivery Network):**

Using CDN means 

- your customers will experience lower network latency,
- the origins of your content will experience reduced load, and
- you can even save money. Once HTTP(S) Load Balancing is set up,
- Cloud CDN can be enabled **with a single checkbox**

mostly used by static contents for web pages.

**Edge Caching:**

![image.png](attachment:90eedae2-a4ff-49a1-ae25-2a5569e3768f:image.png)

## 3.7 Connecting Networks to Google VPC

https://youtu.be/uTYwgmOEbWA

Many Google Cloud customers want to connect their Google Virtual Private Cloud networks to other networks in their system, such as on-premises networks or networks in other clouds.

![image.png](attachment:e8d91e1a-8f16-42dd-81a6-a3db61b3dc21:image.png)

1. **Cloud VPN:** Virtual Private Network connection over the internet and use **Cloud VPN** 
    - **Cloud Router:** To make the connection dynamic, a Google Cloud feature called **Cloud Router** can be used. Cloud Router lets other networks and Google VPC, exchange route information over the VPN using the Border Gateway Protocol (BGP). 
    Using this method, if you add a new subnet to your Google VPC, your on-premises network will automatically get routes to it.
        
        **IPsec VPN:** One option is to start with a Virtual Private Network connection over the Internet and use the **IPsec VPN** protocol to create a “tunnel” connection. To make the connection dynamic, a Google Cloud feature called Cloud Router can be used. Cloud Router lets
        other networks and Google VPC exchange route information over the VPN using the Border Gateway Protocol. Using this method, if you add a new subnet to your Google VPC, your on-premises network will automatically get routes to it.
        
2. **Direct Peering:** (Point of Presense PoP) without internet.  We would place our networking equipment, such as a router, within the same colocation 
facility where Google has a point of presence. called **“points of presence”**
- Google has more than 100 **points of presence** around the world
3. **Carrier Peering:** If we don't have our own equipment in a Google data center or a point of presence, we can connect through a partner who participates in the **Carrier Peering program**.
- Carrier peering gives you direct access from your on-premises network through a service provider's network to Google
- Workspace and to Google Cloud products that can be exposed through one or more public IP addresses.
- One downside of peering, though, is that it isn’t covered by a **Google Service Level Agreement SLA.**
4. **Dedicated Interconnect:** This option allows for one or more direct, private connections to Google
- This is covered 99.99% by an SLA **Service Level Agreement**
- Also, these connections can be backed up by a VPN for even greater reliability.
5. **Partner Interconnect:** which provides connectivity between an on-premises network and a VPC network through a supported service provider. 
- A Partner Interconnect connection is useful if a data center is in a physical location that can't reach a Dedicated Interconnect colocation facility,
- Useful  if the data needs don’t warrant an entire 10 GigaBytes per second connection.
- Can be configured to support mission-critical services or applications that can tolerate some downtime.
- Covered by an SLA of up to 99.99%
6. **Cross-Cloud Interconnect**: Establish high-bandwidth dedicated connectivity between Google Cloud and another cloud service provider.
- Google provisions a dedicated physical connection between the Google network and that of another cloud service provider (AWS).
- Cross-Cloud Interconnect supports your adoption of an integrated multicloud strategy.
- Supporting various cloud service providers, Cross-Cloud Interconnect offers reduced complexity, site-to-site data transfer, and encryption.

- **Connection Type:** Dedicated Interconnect provides a physical, high-capacity, private connection, whereas peering leverages existing networks to access Google services.
- **Performance and Reliability:** Dedicated Interconnect offers higher performance and reliability for critical applications, whereas peering is more economical and convenient for general service access.
- **Infrastructure Requirements:** Dedicated Interconnect requires specific setup at Google locations, while peering can be established without physical network integration.

---

# 4. Storage in Cloud

Every application needs to store data, like **media to be streamed** or perhaps even **sensor data** from devices, and different applications and workloads require different storage database solutions.

## 4.1 Google Cloud has storage options

**Five core storage products:**

1. Cloud Storage
2. Cloud SQL, 
3. Spanner
4. Firestore (Firebase: NoSQL document based)
5. Bigtable

You may have noticed that BigQuery hasn’t been mentioned in this section of the core products. This is because it sits on the edge between **data storage and data processing**, and is covered in more depth in other courses.

**Google Cloud storage options:**

**1. Unstructured Data:** 

- **Cloud Storage** (Object storage for images, videos, backups, logs, etc.)

**2. Structured Data:**

- **Cloud SQL** (Managed relational databases: MySQL, PostgreSQL, SQL Server)
- **Cloud Spanner** (Relational, distributed SQL database for global scalability)
- **Bigtable** (NoSQL wide-column store, optimized for time-series & big data)
- **BigQuery** (Serverless, columnar data warehouse with SQL support, optimized for analytics)

**3. Transactional Data:**

- **Cloud SQL** (Best for traditional relational transactions, OLTP workloads)
- **Cloud Spanner** (Distributed relational transactions, strong consistency, high availability)
- **Firestore** (NoSQL document-based database for real-time apps, strong consistency)

**4. Relational Data:**

- **Cloud SQL** (Traditional relational database management system)
- **Cloud Spanner** (Relational but horizontally scalable across regions, supports strong consistency)

## **4.2 Cloud Storage:**

**Cloud Storage is Google’s object storage product.** It allows customers to 

- Store any amount of data, and to retrieve it as often as needed.
- Fully managed scalable service that has a wide variety of uses.

**But what is object storage?** 

Object storage is a computer data storage architecture that manages data as “objects” and not as a file and folder hierarchy (file storage), or as chunks of a disk (block storage). 

These objects are stored in a **packaged format** which contains the **binary form** of the actual data itself, as well as relevant associated **meta-data** (such as date created, author, resource type, and permissions), and a 

**globally unique identifier**. These unique keys are in the form of URLs, which means object storage interacts well with web technologies. Data commonly stored as objects include video, pictures, and audio recordings. **Cloud Storage is Google’s object storage product.**

**Cloud Storage is a fully managed scalable service:**

![image.png](attachment:30943ff3-7fde-4ee2-99f4-4d1976ae7cf2:image.png)

**Cloud Storage’s primary use are:**

1. Archival & disaster recovery: Binary large-object storage (also known as a “BLOB”) 
2. Website content: Online content such as videos and photos providing direct download
3. Backup and archived data,
4. Storage of intermediate results in processing workflows.

**Cloud Storage files are organized into buckets**

![image.png](attachment:78424be4-57c3-44e9-b26b-9b9942011916:image.png)

A bucket needs a globally unique identifier and a specific geographic location for where it should be stored, and an ideal location for a bucket is where latency is minimized. For example, if most of your users are in Europe, you probably want to pick a European location, so either a specific Google Cloud region in Europe, or else the EU multi-region.

The storage objects offered by Cloud Storage are **immutable**, which means that you do not edit them, but instead **a new version is created with every change made**.

Administrators have the option to either allow each new version to completely overwrite the older one, or to keep track of each change made to a particular object by **enabling “versioning”** within a bucket.

**Versioning Default Disabled for Bucket:** If you don’t turn on object versioning, **by default** new versions will always overwrite older versions.

**Using IAM roles** and, where needed, **access control lists (ACLs)**, organizations can conform to security best practices, which require each

user to have access and permissions to only the resources they need to do their jobs, and no more than that.

There are a couple of options to control user access to objects and buckets.

- **IAM:** For most purposes, IAM is sufficient. Roles are inherited from project to bucket to object.
- **ACL (Access Control List) (similar with Linux):** If you need finer control, you can create access control lists. Each access control list consists of two pieces of information.
    - **Scope:** which defines who can access and perform an action. This can be a specific USER or GROUP
    - **Permission:** which defines what actions can be performed, like read or write.

![image.png](attachment:87250376-b394-4854-ae2d-c328524feaff:image.png)

Cloud Storage also offers **lifecycle management policies** for your objects. For example, you could tell Cloud Storage to delete objects older than 365 days, or to delete objects created before January 1, 2013, or to keep only the 3 most recent versions of each object in a bucket that has versioning enabled. We’ll look more
closely at object lifecycle management in just a few minutes.

**Lifecycle management policies save money:**

Because storing and retrieving large amounts of object data can quickly become expensive, Cloud Storage also offers lifecycle management policies. For example, you could tell Cloud Storage to delete objects older than 365 days, or to delete objects created before January 1, 2013; or to keep only the 3 most recent  versions of each object in a bucket that has versioning enabled. Having this control ensures that you
are not paying for more than you actually need. 

## 4.3 Cloud Storage: Storage classes and data transfer

![image.png](attachment:bf8f2472-6de2-469a-af7b-85907887d8a7:image.png)

- **Standard Storage** - Hot data
- N**earline Storage** - Once per month
- **Coldline Storage** - Once every 90 days
- **Archive Storage** - Once a year

![image.png](attachment:804ea077-d843-437b-b88c-69902bff1cad:image.png)

All storage classes includes:

- Unlimited storage (no min object size)
- Worldwide accessibility and locations
- Low latency and high durability
- A uniform experience (which extends to security, tools, and APIs)
- Geo-redundancy
- Autoclass: Automatically transitions objects to appropriate storage classes based on each object’s access pattern

**Autoclass:** The feature moves data that is not accessed to colder storage classes to reduce storage cost and moves data that is accessed to Standard storage to optimize future accesses. Autoclass simplifies and automates cost saving for your Cloud Storage data.

![image.png](attachment:79dfe53c-d220-43c1-90f1-abf24274a514:image.png)

Cloud Storage has no minimum fee because **you pay only for what you use**, and prior provisioning of capacity isn’t necessary.

Cloud Storage always encrypts data on the server side, before it’s written to disk, at no additional charge. Data traveling between a
customer’s device and Google is encrypted by default using HTTPS/TLS (Transport
Layer Security).

**Bringing data into Cloud Storage:**

![image.png](attachment:2fd18be2-4a81-4e4b-8a78-7a5a9630fa9e:image.png)

- **gcloud** storage, which is the Cloud Storage command from the **Cloud SDK.**
- **drag an drop in the Cloud Console:** if accessed through the Google Chrome web browser.
- **Storage Transfer Service** enables you to import large amounts of online data into Cloud Storage quickly and cost-effectively. The Storage Transfer Service lets you schedule and manage batch transfers to Cloud Storage from another cloud provider, from a different Cloud Storage region, or from an HTTP(S) endpoint.
- **Transfer Appliance,** which is a **rackable**, high-capacity storage server that you lease from Google Cloud.

**Cloud Storage can also be used like a file system:**

Although Cloud Storage is not a file system, it can be accessed as one via third-party tools that can **“mount” the bucket** and allow it to be used as if it were a typical Linux or MacOS directory.

**Integration with other Google Cloud products:**

Cloud Storage’s tight integration with other Google Cloud products and services means that there are many additional ways to move data into the service. For example, you can import and export tables to and from both BigQuery and Cloud SQL. You can also store App Engine logs, Firestore backups, and objects used by App Engine applications like images. Cloud Storage can also store instance startup scripts, Compute Engine images, and objects used by Compute Engine applications.

## 4.4 Cloud SQL

![image.png](attachment:fa629267-1c8e-49a7-8410-ddbe4a122959:image.png)

Cloud SQL offers fully managed relational databases, including **MySQL, PostgreSQL, and SQL Server** as a service. It’s designed to hand off mundane, but necessary and often time-consuming, tasks to Google—like applying patches and updates, managing backups, and configuring replications—so your focus can be on building great applications.

- Cloud SQL doesn't require any software installation or maintenance.
- It can scale up to **128 processor cores, 864 GB of RAM, and 64 TB of storage.**
- It **supports automatic replication** scenarios, such as from a Cloud SQL primary instance, an external primary instance, and external MySQL instances.
- Cloud SQL **supports managed backups**, so backed-up data is securely stored and accessible if a restore is required.
    - The cost of an instance covers seven backups.
- Cloud SQL **encrypts** customer data when on Google’s internal networks and when stored in database tables, temporary files, and backups.
- A benefit of Cloud SQL instances is that they are a**ccessible by other Google Cloud services,** and even external services.
- Cloud SQL can be used with **App Engine** using standard drivers like Connector/J for Java or MySQL db for Python.
- **Compute Engine instances** can be authorized to access Cloud SQL instances and configure the Cloud SQL instance to be in the same zone as your virtual machine.
- Cloud SQL also supports other applications and tools that you might use, like **SQL Workbench, Toad**, and other external applications using standard MySQL drivers.

## 4.5 Spanner

Spanner is a fully managed relational database service that scales horizontally, is strongly consistent, and speaks SQL.

![image.png](attachment:61a44918-1e36-43b5-8f6e-61ece08e2831:image.png)

- SQL relational database management system with joins and secondary indexes,
- Built-in high availability,
- Strong global consistency,
- High numbers of input and output operations per second.

## 4.6 Firestore

Firestore is a flexible, horizontally scalable, **document based NoSQL** cloud database for mobile, web, and server development.

![image.png](attachment:8ea77c9d-82cd-40b4-8e6b-b501e1affe16:image.png)

- Document based databases uses **Collections** for organizing documents which maps:
    - Collections=Table,
    - Document=Row
- Documents can contain c**omplex nested objects** in addition to subcollections.
- Firestore’s **NoSQL** queries can then be used to retrieve individual, specific documents or to retrieve all the documents in a collection that match your query parameters.

![image.png](attachment:6e5e2682-6969-4a16-ae37-0e750f5b8f19:image.png)

- Firestore uses data synchronization to update data on any connected device.
- However, it's also designed to make simple, one-time fetch queries efficiently.
- It caches data that an app is actively using, so the app can write, read, listen to, and query data even if the device is offline. When the device comes back online, Firestore synchronizes any local changes back to Firestore.
- Firestore leverages Google Cloud’s powerful infrastructure:
    - automatic multi-region data replication,
    - strong consistency guarantees,
    - atomic batch operations, and
    - real transaction support.

## 4.7 Bigtable

Bigtable is Google's **NoSQL** big data database service.

When deciding which storage option is best, customers often choose Bigtable if: 

- They’re working with **more than 1TB** of semi-structured or structured data.
- Data is fast with **high throughput**, or it’s rapidly changing.
- They’re working with **NoSQL data**. (This usually means transactions where strong relational semantics are not required.)
- Data is a **time-series** or has natural semantic ordering.
- They’re working with big data, running **asynchronous batch or synchronous real-time** processing on the data.
- they’re running machine learning algorithms on the data.

**Bigtable can interact with other Google Cloud services and third-party clients:**

![image.png](attachment:db99d288-efc5-4a1e-98d2-c19aeae5236e:image.png)

- Using APIs, data can be read from and written to Bigtable through a data service
- Examples: layer like Managed VMs, the HBase REST Server, or a Java Server using the HBase client.
- Typically this is used to **serve data to applications**, **dashboards, and data services.**

Data can also be streamed in through a variety of popular stream processing frameworks like 

- Dataflow Streaming,
- Spark Streaming, and
- Storm.

And if streaming is not an option, data can also be read from and written to Bigtable through batch processes like 

- Hadoop MapReduce,
- Dataflow, or
- Spark.

## 4.8 Comparing storage options

![image.png](attachment:d6544a25-d290-4d69-a36a-d0f7c3b2d4a2:image.png)

- Consider using **Cloud Storage** if you need to store **immutable blobs larger than 10 megabytes**, such as large images or movies. This storage service provides petabytes of capacity with a maximum unit size of 5 terabytes per object.
- Consider using **Cloud SQL or Spanner** if you need full **SQL support for an online transaction** processing system. Cloud SQL provides up to 64 terabytes, depending on machine type, and Spanner provides petabytes. Cloud SQL is best for web frameworks and existing applications, like storing user credentials and customer orders.
- If Cloud SQL doesn’t fit your requirements because you **need horizontal scalability,** not just through read replicas, **consider using Spanner**.
- **Consider Firestore** if you need **massive scaling** and predictability together **with real time query results** and offline query support. This storage service provides terabytes of capacity with a maximum unit size of 1 megabyte per entity. Firestore is best for storing, syncing, and querying data for mobile and web apps.
- Finally, consider using **Bigtable** if you **need to store a large number of structured objects**. Bigtable doesn’t support SQL queries, nor does it support multi-row transactions.

---

# 5. Containers in the Cloud

**Containers help applications scale easily (like PaaS) while also hiding OS and hardware details (like IaaS).**

- Containers allow applications to **scale independently** (like PaaS, where each service can grow as needed).
- Containers also **abstract (hide) the OS and hardware** details (like in IaaS, where you don’t worry about the underlying infrastructure).

**You can install and configure everything as you like—runtime, web server, database, and system resources**.

- You can **customize** your system by installing what you need (**runtime, web server, database, etc.**).
- You can **adjust resources** like **disk space, speed (I/O), and networking**.
- You have **full control** over how your system is built.

**Virtual Machines (VMs) Have Overhead**

- **VMs include a full guest OS**, which can be **large (gigabytes in size)** and take **minutes to boot**.
- Scaling an app with VMs means **copying the entire VM and booting the guest OS** each time, which can be **slow and costly**.

**Containers Are Lightweight & Fast**

- A **container is just an isolated environment** running on the **same OS kernel** as the host.
- It **starts in seconds** (like a regular process), instead of minutes.
- **Containers don’t need a full OS**—they only package the app and its dependencies.

**Why Containers Are Better for Scalability**

- They **scale like PaaS** (fast, independent scaling of workloads).
- They **offer flexibility like IaaS** (you can install what you need).
- They **make code portable**, so you can move an app between **development, staging, production, or the cloud without modification**.

VMs are heavy for autoscaling, require large disk space and long booting/startup process

- Invisible box around your code and its dependencies
- Has limited access to its own host partition of the host file system and hardware
- Only requires a few system calls to create and starts as quick as a process
- Only needs an OS kernel that supports containers and a container runtime, on each host

It scales like PaaS but gives you nearly the same flexibility as IaaS.

This makes code ultra portable, and the OS and hardware can be treated as a black box.

With a container, you can do this in seconds and deploy dozens or hundreds of them, depending on the size of your workload, on a single host.

## 5.1 Kubernetes

**What is Kubernetes?**

Kubernetes is an **open-source tool** that helps manage **containers** (like Docker) on **multiple machines**.

Kubernetes is a tool that makes it easy to run, scale, and manage containers across multiple machines (VMs, Compute Engine VM). It automates deployment, scaling, and updates so you don’t have to manage everything manually.

**Why is it useful?**

- It **automates** running and managing containers.
- It helps **scale** apps easily (add or remove containers as needed).
- It allows **smooth updates** (deploy new versions, roll back if needed).

**How does Kubernetes work?**

- **It uses APIs** to deploy and manage containers.
- **It groups machines (Compute Engine VMs) into a “cluster”** to run the containers.
- The system has **two main parts**:
    1. **Control Plane** (Controller)→ Manages the cluster and decides where to run containers.
    2. **Nodes** → Machines (Compute Engine VMs) that actually run the containers.

```jsx
+--------------------------------------------------+
|                Kubernetes Cluster               |
|  (A group of Virtual Machines running containers) |
+--------------------------------------------------+
         |                 |                 |
   +------------+    +------------+    +------------+
   |   Node 1   |    |   Node 2   |    |   Node 3   |   <-- Nodes = Compute Engine VMs
   | (VM in GCP)|    | (VM in GCP)|    | (VM in GCP)|
   +------------+    +------------+    +------------+
         |                 |                 |
  +--------+  +--------+   +--------+  +--------+ 
  | Pod A  |  | Pod B  |   | Pod C  |  | Pod D  |    <-- Multiple Pods per Node
  |--------|  |--------|   |--------|  |--------|
  |Container| |Container|  |Container| |Container|
  |   App   | |   App   |  |   App   | |   App   |    <-- Containers inside Pods
  +--------+  +--------+   +--------+  +--------+
```

The **Control Plane** is the **brain** of Kubernetes. It manages everything in the cluster, including scheduling Pods, monitoring health, and scaling resources.

A **Kubernetes Cluster** usually has **one logical Control Plane**, but: Every Kubernetes Cluster has one logical Control Plane.

✅ In a **basic setup**, there is **only one Control Plane node** (single master).

✅ In a **high-availability (HA) setup**, multiple Control Plane nodes **work together** for redundancy.

**High-Availability Cluster (Multiple Control Plane Nodes):**

```jsx
+--------------------------------------------------+
|             Kubernetes Cluster                  |
+--------------------------------------------------+
|   Control Plane (Multiple Nodes)                |  <-- HA: 3 Control Plane Nodes
|   - API Server                                  |
|   - Scheduler                                   |
|   - Controller Manager                          |
|   - etcd (Cluster State Database, replicated)   |
+--------------------------------------------------+
         |                 |                 |
   +------------+    +------------+    +------------+
   |   Node 1   |    |   Node 2   |    |   Node 3   |   <-- Worker Nodes (VMs)
   +------------+    +------------+    +------------+
         |                 |                 |
     +--------+        +--------+        +--------+
     | Pod A  |        | Pod B  |        | Pod C  |    <-- Pods (Containers)
     +--------+        +--------+        +--------+
```

Pods: The Pod provides a unique network IP and set of ports for your containers and configurable options that govern how your containers should run.

![image.png](attachment:fda735f1-3e26-4f64-b588-9de5e9b7142f:image.png)

There are only two steps for deploying docker container in Kubernetes, for example nginx blog pages

1. ConfigMap (Optinal) - blog-config.yml: Stores HTML content for the blog (or mount from a volume instead) (or keep static htmls in the container)
2. Deployment- nginx-deployment.yml : defines the Nginx pod and container
    
    `kubectl apply -f nginx-deployment.yml`
    
3. Service - nginx-service.yml: Creates service to expose Nginx inside the cluster
    
    `kubectl apply -f nginx-service.yml`
    
4. Ingress (Optional) - nginx-ingress.yml: If you need a public domain name, use an Ingress 

**kubectl:**  One way to run a container in a Pod in Kubernetes is to use the kubectl run command, which starts a Deployment with a container running inside a Pod.

Kubernetes **creates a Service with a fixed IP address for your Pods**, and a controller says:

*"I need to attach an external load balancer with a public IP address to that Service so others outside the cluster can access it."*

A Service is an abstraction which defines a logical set of Pods and a policy by which to access them.

```bash
# list of running pods
$ kubectl get pods

$ kubectl expose doployments nginx --port=80 --type=LoadBalancer
```

**Kubernetes assigns a fixed internal IP to a Service**, which helps other components in the cluster communicate with a group of Pods.

- Deployments manage Pods, and Pods can be replaced over time.
    - Each time a Pod is created, it gets a **new** IP address.
    - However, **the Service keeps a fixed IP** so that other applications (e.g., frontend) don’t have to keep track of changing Pod IPs.
        
        Example: A frontend Service needs to talk to a backend Service. The backend Service ensures that even if backend Pods are replaced, frontend Pods can still reach it using the same Service name/IP.
        
    - Scaling a Deployment `kubectl scale deployment my-app --replicas=3` (or you can define it in deployment.yml file)
        - Kubernetes automatically places these Pods **behind the same Service**.
        - Autoscaling can be configured to increase the number of Pods when CPU usage gets too high.

Kubernetes **gradually replaces old Pods with new ones** to avoid breaking the application. You can **update your Deployment file and reapply**:
`kubectl apply -f deployment.yml` or `kubectl rollout restart deployment my-app`

**If you want external access**, Kubernetes can attach a **Load Balancer** with a **public IP** to the Service. Service IP is not a public IP address Load Balancer always required for external access.

**In Google Kubernetes Engine (GKE), this is a Network Load Balancer**, which ensures that external clients can reach the application running inside the cluster.

The Load Balancer **routes traffic to the correct Pod behind the Service**.

The real strength of Kubernetes comes when you work in a declarative way. (imperative way is execute kubectl commands)

In **Docker Compose**, you only need **one file (docker-compose.yml)** to define everything. In **Kubernetes**, you typically need **separate YAML files** for **Deployment**, **Service**, and **Volumes**.

## 5.2 Google Kubernetes Engine

GKE is a Google-hosted managed Kubernetes service in the cloud. 

The GKE environment consists of multiple machines, specifically Compute Engine instances, grouped together to form a cluster.

**How is GKE different from Kubernetes?**

GKE manages all the control plane components for us.  GKE takes responsibility for provisioning and managing all the control plane infrastructure behind it.

![image.png](attachment:4c1ea122-cab5-4527-a37c-c6b145cff187:image.png)

**Autopilot mode:** which is recommended, GKE manages the underlying infrastructure such as node configuration, autoscaling, auto-upgrades, baseline security configurations, and baseline networking configuration.

- Autopilot is optimized for production.
- Autopilot also helps produce a strong security posture.
- Autopilot also promotes operational efficiency.

**Standard mode:** you manage the underlying infrastructure, including configuring the individual nodes.

You can create a Kubernetes cluster with Kubernetes Engine by using the Google Cloud console or the gcloud command that's provided by the Cloud SDK software development kit.

**Kubernetes commands and resources are used to** 

1. deploy and manage applications, 
2. perform administration tasks, 
3. set policies, 
4. monitor the health of deployed workloads.

`$> gcloud container clusters create k1`

**GKE Cluster comes with the benefit of:**

1. Advanced cluster management features 
2. Google Cloud's load-balancing for Compute Engine instances, (When you expose a service in GKE, Google Cloud automatically provides a highly available Load Balancer.)
3. Node pools to designate subsets of nodes within a cluster for additional flexibility, 
    1. You can create **groups of nodes (VMs)** with different configurations within the same cluster. One **node pool** could have high-memory machines for **database workloads**.
    2. Another **node pool** could have GPU-enabled nodes for **AI/ML applications**.
4. Automatic scaling of your cluster's node instance count, 
5. Automatic upgrades for your cluster's node software, 
6. Node auto-repair to maintain node health and availability, 
7. Logging and monitoring with Google Cloud Observability for visibility into your cluster.

---

# 6. Applications in the Cloud

## 6.1 Cloud Run

Managed compute platform that runs stateless **containers** via **web requests or Pub/Sub events**.

Cloud Run is an on-demand, fully managed container service.

**How Cloud Run Works:**

- **Containers are initiated on-demand.**
    - When a request comes in, Cloud Run **spins up a container instance** to handle it.
    - If no requests are incoming, Cloud Run can **scale down to zero**, meaning no running containers, saving costs.
- **It scales automatically** based on traffic.
    - If traffic increases, Cloud Run creates **more container instances** to handle the load.
    - When traffic decreases, instances **shut down automatically** to avoid unnecessary resource usage.

You can use a container-based workflow, as well as a source-based workflow.

- **Container-based workflow:**   you define your application environment using a container image. This provides maximum control over the environment because you can specify every aspect, including the operating system, dependencies, configurations, and more. Process:
    1. Build docker image, `gcloud builds submit --tag [gcr.io/$GOOGLE_CLOUD_PROJECT/helloworld](http://gcr.io/$GOOGLE_CLOUD_PROJECT/helloworld)`
    2. Configure Dockerfile (env variables), test it in cloud-shell: `docker run -d -p 8080:8080 [gcr.io/$GOOGLE_CLOUD_PROJECT/helloworld](http://gcr.io/$GOOGLE_CLOUD_PROJECT/helloworld)`
    3. Deploy container image to Cloud Run `gcloud run deploy --image [gcr.io/$GOOGLE_CLOUD_PROJECT/helloworld](http://gcr.io/$GOOGLE_CLOUD_PROJECT/helloworld) --allow-unauthenticated --region=$LOCATION`
        
        After some minutes it will give you Service URL: [`https://helloworld-h6cp412q3a-uc.a.run.app`](https://helloworld-h6cp412q3a-uc.a.run.app/)
        
- **Source-based workflow:** deploy applications directly from the source code without manually packaging them into containers. This workflow often involves automated tools that package the source code into container images behind the scenes. Process
    1. Write your code
    2. Continuous Integration: Google Cloud Build (**cloudbuild.yaml**)

The source-based approach will deploy source code instead of a container image.

Cloud Run then builds the source and packages the application into a container image.

Cloud Run does this using **Buildpacks** - an open source project.

**Is “Cloud Run” Always Running?**

No, unless you use Cloud Run Jobs or **enable minimum instances** (which keeps a few instances always running).
**By default,** Cloud Run follows a **serverless** model, where containers only run when needed and shut down when idle.

Knative, an open API and runtime environment built on Kubernetes. It can be fully managed on Google Cloud, on Google Kubernetes Engine, or anywhere Knative runs.

**📌 What is Knative? (Run time Kubernetes component)**

**Knative** is an open-source platform that adds **serverless capabilities** to Kubernetes.  It provides components to manage the lifecycle of containers, making it easier deploy, and manage modern serverless applications.

- It enables **automatic scaling**, including **scaling to zero** (when there are no requests).
- It simplifies **deploying, running, and managing containerized applications** on Kubernetes.
- Knative provides an API for deploying and managing serverless workloads.
- You can run Knative **anywhere**, even on **your own Kubernetes cluster** outside Google Cloud.

Since Knative runs **inside Kubernetes**, you can see and manage Knative services using **kubectl**: 

`kubectl get pods -n knative-serving`

`kubectl get services.serving.knative.dev`

If you deploy a Knative service using **Cloud Run for Anthos** (Knative on GKE) or run Knative on a self-managed **GKE cluster**, you will see your Knative containers inside Kubernetes.

•	✅ **With GKE:** You **see** and control Knative in Kubernetes. **You manually install and configure Knative on GKE. Knative could use other containers**

•	✅ **With Cloud Run for Anthos:** You get Knative, but Google manages Kubernetes for you. **Knative could use other containers**

•	❌ **With Cloud Run (Fully Managed):** Knative runs behind the scenes, but you don’t manage Kubernetes directly.

Containers running inside **Cloud Run for Anthos** **can communicate** with each other, just like in Kubernetes.

•	Since Cloud Run for Anthos runs **on GKE**, containers can talk to each other using **Kubernetes networking**.

![image.png](attachment:20880e32-fb72-4042-85a1-4e50bd7773ec:image.png)

Once you’ve deployed your container image, you’ll get a unique HTTPS URL back. 

Cloud Run then starts your container on demand to handle requests, and ensures that all incoming requests are handled by dynamically adding and removing containers.

- For some use cases, a container-based workflow is great, because it gives you a great amount of transparency and flexibility.
- Sometimes, you’re just looking for a way to turn source code into an HTTPS endpoint, and you

With Cloud Run, you can do both.

- You can use a container-based workflow, as well as a source-based workflow.
- The source-based approach will deploy source code instead of a container image.

## 6.2 Development in the cloud

**Cloud Run Functions:** 

- lightweight, event-based, asynchronous compute solution
- allows you to create small, single-purpose functions that respond to cloud events, without the need to manage a server or a runtime environment.
- These functions can be used to **construct application workflows** from individual business logic **tasks**.
- Cloud Run functions can also connect and extend cloud services.
- You’re billed to the nearest 100 milliseconds, but only while your code is running.
- Cloud Functions could use “Cloud Logging” : Cloud Run functions is integrated with Google Cloud Observability logging and monitoring services to make it fully observable.
- These include
    - Node.js,
    - Python,
    - Go,
    - Java,
    - Net Core,
    - Ruby
    - PHP.

**Customers choose to use Cloud Run Functions because:** Their application contains event-driven code that they don't want to provision compute resources for.

- **Google Cloud API** is the set of functions accessible over HTTP requests.(create CloudRun remotely on the GCP using API interface)
- **Google Cloud Client Libraries** simplify working with APIs, adapting them into usable methods in programming languages.
- **Google Cloud SDK** contains the **command-line tools** and **utilities to manage cloud resources**, incorporating client libraries for code-level interaction.
- Everything ties back to interacting with Google Cloud APIs. While client libraries and clients are technically part of the SDK's offerings for programming environments conducive to integrating cloud services into applications.

---

# 7. Prompt Engineering

https://youtu.be/5zoKVf-cnf4

**Generative AI:** Is a **subset of artificial intelligence** that is capable of **creating text, images, or other data using generative models,** often in response to prompts.

- Google Cloud Console already contains Gemini
- Gemini is embedded in many Google Cloud products.

**Prompt Engineering:** 

- zero-shot,
- one-shot,
- few-shot,
- role prompts.

![image.png](attachment:c060d648-20f3-4f0e-a8a9-561011bb0ea0:image.png)

Prompt: 

- Preamble
    - Context
    - Instructions/task
    - Example
- input

Promp Engineering Best practices

- write detailed and explicit instructions.
- Be clear and concise in the prompts that you feed into the model.
- define boundaries for the prompt.
- It’s better to instruct the model on what to do rather than what not to do.
- to adopt a persona for your input.

**Multi cloud environment:** microservices could use different cloud platforms like AWS, Azure, GCP some applications run in multi cloud.