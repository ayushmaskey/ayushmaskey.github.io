# Table of content for linux commands
 * [back to ToC](./table_of_content.md)
 * [install and remove](#install-and-remove)
 * [python](#python)
 * [sublime](#sublime)
 * [nodejs](#nodejs)
 * [meteor](#meteor)
 * [semantic-ui](#semantic-ui)
 * [eslint](#eslint)
 * [docker](#docker)
 * [hadoop](#hadoop)
 * [spark](#spark)
 * [sqlite3](#sqlite3)
 * [git](#git)
 * [jekyll](#jekyll)
 * [pycharm](#pycharm)
 * [live reload](#live-reload)
 * [tftp server](#tftp-server)
 * [hamster stop watch](#hamster-stop-watch)
 * [haskell](#haskell)

## install and remove 
```bash
sudo apt-get install package1 package1	#install multiple things at once
sudo apt-get remove packageName		#uninstall but keep config files
sudo apt-get purge packageName		#clean out config files as well

sudo apt-get update -s packageName 	#simulate dry run
sudo apt-get update -d packageName	#download files but not install
```

# Package installation and settings

## python
```bash
sudo apt-get install -y python3-pip
sudo apt-get install -y python-pip
sudo apt-get install python3-numpy
sudo apt-get install pyton3-matplotlib
sudo apt-get install pyton3-scipy
sudo apt-get install pyton3-pyperclip
sudo apt-get install pyton3-sklearn
sudo pip3 install pymining
sudo pip3 install python-craigslist
sudo pip3 install scapy-python3
```

## sublime
```bash
wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | sudo apt-key add -

echo "deb https://download.sublimetext.com/ apt/stable/" | sudo tee /etc/apt/sources.list.d/sublime-text.list

sudo apt-get update
sudo apt-get install sublime-text
```
or
```bash
sudo add-apt-repository ppa:webupd8team/sublime-text-3
sudo apt-get update
sudo apt-get install sublime-text-installer
```

## nodejs
```bash
sudo apt install nodejs
sudo apt install npm
```
## meteor
```bash
sudo apt install curl
curl https://install.meteor.com/ | sh
sudo npm install -g gulp
```
## semantic-ui
```sudo npm install semantic-ui --save```

## eslint
```sudo npm install -g eslint```

## [docker](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-16-04)
```
#remvove docker for fresh install
sudo apt-get remove docker docker-engine docker.io

#add gpg key
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add - 

#docker repository in apt
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt-get udpate

#make sure update is from docker repo instead of default ubuntu repo
apt-cache policy docker-ce

#installation
sudo apt-get install -y docker-ce

#verify docker is running
sudo systemctl status docker
```

## [hadoop](https://www.digitalocean.com/community/tutorials/how-to-install-hadoop-in-stand-alone-mode-on-ubuntu-16-04)
```
sudo apt-get update

#OpenJDK is enough, no need Oracle version
sudo apt-get install default-jdk
java -version

#find best mirror website from apache website [Hadoop](http://www.apache.org/dyn/closer.cgi/hadoop/common/hadoop-2.8.1/hadoop-2.8.1.tar.gz)
wget http://www.trieuvan.com/apache/hadoop/common/hadoop-2.8.1/hadoop-2.8.1.tar.gz	

#run sha256 checksum verification and compare to website
shasum -a 256 hadoop-2.8.1.tar.gz

#extract and uncompress
tar -xzvf hadoop-2.8.1.tar.gz

#move extracted files to appropriate place for locally installed software
sudo mv hadoop-2.8.1 /usr/local/hadoop

#find Java_Home
readlink -f /usr/bin/java | sed "s:bin/java::"

#set Hadoop's environmental variable JAVA_HOME
#open
sudo nano /usr/local/hadoop/etc/hadoop/hadoop-env.sh

#remove or comment out 
export JAVA_HOME=${JAVA_HOME}

#add
export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64/jre/

#test if following command does not give error
/usr/local/hadoop/bin/hadoop

#test MapReduce - should show some "File System Counters and Map-Reduce Framework"
mkdir ~/input
cp /usr/local/hadoop/etc/hadoop/*.xml ~/input
/usr/local/hadoop/bin/hadoop jar /usr/local/hadoop/share/hadoop/mapreduce/hadoop-mapreduce-examples-2.7.3.jar grep ~/input ~/grep_example 'principal[.]*'
```

## spark
```
sudo apt-get install scala
sudo apt-get install git

#download tar.gz from https://spark.apache.org/downloads.html and untar

tar xvf spark...tgz
or 
clone straight from github
git clone git://github.com/apache/spark.git -b branch-2.2
```

## sqlite3
```sudo apt-get sqlite3 libsqlite3-dev```


## git
```
sudo apt-get install git

#set time for password
git config --global credential.helper "cache --timeout=3600"

#enable git push
git config --global push.default matching
git config --global user.name "amaskey"
git config --global user.email "maskey.maskey@gmail.com"		
```
## [jekyll](https://www.digitalocean.com/community/tutorials/how-to-set-up-a-jekyll-development-site-on-ubuntu-16-04)
```
sudo gem install jekyll bundler
jekyll new jekyll-site
cd jekyll-site
bundle exenjekyll serve
```
## [pyCharm](http://ubuntuhandbook.org/index.php/2016/07/latest-pycharm-ubuntu-16-04-ppa/)
```
sudo add-apt-repository ppa:viktor-krivak/pycharm
sudo apt-get update
```

## live reload
```
sudo apt-get install ruby-dev
sudo gem install rdoc -V
sudo gem install guard -V
sudo gem install guard-livereload -V
create file named .Guardfile with following text

# //github.com/guard/guard-livereload
guard :livereload do
  watch(%r{.+.(css|js|html)$})
end
```

## [tftp server](https://help.ubuntu.com/community/TFTP)
```
sudo apt-get install tftpd-hpa
sudo service tftpd-hpa status
```

## hamster stop watch
```
#install stop watch
sudo apt install hamster-indicator	

#show in top bar
gconftool-2 --set "/apps/hamster-indicator/show_label" --type bool "true"	
```

## haskell
```
curl -sSL https://get.haskellstack.org/ | sh
```
jekyll
liquid
semantic-ui
YAML filess
include with parameters
YAML based links
prince XML for pdf
google site search

