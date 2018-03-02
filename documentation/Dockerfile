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
RUN apt-get -y install locales
RUN locale-gen en_US.UTF-8
RUN localedef -i en_GB -f UTF-8 en_US.UTF-8


RUN useradd -m amaskey -p Docker!
RUN usermod -aG sudo amaskey

#RUN sh -c "echo -e 'LANG=en_US.UTF-8\nLC_ALL=en_US.UTF-8' > /etc/default/locale" 

RUN su amaskey && cd ~ && git clone https://github.com/ayushmaskey/equipment_log.git
#RUN chown amaskey -R /equipment_log && chmod 770 /equipment_log

#RUN su amaskey && mv /equipment_log ~/meteor
#RUN su amaskey && cd ~ && echo "export LC_ALL=en_US.UTF-8" >> ~/.bashrc

RUN su amaskey && cd ~ && curl https://install.meteor.com/ | sh
RUN su amaskey && cd ~ && cd ~/equipment_log/app && meteor npm install

RUN su amaskey && cd ~/equipment_log/app && meteor npm run start

#exit

RUN apt-get update
RUN apt-get -y upgrade
RUN apt-get -y dist-upgrade
RUN apt-get autoclean
RUN apt-get autoremove

#RUN apt-get install -y nodejs
#RUN apt-get -y install iputils-ping

