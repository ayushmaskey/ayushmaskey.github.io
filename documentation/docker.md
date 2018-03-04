# Docker

[docker cheat sheet](https://github.com/wsargent/docker-cheat-sheet)

## Basics

##### check if docker is running
```docker
sudo systemctl status docker
```

##### docker help
```docker
docker
docker docker-subcommand --help
```
##### system wide info of docker
```docker
docker info
```
##### sublime remote server
https://stackoverflow.com/questions/37458814/how-to-open-remote-files-in-sublime-text-3 


## Images

##### download iamge
```docker
docker pull ubuntu
```

##### see available images
```docker
docker images
```
##### Delete images
```docker
docker rmi [image ID/ name]`
```

## Containers

##### view active containers
```docker
docker ps
```
##### all containers	
```docker
docker ps -a
```
##### last created
```docker
docker ps -l
```
##### delete
```docker
docker rm [container ID/name]
```
##### rename
```docker
docker rename oldName newName
```

##### start container
```docker
docker start [container ID/name]
```
##### go to container shell
```docker
docker attach [container ID/name]
```
##### stop container
```docker
docker stop [container ID/name]
```

##### JSON file with info about container
```docker
docker inspect [container ID/name]
```

##### create containers

```docker
docker run -it -–name=<containerName> –-hostname=<hostName> \
	-v ~/<abs_path_in_host>/<folder>:/<volume_in_root_of_container> 
	-p 3000:3000
	ubuntu

# -i --> open container in interactive mode
# --name --> name of container
# --hostname --> hostname of container
# -v --> mount one or more volume to container
# -p --> publis container port to host
# -t --> allocate pseudo tty
# --rm --> remove container upon exit
```

## workflow

##### Sample Dockerfile
```bash
# inherit from other images
FROM ubuntu

ARG DEBIAN_FRONTEND=noninteractive

USER root
RUN echo "root:Docker!" | chpasswd

EXPOSE 3000

RUN apt-get update
RUN apt-get -y install apt-utils 
RUN apt-get -y install git 
RUN apt-get -y install vim
RUN apt-get -y install curl 
RUN apt-get -y install sudo
RUN apt-get -y install ssh
RUN apt-get -y install iproute

#fix mongodb
RUN apt-get -y install locales
RUN locale-gen en_US.UTF-8
RUN localedef -i en_GB -f UTF-8 en_US.UTF-8

#new user
RUN useradd -ms /bin/bash amaskey
RUN usermod -aG sudo amaskey

RUN apt-get update
RUN apt-get -y upgrade
RUN apt-get -y dist-upgrade
RUN apt-get autoclean
RUN apt-get autoremove


USER amaskey
WORKDIR /home/amaskey
RUN echo "amaskey:Docker!" | chpasswd




#RUN apt-get install -y nodejs
#RUN apt-get -y install iputils-ping

```

##### sample bootstrap.sh
```bash


```


##### create image with Dockerfile
```docker
docker build -t <folder>/<new_imageName> .
```


##### using containers

```docker
docker run -it --rm --name test --hostname test -p 3000:3000 amaskey/test

#install meteor and download git repository
cd
git clone https://github.com/ayushmaskey/equipment_log.git
curl https://install.meteor.com/ | sh
cd /equipment_log/app
meteor npm install

#RUN chown amaskey -R /equipment_log && chmod 770 /equipment_log
#RUN su amaskey && mv /equipment_log ~/meteor
#RUN su amaskey && cd ~ && echo "export LC_ALL=en_US.UTF-8" >> ~/.bashrc
#RUN su amaskey && cd ~/equipment_log/app && meteor npm run start

#change password
passwd
su local && passwd

```

##### commit change to image and push to hub.docker.com
```docker
docker commit -m "message" -a "Ayush" [container-id] finid/ubuntu_nodejs

docker login -u amaskey

docker tag [image Repository Name] amaskey/[repoNameFromHub]:[newTagName]
docker push amaskey/[repoNameFromHub]:[newTagName]
```

**DNS Routing**
#place all routes and IPs in /etc/hosts/, hard coded ip routes
vi /etc/hosts
**172.17.0.2	hdmaster**
#networking
ip a 
ping
docker network ls 	#(default has bridge= virtual network and host)
docker network inspect bridge
#create own bridge
docker network create -d bridge amaskeyBridge
#attach containers to that bridge
docker run -d -net=amaskeyBridge -name db training/postgres
#rename container and hostnamedoc
docker run -it --name=hdmaster --hostname=hdmaster finid/ubuntu_nodejs

**Linux System Admin Primer**
ls, rm, mkdir, rmdir, cat, vi, sudo, su
#config files 
/etc
#store optional stuff
/opt/
#log files
/var/log
/bin, /sbin, /usr/bin, /usr/local
#all user directories stay here
/home
shell/env variables, echo, export, bashrc, profile, source cmd
tar, gzip, zip
rpm
ssh, ssh-keygen -t rsa, .ssh/, authorized_keys
ip a, /etc/hosts, ping

whoami		#get username
hostname	#host name


**ssh**
#start ssh in all master and slave
/etc/init.d/ssh start
#ssh without password (all default after command below) - RSA2048 SHA256 key
ssh-keygen -t rsa
ls ~/.ssh (id_rsa -private, id_rsa.pub=public key)
vim authorized_keys (copy public key and save)
#authorized_keys has to be 600 permission rw-------
chmod 600 authorized_keys
#or append public key to authorized keys
cat id_rsa.pub >> authorized_keys
#all master and slave need all keys including self??

 * key_gen can be added to bootstrap.sh

hadoop/etc/hadoopcore-site.xml		#configs


