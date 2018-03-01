# Docker

## Basics

### check if docker is running
sudo systemctl status docker

### all available subcommand
docker
docker docker-subcommand --help
### system wide info of docker
docker info

### download iamge
docker pull ubuntu

## Images

### see available images
docker images
### Delete images
docker rmi [image ID/ name]


## Containers

### view active containers
docker ps
### all containers	
docker ps -a
### last created
docker ps -l
### delete
docker rm [container ID/name]
### rename
docker rename oldName newName

### create containers
docker run -it -–name=<containerName> –-hostname=<hostName> image
 * -it gives access to image from command line

### container with 2 volume mounted
docker run -it -–name=<containerName> –-hostname=<hostName> -v ~/<abs_path_in_host>/<folder>:/<data_volume_in_root_of_container> ~/<abs_path_in_host>/<folder>:/<code_volume_in_root_of_container> ubuntu

### start container
docker start [container ID/name]
### go to container shell
docker attach [container ID/name]
### stop container
docker stop [container ID/name]

### JSON file with info about container
docker inspect [container ID/name]
#create image with Dockerfile
docker build -t <folder>/<imageName> .


## sublime remote server
https://stackoverflow.com/questions/37458814/how-to-open-remote-files-in-sublime-text-3 

## Updating and installing package after accessing docker image
apt-get update
apt-get install -y nodejs
apt-get -y install vim
apt-get -y apt-utils
apt-get -y install iputils-ping
apt-get -y install openssh-client
apt-get -y install openssh-server
apt-get -y install iproute
apt-get -y install nano
apt-get -y install git
apt-get -y install default-jre

## commit change to image and push to hub.docker.com
docker commit -m "message" -a "Ayush" [container-id] finid/ubuntu_nodejs

docker login -u amaskey

docker tag [image Repository Name] amaskey/[repoNameFromHub]:[newTagName]
docker push amaskey/[repoNameFromHub]:[newTagName]

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
#add users
adduser (interactive) 
useradd (from script)
#test user hduser/hduser
chown
chmod 		#(change file/dir permission)
ls -l
apt-get update, apt-get install, rpm
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

Dockerfile 				#all setup and installation
hadoop/etc/hadoopcore-site.xml		#configs
bootstrap.sh				#shell script to run when container starts
#key_gen can be added to bootstrap.sh


