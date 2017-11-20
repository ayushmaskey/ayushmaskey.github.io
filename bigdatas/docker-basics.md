---
layout: bigdata
type: bigdata
published: true
image: images/docker-vm-container.png
title: Docker Basics
permalink: bigdatas/docker-basics
date: 2017
labels:
  - docker
summary: build apps in docker containers.
---

   * [Installation](#installation)
   * [Images](#images)
   * [Dockerfile](#dockerfile)
   * [Containers](#containers)
   * [Useful commands](#useful-commands)
   * [Text editor](#text-editor)


<img class="ui medium right floated image" src="../images/docker-vm-container.png"> Docker has been a hot topic among developers community for a couple of years now. This infatuation with docker comes as no surpise once you understand the architecture of docker. While docker container seem like an alternative to one of the many virtual machine solution, the picture one the right shows architectural difference betwee the two. Regular virtual machine has individual OS since they are virtualized at the hardware level. Docker on the other hand share the OS making it much more efficient in terms of resource management. Laptop that can run barely 2 vms can run 4-6 containers.

#### Installation
Installing docker on ubuntu was fairly straightforward process. There are many step by step instructions online that walk you through installation and testing. [digitalocean.com](https://www.digitalocean.com/community/search?q=docker) has been a great resource for me since I am fairly new to linux ecosystem. I followed instructions to [install docker](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-16-04) on digit ocean below are the commands I found useful


 * remove existing docker for fresh install
```
sudo apt-get remove docker docker-engine docker.io
```
 * add gpg key
```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

 * add docker repository in apt
```
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
```

 * make sure cache is from docker repo instead of default ubuntu repo
```
apt-cache policy docker-ce
```

 * installation
```
sudo apt-get udpate
sudo apt-get install -y docker-ce
```

 * verify docker is running
```
sudo systemctl status docker
```

 * clean up unecessary files
```
sudo apt autoclean
sudo apt autoremove
sudo rm -rf /var/lib/apt/lists/*
```

#### Images
 * Command to download some of the useful images I came across as I build docker containers for the syslog analysis.
```
docker pull ubuntu
docker pull centos
docker pull elasticsearch
docker pull logstash
docker pull kibana
```

After pulling the base image from [docker hub](https://hub.docker.com/), we can add packages necessary packages and run necessary scripts to create a suitable image for any given project.
```
docker build -t <folder>/<image_name> .
```

The command above builds new image with the given name using Dockerfile in current folder.

#### Dockerfile
Dockerfile uses existing base image and automates creation of a new images with necessary packages. 

 * Below is an example of a Dockerfile I used to create ubuntu base image that I use to create all other images.

```
FROM ubuntu

USER root
RUN echo "root:password_for_root" | chpasswd

RUN apt-get update

RUN apt-get install -y wget curl tar sudo openssh-server openssh-client rsync
RUN rm -f /etc/ssh/ssh_host_dsa_key /etc/ssh/ssh_host_rsa_key /root/.ssh/id_rsa
RUN ssh-keygen -q -N "" -t dsa -f /etc/ssh/ssh_host_dsa_key
RUN ssh-keygen -q -N "" -t rsa -f /etc/ssh/ssh_host_rsa_key
RUN ssh-keygen -q -N "" -t rsa -f /root/.ssh/id_rsa
RUN cp /root/.ssh/id_rsa.pub /root/.ssh/authorized_keys

RUN apt-get -y install apt-utils
RUN apt-get -y install vim
RUN apt-get -y install iputils-ping
RUN apt-get -y install iproute
RUN apt-get -y install nano
RUN apt-get -y install pdsh
RUN apt-get -y install git

RUN apt-get -y upgrade
RUN apt-get -y dist-upgrade

RUN apt autoremove
RUN apt autoclean
RUN rm -rf /var/lib/apt/lists/*

RUN useradd -m -p amaskey password_for_user
```

Using ubuntu image as base image, docker file first changes the password for root and goes on to install all the packages. The first step is to install openssh, remove existing keys and create new keys for passwordless login. Dockerfile proceeds to install basic necessities for administration like apt-utils, vim, iputils-ping, iproute and git. After upgrading the container OS and cleaning up unecessary files, we finally create a new user in the container. 

Dockerfile simplies creation of consistent image which can be used to create container on the fly.

#### Containers
```
docker run -d -p 5140:5140/udp \
-h <hostname> --name <container_name> \
--link elasticsearch:elasticsearch -it \
-v ~/absolute_path/folder:/config-dir \
logstash \
-f /config-dir/logstash.conf
```

Some use flags when creating containers
 * -d 	--> create container in detached mode
 * -p 	--> map a udp port in container to localhost
 * -h 	--> hostname of container
 * --name 	--> name of container
 * --link	--> create a cluster with other docker container
 * -it	--> open interactive terminal of the container
 * -v 	--> attach folder in localhost as volume in the container
 * -f 	--> run script when container starts

#### Useful commands
Getting used to docker commands takes some time even though they seem to follow syntactical rules of unix. 

```
docker				# show all available docker commands
docker <sub-cmd> --help		# help with syntax and flags for the <sub_cmd>
docker info			# system wide info of docker

docker images			# show all available images
docker rmi <image-name>		# delete image

docker ps			# show all running container
docker ps -a			# show all container including stopped

docker run ubuntu		# create container from ubuntu image
docker rm <image-name>		# delete container
doker start <name>		# start container
docker stop <name>		# stop container
docker attach <name>		# attach to the container
docker inspect <name>		# info about the container in JSON format
```

#### Text editor

If feel lost when coding in text editors like vim and nano. I had to find an alternative to simplify my workflow. If the docker containers are in the my machine then sharing a volume works just fine. However, for most real world scenario, docker is probably installed in the remote machine. Now I was stuck with editing code in vim again until sublime-text3 community came to the rescue with a package called rsub. Installing rsub is a two step process. 

 * On the remote machine
```
wget -O /usr/local/bin/rsub \https://raw.github.com/aurora/rmate/master/rmate
chmod a+x /usr/local/bin/rsub
```

 * On local machine
   * open package mangager in sublime
   * seach for rsub
   * install rsub

 * Finally, open a rsub port when ssh into remote machine
```
ssh -R 52698:localhost:52698 user@serverIP
rsub path_to_file/file.py
```

This opens the file.py in sublime in localhost. Combination of rsub package and shared volumes in docker simplify editing codes a much improved experience.


I have really enjoyed using docker for the last couple of months. For one, docker is lightweight compared to a virtual machine and it is very easy to get up and running. I don’t need to test new packages in my local machine and all the errors and troubleshooting that comes with it. If there is an error discard the container and mount a new one with prebuilt good image, using same shared volume for data and code. For a big team it is easy to package and ship the program. It can replicate cluster of machines which makes building apps for clustered environment convienent and cost effective. And it is one of the better solution to deploy in the production environment as well and best of all it is free.
