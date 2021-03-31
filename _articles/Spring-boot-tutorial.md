---
layout: article
permalink: 
name: 
file_type: 
title: Spring Boot Tutorial
description: >-
  Spring Boot Tutorial
tags:  java
category:  
sort_order: 200
rating: 10
changefreq: monthly
priority: 0.5
published: true
create_date: 2021-01-23
modified_date: 2021-01-23
created_by: atilla
modified_by: atilla
comments: true
redirect_url: 
toc: false
---

# Spring Boot Tutorial


Spring Boot is an open-source Java-based application development framework mostly used to create a microservice.

**Spring boot:** 

- Includes Embedded Servlet Container
- Provides Rapid Application Development (RAD)
- Reduces the development time
- Increases productivity
- Decreases complexity
- Compatible with Containers
- Simple scalability
- Easy deployment
- Everything is auto-configured by annotations
- Eases dependency management

**Spring:**  The main feature of the Spring Framework is DI (Dependency Injection) or IoC (Inversion of Control). We can develop a loosely coupled application. 

**Spring Boot:** Is a module of Spring Framework. It allows you to build a stand-alone application with minimal configurations, 

- Widely used to develop REST APIs.
- The primary feature of Spring Boot is Autoconfiguration. It automatically configures the classes based on the requirement.
- It helps to create stand-alone microservices with less configuration.
- It reduces boilerplate code. increase modularity, reusability.
- It has an embedded server (Tomcat, Jetty)



**Spring MVC:** is a Web MVC Framework for building web applications. It is another module of Spring like Spring Boot. 

Spring Boot uses all the modules of Spring, like Spring MVC, Spring Data, etc. The architecture of Spring Boot is the same as the architecture of Spring MVC, except one thing: there is no need for **DAO** and **DAOImpl** classes in Spring boot.

**Architecture of Spring Boot:** Spring Boot has layered architecture. There are four layers in Spring Boot

- **Presentation Layer :** Authentication, JSON translation
  - The presentation layer handles the HTTP requests, translates the JSON parameter to object, and authenticates the request and transfer it to the business layer. In short, it consists of **views** i.e., frontend part.
- **Business/Service Layer :** Business/Service Logic, Validation, Authorisation
  - The business layer handles all the **business logic**. It consists of service classes and uses services provided by data access layers. It also performs **authorization** and **validation**.
- **Persistence Layer:** Storage Logic (DTO to and from Data Model)
  - The persistence layer contains all the **storage logic** and translates business objects from and to database rows.
- **Database Layer:** Actual Database
  - In the database layer, **CRUD** (create, retrieve, update, delete) operations are performed.





## Create a Spring Boot Project

**Spring Initializr:** is a web-based tool it helps creating spring projects.

- **initializr-actuator:**  It provides additional information and statistics on project generation. It is an optional module. promethous can collect data from actuator.
- **initializr-bom:** In Spring Boot, BOM is a special kind of **POM** that is used to control the **versions** of a project's **dependencies**.
- **initializr-docs:** It provides documentation.
- **initializr-generator:** It is a core project generation library.
- **initializr-generator-spring:**
- **initializr-generator-test:** It provides a test infrastructure for project generation.
- **initializr-metadata:** It provides metadata infrastructure for various aspects of the projects.
- **initializr-service-example:** It provides custom instances.
- **initializr-version-resolver:** It is an optional module to extract version numbers from an arbitrary POM.
- **initializr-web:** It provides web endpoints for third party clients.


london socials



Spring Boot automatically configures your application based on the dependencies you have added to the project by using **@EnableAutoConfiguration** annotation. 

**@SpringBootApplication:** The entry point class of the Spring Boot application. It is the class that has the main method. SpringBootApplication annotation includes Auto-Configuration, Component Scan, and Spring Boot Configuration. If you added **@SpringBootApplication** annotation to the class, you do not need to add the **@EnableAutoConfiguration, @ComponentScan** and **@SpringBootConfiguration**annotation. The **@SpringBootApplication** annotation includes all other annotations.

```java
@SpringBootApplication
public class ProducerApplication {	 
	public static void main(String[] args) {
		ApplicationContext context= SpringApplication.run(ProducerApplication.class, args);
	}
}

//equals

@EnableAutoConfiguration
@ComponentScan
@SpringBootConfiguration
public class ProducerApplication {	 
	public static void main(String[] args) {
		ApplicationContext context= SpringApplication.run(ProducerApplication.class, args);
	}
}

```

**Auto Configurations:** Spring Boot Auto Configuration automatically configures your Spring application based on the JAR dependencies you added in the project. For example, if MySQL database is on your class path, but you have not configured any database connection, then Spring Boot auto configures an in-memory database.

