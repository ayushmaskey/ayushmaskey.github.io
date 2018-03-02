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
RUN apt-get -y install nodejs
RUN apt-get -y install iputils-ping

#fix mongodb
RUN apt-get -y install locales
RUN locale-gen en_US.UTF-8
RUN localedef -i en_GB -f UTF-8 en_US.UTF-8

RUN apt-get update
RUN apt-get -y upgrade
RUN apt-get -y dist-upgrade
RUN apt-get autoclean
RUN apt-get autoremove


#new user
RUN useradd --create-home --shell /bin/bash amaskey 
RUN echo 'amaskey:Docker!' | chpasswd
RUN usermod -aG sudo amaskey

USER amaskey
WORKDIR /home/amaskey







