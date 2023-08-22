- [Get Docker CE for Ubuntu](#get-docker-ce-for-ubuntu)
- [manage docker](#manage-docker)
- [Uninstall Docker CE](#uninstall-docker-ce)
- [images](#images)
  - [official images](#official-images)
  - [check images](#check-images)
  - [create image](#create-image)
  - [check history](#check-history)
  - [remove images](#remove-images)
- [containers](#containers)
  - [create a container](#create-a-container)
  - [remove container](#remove-container)
  - [logs](#logs)
  - [check docker process/containers](#check-docker-processcontainers)
  - [important commands](#important-commands)
  - [create ssl](#create-ssl)
  - [inspect](#inspect)
  - [run container's shell](#run-containers-shell)
  - [stats](#stats)
  - [copy files between host and container](#copy-files-between-host-and-container)
  - [commit](#commit)
  - [overwrite cmd](#overwrite-cmd)
  - [simple machine](#simple-machine)
  - [self-destructing containers](#self-destructing-containers)
  - [start one or more stopped containers](#start-one-or-more-stopped-containers)
- [volumes](#volumes)
  - [list volumes](#list-volumes)
  - [create volume](#create-volume)
  - [remove volume](#remove-volume)
  - [assgin volume to a container](#assgin-volume-to-a-container)
  - [Dangling volumes 😉](#dangling-volumes-)
- [networking](#networking)
  - [list networks](#list-networks)
  - [inspect](#inspect-1)
  - [create network](#create-network)
  - [connect container](#connect-container)
  - [disconnect network](#disconnect-network)
  - [delete network](#delete-network)
  - [ip assignment](#ip-assignment)
  - [host and none](#host-and-none)
- [Docker Compose](#docker-compose)
  - [install](#install)
  - [file](#file)
  - [manage](#manage)
  - [custom project name](#custom-project-name)
  - [logs](#logs-1)
- [registry](#registry)
  - [upload image](#upload-image)
  - [download image](#download-image)
  - [share registry](#share-registry)

# Get Docker CE for Ubuntu

- Just like docs 🤓, add the keys, repository, etc.
- install `sudo apt-get update && sudo apt-get install docker-ce`
- check version `docker --version`
- add user to docker group `sudo usermod -aG docker [USUARIO] && sudo init 6`
- Verify that Docker CE is installed correctly by running: `docker run hello-world`

# manage docker

- status: `sudo systemctl status docker`
- start: `sudo systemctl start docker`
- disable on startup: `sudo systemctl disable docker`
  - alternative:
    - service: `sudo systemctl disable docker.service`
    - socket: `sudo systemctl disable docker.socket`
  - enable on startup: `sudo systemctl enable docker`
- check docker services: `systemctl list-unit-files | grep -i docker`
- clean: `docker system prune`

# Uninstall Docker CE

- Uninstall the Docker CE package `sudo apt-get purge docker-ce`
- To delete all images, containers, and volumes `sudo rm -rf /var/lib/docker`

# images

## official images

- download from <https://hub.docker.com/>
- for example `docker pull mysql`

## check images

```bash
docker images
docker images -f dangling=true
```

## create image

- create a **Dockerfile**
- execute: `docker build --tag apache-chentos:primera .` or `docker build -t test:420 -f my-dockerfile .`

## check history

```bash
docker history -H apache-centos:quinta
```

## remove images

```bash
docker rmi [id or name:tag]
docker images -f dangling=true -q | xargs docker rmi
```

# containers

## create a container

```bash
docker run -d --name apache -p 80:80 apache-centos:sexta
```

- _-d_: Run container in background and print container ID
- _-p_: Publish a container's port(s) to the host (myMachine:container)

```bash
docker run -dti -e "prueba1=420" --name envtest [image]
# on machine
echo $prueba1 😉
```

- _-i_: interactive. Keep STDIN open even if not attached
- _-t_: Allocate a pseudo-TTY

## remove container

- stop `docker container stop [container-name]`
- remove:

  ```bash
  docker rm -fv apache
  ```

  - _-f_: Force the removal of a running container (uses SIGKILL)
  - _-v_: Remove the volumes associated with the container

### remove all

```bash
docker ps -q | xargs docker rm -f
```

## logs

```bash
docker logs -f [ps]
```

## check docker process/containers

```bash
docker ps
docker ps --no-trunc
docker ps -a
```

## important commands

- From
- Run
- Copy
- Add
- Env
- WorkDir
- Expose
- Label
- User
- Volume
- CMD
- dockerignore

## create ssl

```bash
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout docker.key -out docker.crt
```

- **common name**: _localhost_

## inspect

```bash
docker inspect [container-name]
```

## run container's shell

```bash
docker exec -ti [containerName] bash
```

- _-t_: Allocate a pseudo-TTY
- _-i_: interactive. Keep STDIN open even if not attached

```bash
docker exec -u root  -ti [containerName] bash
#test with whoami and hostname
```

### run command from the outside

```bash
docker exec [container-name] bash -c "cat /what/ever"
docker exec [container-name] bash -c "ping 192.168.1.2"
docker exec [container-name] bash -c "ping [container-name]"
```

## stats

```bash
docker stats [container-name]
```

## copy files between host and container

```bash
docker cp [file] [container-name]:[/route]
```

## commit

```bash
docker commit [image] [new-image]
docker images 😉
```

## overwrite cmd

```bash
docker run -dti centos [new command]
docker run -dti -p 8080:8080 centos python -m SimpleHTTPServer 8000
```

## simple machine

```bash
docker run -dti centos
```

## self-destructing containers

```bash
docker run --rm -ti --name whatever centos bash
```

## start one or more stopped containers

```bash
docker start [OPTIONS] CONTAINER [CONTAINER...]
docker start my_container
```

# volumes

- Host: something like

```bash
docker run --name some-mysql -v /my/own/datadir:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql:tag
docker run --name some-mysql -v /opt/mysql:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql:tag
```

- Anonymous (not very recommended, not passing the **/my/own/datadir**)
- Named Volumes (with functions, directly on shell😉)
- on Dockerfile (it will create an anonymous volume)

## list volumes

```bash
docker volume ls
```

### check volume data

```bash
docker info | grep -i root
cd [docker-root-dir]
cd volumes
cd [id]/[data] 👽
```

## create volume

```bash
docker volume create [volume-name]
```

## remove volume

```bash
docker volume rm [volume-name]
```

## assgin volume to a container

after created volume, run:

```bash
docker run --name some-mysql -v [volume-name]:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql:tag
```

## Dangling volumes 😉

- list dangling volumes: `docker volume ls -f dangling=true`
- remove dangling volumes: `docker volume ls -f dangling=true -q | xargs docker volume rm`

# networking

## list networks

```bash
docker network ls
```

## inspect

```bash
docker network inspect [network-name]
```

## create network

```bash
docker network create [network-name]
docker network create -d bridge --subnet 172.124.10.0/24 --gateway 172.124.10.1 [network-name]
```

## connect container

- on creation

```bash
docker run --network [network-name] -d --name test420 -ti centos
```

- hot pluggin

```bash
docker network connect [network-name] [container-name]
```

## disconnect network

```bash
docker network disconnect [network-name] [container-name]
```

## delete network

```bash
docker network rm [network-name]
```

## ip assignment

```bash
docker network create --subnet 172.128.10.0/24 --gateway 172.128.10.1 -d bridge my-network
docker run --network my-net --ip 172.128.10.50 -d --name nginx1 -ti centos
```

## host and none

theirs names talks by themselves

# Docker Compose

## install

do it like it says on doc.

- check version `docker-compose --version`
- [cheatsheet](https://docs.docker.com/compose/)

## file

- **docker-compose.yml**
- [version: required](https://docs.docker.com/compose/compose-file/compose-versioning/)
- services: required
- volume: optional
- network: optional

## manage

- start: `docker-compose up -d`
- start - multiple projects: `docker-compose -p appv420 up -d`
- stop: `docker-compose down`

## custom project name

```bash
docker-compose -p [custon-project-name] up -d
docker-compose -p [custon-project-name] up --build
```

## logs

```bash
docker-compose logs -f
```

# registry

- create `docker run -d -p 5000:5000 --name registry420 -v $PWD/data:/var/lib/registry registry:2`

## upload image

```bash
docker pull hello-world
# 👽
docker tag hello-world:latest localhost:5000/hello-world
docker push localhost:5000/hello-world 🤓
```

- testing it: `docker rmi hello-world localhost:5000/hello-world`

## download image

```bash
docker pull localhost:5000/hello-world
```

## share registry

```bash
docker tag hello-world 10.0.2.15:5000/hello-world
docker push 10.0.2.15:5000:5000/hello-world 🤓
```

### before share edit 🙋

/lib/systemd/system/docker.service

```bash
## ExecStart=/usr/bin/docker from this to 👇

ExecStart=/usr/bin/docker --insecure-registry 10.0.2.15.5000 👈
sudo systemctl daemon-reload
docker stop registry
sudo systemctl restart docker
#
docker pull 10.0.2.15:5000:5000/hello-world 🤓
```