For this purpose, you need to add **@EnableAutoConfiguration** annotation or **@SpringBootApplication** annotation to your main class file. Then, your Spring Boot application will be automatically configured. 

**@ComponentScan**: Spring Boot automatically scans all the components included in the project by using ComponentScan annotation.It runs according to package declarations, you need to put your main class into root location, otherwise, you need to declare some additional annotations such as **@EntityScan("specific.package")**

**spring-boot-starter-***: All Spring Boot starters follow the same naming pattern for example spring-boot-starter-actuator, spring-boot-starter-jpa, etc.



### First RESTful service



```java
package spring.executable.executable;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@SpringBootApplication
@RestController
public class FirstApplication {

	public static void main(String[] args) {
		SpringApplication.run(FirstApplication.class, args);
	}

	@RequestMapping(value = "/hello")
	public String hello() {
		return "Hello World";
	}
}
```



```bash
$ mvn package
$ java -jar target/<jar-name>
```



Call service: `http://localhost:8080/hello`

**spring-boot-starter-parent:** dependency is the parent POM. It provides dependency and plugin management for Spring Boot applications. It contains the default versions of Java to use, The devault versions of dependencies that Spting Boot uses

**spring-boot-dependencies:** spring-boot-starter-parent inherits from spring-boot-dependencies. This file is the actual file which contains the information of default version to use for all libraries. 

inheritance: 

my-spring-project **<--** spring-boot-starter-parent **<--** spring-boot-dependencies

one of the spring boot dependency **<--** spring-boot-parent or spring-boot-starter

**Overriding default dependencies:** 

Default version of gson library is 2.8.2 

pom.xml: spring-boot-dependencies

```xml

<properties>
    <!-- Dependency versions -->
    <java.version>1.8</java.version>
  	<gson.version>2.8.2</gson.version>
    ...
</properties>
```

Overriding default version of gson library with 2.7

```xml
<properties>
    <java.version>1.8</java.version>
    <gson.version>2.7</gson.version>
  ...
</properties>
```


### Spring-boot-starter Maven Templates

Spring Boot comes with over 50+ different starter modules, which provide ready-to-use integration libraries for many different frameworks, such as database connections that are both relational and NoSQL, web services. 

Spring Boot starters are templates that contain a collection of all the relevant transitive dependencies that are needed to start a particular functionality.  Each starter has a special file, which contains the list of all the provided dependencies Spring provides. 
These files can be found inside pom.xml files in respective starter module.



| STARTER Templates                | DEPENDENCIES                                                 |
| -------------------------------- | ------------------------------------------------------------ |
| spring-boot-starter              | spring-boot, spring-context, spring-beans                    |
| spring-boot-starter-jersey       | jersey-container-servlet-core, jersey-container-servlet, jersey-server |
| spring-boot-starter-actuator     | spring-boot-actuator, micrometer-core                        |
| spring-boot-starter-aop          | spring-aop, aspectjrt, aspectjweaver                         |
| spring-boot-starter-data-rest    | spring-hateoas, spring-data-rest-webmvc                      |
| spring-boot-starter-hateoas      | spring-hateoas                                               |
| spring-boot-starter-logging      | logback-classic, jcl-over-slf4j, jul-to-slf4j                |
| spring-boot-starter-log4j2       | log4j2, log4j-slf4j-impl                                     |
| spring-boot-starter-security     | spring-security-web, spring-security-config                  |
| spring-boot-starter-test         | spring-test, spring-boot,junit,mockito, hamcrest-library, assertj, jsonassert, json-path |
| spring-boot-starter-web-services | spring-ws-core                                               |



###  Multi-module maven projects


**What are the benefits of multi-module projects in Spring Boot:**

- Provide the ability to build all module with a single command. Run the build command from parent module.
- Build system take care of the build order.
- Make it easy and flexible to deploy the application.
- You can re-use the code from the modules across different projects.



#### 1. Spring Boot Parent Module

To start with our spring boot multi-module project, the first step is to create a simple parent project. This parent module contains a `pom.xml` file and our `pom.xml` will have the following details:

1. List of all the modules (actual projects).
2. List of common dependencies across all modules (we need not duplicate it on all module).
3. Common configuration for all modules (e.g. java version etc.)

