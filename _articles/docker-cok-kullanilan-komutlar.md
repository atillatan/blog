---
layout: article
permalink:
name:
file_type:
title: Docker most used commands
description: >-
  Docker most used commands
tags:  
category:  
sort_order: 30
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
# DOCKER



## Docker most used commands

- Docker components versions

```bash
$ docker --version
Docker version 1.12.3, build 6b644ec

$ docker-compose --version
docker-compose version 1.8.1, build 878cff1

```

### What is image? What is container?

Image is customized operating system images. There are a lot of images in docker hub: https://hub.docker.com
you can not run an image on your computer. if you want to run image on your computer, you have to create runnable instance of image which is called "Container"
so
Container is a runnable instance of an image. 

- There are few core operation system images in docker hub
- All other images derived from core os images for example some created wordpress images using core os images.
- If you want to create your own image you can create a "Dockerfile"


### docker image

- `docker image` shows help

```shell
docker image build       Build an image from a Dockerfile
docker image history     Show the history of an image
docker image import      Import the contents from a tarball to create a filesystem image
docker image inspect     Display detailed information on one or more images
docker image load        Load an image from a tar archive or STDIN
docker image ls          List images
docker image prune       Remove unused images
docker image pull        Pull an image or a repository from a registry
docker image push        Push an image or a repository to a registry
docker image rm          Remove one or more images
docker image save        Save one or more images to a tar archive (streamed to STDOUT by default)
docker image tag         Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE
```

### docker container

- `docker container` shows help

```shell
docker container attach      Attach local standard input, output, and error streams to a running container
docker container commit      Create a new image from a container's changes
docker container cp          Copy files/folders between a container and the local filesystem
docker container create      Create a new container
docker container diff        Inspect changes to files or directories on a container's filesystem
docker container exec        Run a command in a running container
docker container export      Export a container's filesystem as a tar archive
docker container inspect     Display detailed information on one or more containers
docker container kill        Kill one or more running containers
docker container logs        Fetch the logs of a container
docker container ls          List containers
docker container pause       Pause all processes within one or more containers
docker container port        List port mappings or a specific mapping for the container
docker container prune       Remove all stopped containers
docker container rename      Rename a container
docker container restart     Restart one or more containers
docker container rm          Remove one or more containers
docker container run         Run a command in a new container
docker container start       Start one or more stopped containers
docker container stats       Display a live stream of container(s) resource usage statistics
docker container stop        Stop one or more running containers
docker container top         Display the running processes of a container
docker container unpause     Unpause all processes within one or more containers
docker container update      Update configuration of one or more containers
docker container wait        Block until one or more containers stop, then print their exit codes
```


### Build an image from a Dockerfile


- `docker build --help` shows help

```shell
Usage:  docker build [OPTIONS] PATH | URL | -

docker build  --add-host list           Add a custom host-to-IP mapping (host:ip)
docker build  --build-arg list          Set build-time variables
docker build  --cache-from strings      Images to consider as cache sources
docker build  --disable-content-trust   Skip image verification (default true)
docker build  -f, --file string             Name of the Dockerfile (Default is 'PATH/Dockerfile')
docker build  --iidfile string          Write the image ID to the file
docker build  --isolation string        Container isolation technology
docker build  --label list              Set metadata for an image
docker build  --network string          Set the networking mode for the RUN instructions during build (default "default")
docker build  --no-cache                Do not use cache when building the image
docker build  -o, --output stringArray      Output destination (format: type=local,dest=path)
docker build  --platform string         Set platform if server is multi-platform capable
docker build  --progress string         Set type of progress output (auto, plain, tty). Use plain to show container output (default docker build"auto")
docker build  --pull                    Always attempt to pull a newer version of the image
docker build  -q, --quiet                   Suppress the build output and print image ID on success
docker build  --secret stringArray      Secret file to expose to the build (only if BuildKit enabled): id=mysecret,src=/local/secret
docker build  --ssh stringArray         SSH agent socket or keys to expose to the build (only if BuildKit enabled) (format: default|<id>docker build[=<socket>|<key>[,<key>]])
docker build  -t, --tag list                Name and optionally a tag in the 'name:tag' format
docker build  --target string           Set the target build stage to build.

```

When you build your images add “–rm” this should help with removing any intermediate and none images.

```shell
docker build --rm
```


### Download an image


```shell
$ docker pull alpine
```

### Create a Container

You can create container using `docker run` command

```shell
docker run --help

Usage:  docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
```

Example:

```shell
docker run -ti --detach --name alpine1 --hostname alpine1 alpine /bin/sh
```
-d, --detach : Run container in background and print container ID
--name : Assign a name to the container
--hostname : Container host name
-t, -tty : Allocate a pseudo-TTY
-i, --interactive : Keep STDIN open even if not attached
-p, --publish list : Publish a container's port(s) to the host

/bin/sh : a command it'll execute in instance.

### Networking 

```bash
Usage:  docker network COMMAND

Manage networks

Commands:

$ docker network connect    : Connect a container to a network
$ docker network create     : Create a network
$ docker network disconnect : Disconnect a container from a network
$ docker network inspect    : Display detailed information on one or more networks
$ docker network ls         : List networks
$ docker network prune      : Remove all unused networks
$ docker network rm         : Remove one or more networks
```

`docker network inspect bridge` returns a JSON object describing the bridge network

Example:

`docker network custom1` create network
`docker network ls` show list of networks
`docker network connect <network name> <container name>` connect your container to the custom network



- `docker run -d -p 80:80 --name webserver nginx`  creates a container using nginx Docker image.  
 `-p 80:80` indicates published ports, `<host port>:<container port>` 
 `--name <container name>` : container name
#### How do I run a command in my container?
  - Use `docker container ls` to get the name of the existing container
  - `docker exec ...` execute command in docker container
  - Use the command `docker exec -it <container name> /bin/bash`, `docker exec -it <container name> sh` to get a bash shell in the container
  - Generically, use `docker exec -it <container name> <command>` to execute whatever command you specify in the container.


#### Sharing volume between Docker containers
  - Create a named data volume with name service-data:
`docker volume create --name service-data`
  - You can then create a container that mounts it in your /public folder by using the -v flag:
`docker run -t -i -v service-data:/public debian:jessie /bin/bash`
  - For testing purpose we create a small text file in our mapped folder:

```shell
cd public
echo 'hello' > 'hello.txt'
```
You may then attach your named volume to a second container, but this time under the data folder:

`docker run -t -i -v service-data:/data debian:jessie /bin/bash`
`ls /data`       #-->shows "hello.txt"


#### Mounting files directly

```bash
docker run --name nginx-container \
  -v /path/to/static/files/on/host:/usr/share/nginx/html:ro \
  -v /path/to/conf/on/host:/etc/nginx/nginx.conf:ro \
  -P -d nginx
```

or 

```bash
docker run --name nginx-container \
  -v $(pwd)/html:/usr/share/nginx/html:ro \
  -v $(pwd)/nginx.conf:/etc/nginx/nginx.conf:ro \
  -P -d nginx
```

- show logs interactively `-it`

```bash
docker run -it --name nginx-container \
  -v $(pwd)/html:/usr/share/nginx/html:ro \
  -v $(pwd)/nginx.conf:/etc/nginx/nginx.conf:ro \
  -P nginx bash
```

#### create nginx docker service in for steps.

1. Create dockerfile

```bash
FROM nginx
VOLUME /usr/share/nginx/html
VOLUME /etc/nginx
```

2. `docker build -t <nginx image name> .`  
3. 
```shell
docker run -it --name <container name> \
  -v $(pwd)/src:/usr/share/nginx/html:ro \
  -v $(pwd)/nginx/nginx.conf:/etc/nginx/nginx.conf:ro \
  -P -d <nginx image name>`  
```
:ro --> read only

example 2

```shell
docker run -it --name wiki1 -p 8181:80 \
  -v /Users/atilla/WP/usiswiki/src/:/usr/share/nginx/html/ \
  -v /Users/atilla/WP/usiswiki/nginx/nginx.conf:/etc/nginx/nginx.conf:ro \
  -P -d usiswikiimage
```

4. start your container

```bash
docker start usiswikicontainer
docker stop usiswikicontainer
```
 
- create Mysql container
`docker run --name mysqlc1 -p 3306:3306 -e MYSQL_ROOT_PASSWORD=123 -d mysql`

`-e or --env list` : Set environment variables

#### Docker attach
attach provides connecting directly running process

```shell
$ docker attach alpine1
```

### Some Examples


- Create postgresql container from 'postgres' image and create table

```shell

$ docker pull postgres 
$ docker run --name postgres1 -p 5432:5432 -e POSTGRES_PASSWORD=123 -d postgres
$ docker ps
$ docker exec -it postgres1 bash $ su postgres
$ psql
$ DROP TABLE IF EXISTS trades;
$ CREATE TABLE Trade(id serial PRIMARY KEY, tradeId VARCHAR(255), version
integer, counterparty VARCHAR(255), bookid VARCHAR(255),maturityDate DATE,
createddate DATE, expiredFlag VARCHAR(255));

```

- Create pgadmin container from 'dpage/pgadmin4' docker image

```shell
$ docker pull dpage/pgadmin4
$ docker run -p 80:80 --name pgadmin1 --hostname pgadmin1  -e 'PGADMIN_DEFAULT_EMAIL=atilla@admin.com' -e 'PGADMIN_DEFAULT_PASSWORD=123' -d dpage/pgadmin4
```


#### Docker compose examples

```yml
version: '3.9'

services:
  postgres:
    image: postgres
    container_name: postgres1
    environment:
      - POSTGRES_USER=postgres
      - POSTGRES_PASSWORD=123
      - POSTGRES_DB=Trade
    ports:
      - 5432:5432
 
  pgadmin:
    image: dpage/pgadmin4
    container_name: pgadmin1    
    environment:
      - PGADMIN_DEFAULT_EMAIL=atilla@admin.com
      - PGADMIN_DEFAULT_PASSWORD=123
    ports:
      - 80:80
    links:
      - postgres

  kafka:
    build: resources/kafka-with-zookeeper/
    container_name: kafka
    ports: 
      - 2181:2181
      - 9092:9092
      - 9093:9093
      - 9094:9094
    # links:
    #   - zookeeper
    environment: 
      - ZOOKEEPER_CONNECT=zookeeper:2181
ss
  producer:
    build: src/producer/
    container_name: producer
    ports: 
      - 8081:8081
    links:
      - kafka

  consumer:
    build: src/consumer/
    container_name: consumer
    ports: 
      - 8082:8082
    links:
      - kafka
      - postgres
```