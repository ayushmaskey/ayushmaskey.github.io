---
layout: bigdata
type: bigdata
published: true
image: images/cotton-square.png
title: docker basics
permalink: bigdatas/docker-basics
date: 2017
labels:
  - docker
  - useful flags
summary: build apps in docker containers.
---


what is docker?
docker vs vm

basic docker commands

Dockerfile
scripts
building images
running containers

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
 * make sure update is from docker repo instead of default ubuntu repo
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

Useful images to build docker containers for the ELK project.

```
docker pull ubuntu
docker pull centos
docker pull elasticsearch
docker pull logstash
docker pull kibana
```

 

Getting used to docker commands is taking some time, especially since I am learning many other syntax right now. I started using ubuntu less than a year ago and I am finally comfortable performing most day to day task using terminal. Then there is powershell commands to manage window servers at work. For the classes this semester I am learning docker, hadoop, scala, python, git, Meteor, mongo, javascript etc. and at work I use sql, cisco, GE proprietary languages mel and ccc. It was getting really overwhelming so I started a google doc for each language with frequently used commands and have it open on the side while I work on that language. Infact, homework requirement for this class to document what I do was the inspiration to creating all these syntax documents.

Now back to docker instruction after a little rant. After pulling the images, I created a container using docker run -it ubuntu which opens up terminal access to the container as well. I installed few packages and continued to use docker run -it ubuntu. Old habit of not reading the documentation came back to bite me again. When I finally learnt about docker ps -a I had over 10 container with nothing in there. Turns out there is a command to use existing container docker start <containerName> && docker attach <containerName>

There were times when my docker container failed to install or update packages with following error.
Err:1 http://archive.ubuntu.com/ubuntu xenial/main amd64 libpopt0 amd64 1.16-10
  Temporary failure resolving 'archive.ubuntu.com'
I suspect the issue was caused by grive running in the background to sync my google drive. I had to reboot my laptop to resolve this issue.  Running docker in my laptop was no longer the best option for me. I had two options, either use uh ics docker server or create my own at work. I plan to use docker for work data so I created my own test docker server at work. I was not in the habit writing instructions to myself during first installation in my laptop. So I had to start from scratch during the second installation in the server. This time I made good notes and used the same note to create DockerFile.

I came across two big issue when I started using docker. 
The first was writing the codes that I planned to run on docker container. I cannot write codes on vim or nano beyond few lines. I am very dependent on ide even if it is just notepad++ with few syntax highlight. One option is manually sync the code in my laptop with the code in docker. But pulling and pushing after every little change would get annoying. I came across sublime plugin rsub that work pretty well with remote files.
On the server,
# wget -O /usr/local/bin/rsub \https://raw.github.com/aurora/rmate/master/rmate
    # chmod a+x /usr/local/bin/rsub
On my laptop, open package manager in sublime and search for rsub and install. Finally ssh into the server 
# ssh -R 52698:localhost:52698 user@serverIP
# rsub path_to_file/file.txt
This opens the file in sublime. This is good for editing one file at a time but when working on a project there would be need to access whole project. After asking the question on slack, Kyle recommended using a folder in the host machine as volume for the container. DigitalOcean to the rescue again to help with shared volume. 
Create folders named data and code in the host machine
docker run -it --name container_with_volume -v ~/abs-path-in-host/data:/data-volume-in-root-of-container ~/abs-path-in-host/code:/code-volume-in-root-of-container ubuntu
Shared volume together with rsub plugin should allow me to use sublime to edit any code in container in remote server but I still have settled to an optimum workflow yet. 

The second big issue was moving container to different machine. Within few weeks of using docker I have had to move docker container to different machines and that will need will never go away. One option was to create create an image and host it on docker hub. But having patient data on docker hub would not be acceptable. Kyle’s recommendation of mounting the volume to docker container solves this problem as well. All the codes and data stay in a volume shared from the host machine and the container use it as volume. More than one container share the same volume which makes coding even simpler if I need to send same block of code to many containers

I really enjoyed using docker so far. For one, docker is lightweight compared to VM and it is very easy to get up and running. Once I have a good image, I don’t need to worry about troubleshooting errors in my OS. If there is an error discard the container and mont a new one with prebuilt good image and same volume for data and code. Going forward I am thinking about bare minimum OS. I would probably need couple of  ide and web browser. Everything else I can run with isolated docker containers.