As part of the [Spring Boot](https://www.javadevjournal.com/spring-boot/) application, we will also add the [spring-boot-starter-parent](https://www.javadevjournal.com/spring-boot/spring-boot-starter-parent/) dependency. It is the parent POM providing dependency and plugin management for Spring Boot-based applications. This step is optional but highly recommended for Spring Boot application. To create the parent project, we have the following 2 options:

1. Create `pom.xml` manually.
2. Use maven quick-start archetype

```bash
mvn archetype:generate -DgroupId=com.javadevjournal
        -DartifactId=spring-boot-multi-module-project
        -DarchetypeArtifactId=maven-archetype-quickstart
        -DinteractiveMode=false
```



Once we run above command, Maven will create a structure for us along with the `pom.xml` file. Change the packaging type as pom for this parent module. This is how the final `pom.xml` look like.

Parent Module:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
   <modelVersion>4.0.0</modelVersion>
   <groupId>org.javadevjournal</groupId>
   <artifactId>spring-boot-multi-module-project</artifactId>
   <version>0.0.1-SNAPSHOT</version>
   <packaging>pom</packaging>
   <name>spring-boot-multi-module-project</name>
   <url>https://www.javadevjournal.com</url>
   <parent>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-parent</artifactId>
      <version>2.2.4.RELEASE</version>
   </parent>
   <properties>
      <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
      <maven.compiler.source>1.8</maven.compiler.source>
      <maven.compiler.target>1.8</maven.compiler.target>
      <java-version>1.8</java-version>
   </properties>
   <modules>
      <module>jdj-core</module>
      <module>jdj-web</module>
   </modules>
   <dependencies>
      <dependency>
         <groupId>org.springframework.boot</groupId>
         <artifactId>spring-boot-starter-test</artifactId>
         <scope>test</scope>
      </dependency>
      <dependency>
         <groupId>org.springframework.boot</groupId>
         <artifactId>spring-boot-starter</artifactId>
      </dependency>
   </dependencies>
</project>
```

In our `pom.xml` file, we are defining *spring-boot-starter* as the global dependency (as we need it in all module). We’ll create two directories inside our project. These 2 directories represents the sub-modules defined in the parent `pom.xml` file.

jdj-core, pom.xml:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
   <modelVersion>4.0.0</modelVersion>
   <parent>
      <groupId>org.javadevjournal</groupId>
      <artifactId>spring-boot-multi-module-project</artifactId>
      <version>0.0.1-SNAPSHOT</version>
   </parent>
   <groupId>com.javadevjournal</groupId>
   <artifactId>jdj-core</artifactId>
   <version>0.0.1-SNAPSHOT</version>
   <name>jdj-core</name>
   <description>Core module for our multi module Spring Boot application</description>
</project>
```



jdj-web, pom.xml:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
   <modelVersion>4.0.0</modelVersion>
   <parent>
      <groupId>org.javadevjournal</groupId>
      <artifactId>spring-boot-multi-module-project</artifactId>
      <version>0.0.1-SNAPSHOT</version>
   </parent>
   <groupId>com.javadevjournal</groupId>
   <artifactId>jdj-web</artifactId>
   <version>0.0.1-SNAPSHOT</version>
   <name>jdj-web</name>
   <description>Web module for our multi module Spring Boot application</description>
   <dependencies>
      <dependency>
         <groupId>org.springframework.boot</groupId>
         <artifactId>spring-boot-starter-web</artifactId>
      </dependency>
      <dependency>
         <groupId>com.javadevjournal</groupId>
         <artifactId>jdj-core</artifactId>
         <version>0.0.1-SNAPSHOT</version>
      </dependency>
   </dependencies>
   <build>
      <plugins>
         <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
         </plugin>
      </plugins>
      <finalName>javadev-web</finalName>
   </build>
</project>
```





### Annotations

`@SpringBootApplication` annotation enable all able things in one step. It enables the three features:

1. `@EnableAutoConfiguration` : enable auto-configuration mechanism
2. `@ComponentScan` : enable @Component scan
3. `@SpringBootConfiguration` : register extra beans in the context

**@ImportAutoConfiguration:** It import and apply only the specified auto-configuration classes. The difference between `@ImportAutoConfiguration` and `@EnableAutoConfiguration` is that later attempts to configure beans that are found in the classpath during scanning, whereas `@ImportAutoConfiguration` only runs the configuration classes that we provide in the annotation.

We should use `@ImportAutoConfiguration` when we don’t want to enable the default auto-configuration.



@ImportAutoConfiguration example:

```java
@ComponentScan("path.to.your.controllers")
@ImportAutoConfiguration({WebMvcAutoConfiguration.class
    ,DispatcherServletAutoConfiguration.class
    ,EmbeddedServletContainerAutoConfiguration.class
    ,ServerPropertiesAutoConfiguration.class
    ,HttpMessageConvertersAutoConfiguration.class})
public class App 
{
    public static void main(String[] args) 
    {
        SpringApplication.run(App.class, args);
    }
}
```



















- Referances:

https://www.javadevjournal.com/spring-boot/multi-module-project-with-spring-boot/

