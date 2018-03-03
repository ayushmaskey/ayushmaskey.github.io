# Table of content for linux commands
 * [back to ToC](./table_of_content.md)
 * [maintenance](#maintenance)
 * [google drive](#google-drive)
 * [Environment](#environment)
 * [Directory](#directory)
 * [unix folders](#unix-folders)
 * [Files](#files)
 * [vim](#vim)
 * [nano](#nano)
 * [Permissions and Groups](#permissions-and-groups)
 * [wget](#wget)
 * [tar](#tar)
 * [ssh with sublime](#ssh-with-sublime)

## maintenance
```
sudo apt-get update
sudo apt-get upgrade
sudo apt-get dist-upgrade
sudo apt-get clean
sudo apt-get autoclean
sudo apt-get autoremove
sudo ucaresystem-core
sudo reboot
sudo rm -rf /var/lib/apt/list/*

grive

#hold shift during restart to get to grub2
memtestx86
```

**time** 
```
sudo dpkg-reconfigure tzdata
sudo ntpdate ntp.ubuntu.com pool.ntp.org
```

**firewall**
```
sudo so-allow
```

## [google drive]
```grive -a```

## Environment
**path name of the files which would be executed in current environment**
```which nodejs```

**who is logged in**
```who```

**clear screen**
```clear```

**change password**
```passwd root```

**Ubuntu Version**
```lsb_release -a```

**maintenance package**
```sudo apt-get installlocalepurge```

**ucaresystem**
```
sudo add-apt-repository ppa:utappia/stable
sudo apt update
sudo apt install ucaresystem-core
```

**move file across ssh**
```
# linux to linux
scp /pwd/fileName amaskey@ip:pwd/fileName
# windows to linux(https://community.nxp.com/thread/220596)
* install putty
# in cmd line
set PATH=C:\Program Files\PuTTY
pscp "c:\..\..\desktop\filename.txt" username@ubuntu:/home/user
```

**adding trusted cert**
```
In ubuntu:
    Go to /usr/local/share/ca-certificates/
    Create a new folder, i.e. "sudo mkdir school"
    Copy the .crt file into the school folder
    Make sure the permissions are OK (755 for the folder, 644 for the file)
    Run "sudo update-ca-certificates"

```

**display manual of specified command**
```man ls```

```
alias pd="pwd"						#create shortcuts no space pd="pwd"
export USER="me myself and I"				#export makes the variable available to all child session
echo $USER						#current user or alias, $ used to return variable value
export PS1=">>"						#change prompt from $ to >>
history							#history of commands used in the session
env							#returns list of all environment variables for current user
```

**shorten path name in terminal**
```
vim ~/.bashrc
```
```
if [ "$color_prompt" = yes ]; then
    PS1='${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$ '
else
    PS1='${debian_chroot:+($debian_chroot)}\u@\h:\w\$ '
fi
unset color_prompt force_color_prompt
```
make ???- maintain group of programs
systemd-analyze blame

**remove error message**
```
ls -l /var/crash
sudo rm /var/crash/*
```

## Directory
**print working directory**
```pwd```

**list directory**
```
ls -alt
 -a 	hidden files and folders
 -l 	more details
 -t 	newest first
ls -d */							#show directory only
ls -la | less							#one page at a time
ls intel*							#all files starting with intel.
ls /								#look at root
```
**estimate file space usage**
```
ls -sh
 -s 	size
 -h 	human readable
du -hs
  -h	human readable
  -s 	size
  
#size of each folder with files
du -abch --max-depth=1
```
**create or delete**
```
mkdir
rmdir
rm -r 								#recursively remove dir and all the files
```
**change**
```
cd 
cd ../FolderName 						# go to parent directory and open folder
cd ~ or cd 							# home
cd - 								# back to last directory
```
**copy or move**
```
mv ./* ~Google/							# move all files and folders
cp -a ./sourceFolder ./targetFolder 
```

## unix folders
**config file**
```/etc```

**store optional stuff**
```/opt/```

**log files**
```/var/log, /bin, /sbin, /usr/bin, /usr/local```

## Files
**delete file**
```rm```

**move and copy**
```
mv "filename" ~\newLocation 						#move files
mv file1 file 2 							#file1 renamed to file2

cp file1 file2 								#copy content of file1 to file2
cp dir/file1 . 								#copy file1 to current directory
```
**create new file**
```touch fileName.ext```
**create and write**
```
echo "Hello" > Hello.txt						#create new file Hello.txt and write "Hello
```
**display words on terminal**
```echo hello```

**file content**
```
cat hello.txt
cat Hello.txt > bye.txt						#overwright content of bye with content of hello
cat hello.txt >> bye.txt					#append content of hello to end of bye
cat hello.txt | wc						#output of whats left of pipe and uses it as input for the right
  -wc 								#number of lines
cat h.txt | wc | cat > b.txt					#get content of h.txt, count num of lines and overwright it in b.txt
sort hello.txt							#sort and display content of hello
cat hello.txt | sort > bye.txt						#get content of hello, sort it and overwright bye.txt
uniq hello.txt							#check the next line and if it is similar then show show only one
sort hello.txt | uniq						#sort first and then get unique 
sort h.txt | uniq > r.txt					#sort first and then get unique and then overwright to r.txt
```
**grep**
```
grep Mount mountain.txt						#search mountain.txt and look for "Mount"
grep -i Mount mountain.txt					#search mountain.txt and look for "Mount" or "mount"
grep -R "Ayush" home/Google					#search all files in the directory recursively for "Ayush" and output filename + the line 
grep -Rl "Ayush" home/Google					#output only fileName. No line
```
**sed**
```
sed 's/hello/bye' hello.txt					#change first occurence of hello to bye in each line of hello.txt
sed 's/hello/bye/g' hello.txt					#change all instance of hello to bye
```
**one page**
```less hello.txt```

**file type**
```file hello.txt```

**open file**
```
gedit "TextFileName.txt"
evince "pdfFileName.pdf"
libreoffice "fileName.doc .pptx .xls"
```

## vim
```vim fileName```

**insert mode**
```
i 	#insert before cursor
I	#insert at the beginning of the line
a	#append after cursor
A	#append at the end of the line
esc	#end insert mode
```
**quit**
```
:q	#quit
:wq	#save and exit
:q!	#quit without saving
```
**split screen**
```:split fileName```

**goto line number**
```:512```

**find phrase**
```? phrase```

## nano
```
nano hello.txt								#open hello in text editor
ctrl+o									#save
ctrl+x									#exit
nano ~/.bash_profile							#stores environment variables
```

## permissions and groups
**current permission**
```
ll
  -rwxrwxrwx	username	group
  drws------
```
 * first: dash '-' then normal file, if 'd' then directory
 * next 3 = owner permission: r (read), w(write), x(execute), -(no permission) 
 * next 3 = group permission
 * final 3 = rest of the world permission
 * first - owner of file
 * second - group the file belongs to #groups <username> to get groups memmbership
 
**change permission**
```chmod 664 test.html ( rw-rw-r-- )```

**permission number representation**
```0(---), 1(--x), 2(-w-), 3(-wx), 4(r--), 5(r-x), 6(rw-), 7(rwx)```

**take ownership**
```chown <username> -R filename```

**recursively change ownership of all files and folders**
```chown -R hduser:hduser /opt/hdfs```

**add user to group**
```usermod -aG sudo <username>```

** all users**
``` compgen -u```

**all groups**
```compgen -g```

** all groups of  user ** 
```groups amaskey```

**disable ipv6**
```
nano /etc/sysctl.conf

#add 
net.ipv6.conf.all.disable_ipv6 = 1
net.ipv6.conf.default.disable_ipv6 = 1
net.ipv6.conf.lo.disable_ipv6 = 1

sudo sysctl -p

cat /proc/sys/net/ipv6/conf/all/disable_ipv6
#return 1
```
## wget
**download file**
```wget http://www.example.com/filename```

**download entire website**
```wget -r http://www.example.com```

**download entire website and external links**
```wget -r -H http://www.example.com```

## tar
** untar **
```
tar -xzvf fileName.tar.gz
 -x flag to extract
 -z uncompress
 -v verbose output
 -f specify that we are extracting from a file
```
** read file without untar **
```
tar -tf fileName
 -t list
```
**unzip**
```unzip file.zip -d "dest_folder"```

## ssh with sublime
**server side**
```
wget -O /usr/local/bin/rsub \https://raw.github.com/aurora/rmate/master/rmate
chmod a+x /usr/local/bin/rsub
```
**client sublime**
```
ctrl + shift + P 	#to open package mannager 
choose install package
search rsub and install
```
**ssh into remote machine**
```
#linux
ssh -R 52698:localhost:52698 user@serverIP

#putty
host_ip 
port - 22
category --> connection --> SSH --> Tunnels
source port: 52698
Destination: localhost:52698
remote and auto
```

**on server terminal**
```rsub ~/path_to_file/fileName```



## remote login
**__ Host machine settings __**
```
sudo apt-get install vnc4server
sudo apt intall xfce4 xfce4-goodies tightvncserver			#install xfce4 and tightvnc in client machine
gsettings set org.gnome.Vino require-encryption false		#remote access from VNC
```
### readlink
```
#find default path of java
readlink -f /usr/bin/java | sed "s:bin/java::"
```

### text editor
```
vi - 
su - log in as super user 
su amaskey - switch user to amsaskey
sudo - run single command with root previledge

curl
dpkg - dpkg -l, 
aptitude
```

#### all user directories stay here
```
/home
shell/env variables, echo, export, bashrc, profile, source cmd
tar, gzip, zip
adduser, useradd
```

rpm
#### ssh and key generation and passwordless login
ssh, ssh-keygen -t rsa, .ssh/, authorized_keys
ip a, /etc/hosts, ping


#### install deb
sudo dpkg -i /home/amaskey/Downloads/intellij-idea-community_2017.2.2-1_all.deb 
install dependencies
sudo dpkg --configure -a --force-depends
sudo apt-get install -f



sudo openconnect https://
ssh - add deffiehellman sha1 to ~/.ssh/config

**cisco packet capture**
capture capin interface inside match ip any any
capture capout interface outside match ip any any (any can be replaced by ip and subnet)
show capture
show capture capin
https://<asa-ip-address>/admin/capture/capin
no capture capin interface inside
no capture capout interface outside


#change \w to \W in both PS1
source ~/.bashrc	#reset terminal


