# Table of content for linux commands
 * [Environment](#environment)
 * [Directory](#directory)
 * [Files](#Files)

## Environment
path name of the files which would be executed in current environment
```
which nodejs
```
who is logged in
```
who
```

## Directory
**list directory**
```
ls -alt
 -a 	hidden files and folders
 -l 	more details
 -t 	newest first
ls -sh
 -s 	size
 -h 	human readable
ls -d */							#show directory only
ls -la | less							#one page at a time
ls intel*							#all files starting with intel.
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
**estimate file space usage**
```
du -hs
  -h	human readable
  -s 	size
```

## Files
```
rm - delete file
clear
mv "filename" ~\newLocation - move files
mv file1 file 2 - file1 renamed to file2

cp file1 file2 - copy content of file1 to file2
cp dir/file1 . - copy file1 to current directory

touch - create new file

echo - display words on screen
echo "Hello" > Hello.txt	#create new file Hello.txt and write "Hello

cat - display content of file
cat Hello.txt > bye.txt		#overwright content of bye with content of hello
cat hello.txt >> bye.txt	#append content of hello to end of bye
cat hello.txt | wc		#output of whats left of pipe and uses it as input for the right
wc 				#number of lines
cat h.txt | wc | cat > b.txt	#get content of h.txt, count num of lines and overwright it in b.txt
sort hello.txt			#sort and display content of hello
cat hello.txt | sort > bye.txt	#get content of hello, sort it and overwright bye.txt
uniq hello.txt			#check the next line and if it is similar then show show only one
sort hello.txt | uniq		#sort first and then get unique 
sort h.txt | uniq > r.txt	#sort first and then get unique and then overwright to r.txt

grep Mount mountain.txt		#search mountain.txt and look for "Mount"
grep -i Mount mountain.txt	#search mountain.txt and look for "Mount" or "mount"
grep -R "Ayush" home/Google	#search all files in the directory recursively for "Ayush" and output filename + the line 
grep -Rl "Ayush" home/Google	#output only fileName. No line

sed 's/hello/bye' hello.txt	#change first occurence of hello to bye in each line of hello.txt
sed 's/hello/bye/g' hello.txt	#change all instance of hello to bye

nano hello.txt			#open hello in text editor
ctrl+o				#save
ctrl+x				#exit
nano ~/.bash_profile		#stores environment variables
alias pd="pwd"			#create shortcuts no space pd="pwd"
export USER="me myself and I"	#export makes the variable available to all child session
echo $USER			#current user or alias, $ used to return variable value
export PS1=">>"			#change prompt from $ to >>
history				#history of commands used in the session
env				#returns list of all environment variables for current user

less hello.txt			#similar to nano
file hello.txt			#ASCII or images or what type of file

ls /				#look at root

man - display manual of specified command
unzip file.zip -d "destination folder" (unzip)
pwd - print working directory

gedit "TextFileName.txt"
evince "pdfFileName.pdf"
libreoffice "fileName.doc .pptx .xls"

make ???- maintain group of programs
```
### text editor
```
vi - 
gedit
nano
less

su - log in as super user 
su amaskey - switch user to amsaskey
sudo - run single command with root previledge


sudo apt-get install package1 package1	#install multiple things at once
sudo apt-get remove packageName		#uninstall but keep config files
sudo apt-get purge packageName		#clean out config files as well

sudo apt-get update -s packageName 	#simulate dry run
sudo apt-get update -d packageName	#download files but not install

sudo add-apt-repository ppa:ubuntuhandbook1/corebird	#add repository
curl
wget
dpkg - dpkg -l, 
apt
aptitude
```
### readlink
```
#find default path of java
readlink -f /usr/bin/java | sed "s:bin/java::"
```

### Linux System Admin Primer
```
ls, rm, mkdir, rmdir, cat, vi, sudo, su
```
#### config files 
```
/etc
```
#### store optional stuff
```
/opt/
```
#### log files
```
/var/log
/bin, /sbin, /usr/bin, /usr/local
```
#### all user directories stay here
```
/home
shell/env variables, echo, export, bashrc, profile, source cmd
tar, gzip, zip
adduser, useradd
```
#### change owner of file/director
```
chown (chown -R hduser:hduser /opt/hdfs		#recursively change ownership of all files and folders
```
#### change permission of file/dir 
```
chmod (chmod 600 hello.txt)
```
ls -l
apt-get update, apt-get install, rpm
#### ssh and key generation and passwordless login
ssh, ssh-keygen -t rsa, .ssh/, authorized_keys
ip a, /etc/hosts, ping


#### install deb
sudo dpkg -i /home/amaskey/Downloads/intellij-idea-community_2017.2.2-1_all.deb 
install dependencies
sudo dpkg --configure -a --force-depends
sudo apt-get install -f
sudo apt-get dist-upgrade

sudo apt install hamster-indicator	#install stop watch
gconftool-2 --set "/apps/hamster-indicator/show_label" --type bool "true"	#show in top bar


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


**tftp server**
https://help.ubuntu.com/community/TFTP
sudo apt-get install tftpd-hpa
sudo service tftpd-hpa status

**wget**
#download file
wget http://www.example.com/filename
#downloan entire website
wget -r http://www.example.com
#download entire website and external links
wget -r -H http://www.example.com

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
systemd-analyze blame

#remove error message
ls -l /var/crash
sudo rm /var/crash/*

#installing live reload
sudo apt-get install ruby-dev
sudo gem install rdoc -V
sudo gem install guard -V
sudo gem install guard-livereload -V
create file named .Guardfile with following text

# //github.com/guard/guard-livereload
guard :livereload do
  watch(%r{.+.(css|js|html)$})
end

download chrome

grive -a

**shorten path name in terminal**
vim ~/.bashrc

if [ "$color_prompt" = yes ]; then
    PS1='${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$ '
else
    PS1='${debian_chroot:+($debian_chroot)}\u@\h:\w\$ '
fi
unset color_prompt force_color_prompt

#change \w to \W in both PS1
source ~/.bashrc	#reset terminal

memtestx86		#hold shift during restart to get to grub2

**vim**
vim fileName
#insert mode
i 	#insert before cursor
I	#insert at the beginning of the line
a	#append after cursor
A	#append at the end of the line
esc	#end insert mode
#quit
:q	#quit
:wq	#save and exit
:q!	#quit without saving
#split screen
:split fileName
# goto line nuber
:512
#find phrase
? phrase

**unix permissions**
-rwxrwxrwx	amaskey	amaskey
drws------
#first: dash '-' then normal file, if 'd' then directory
#next 3 = owner permission: r (read), w(write), x(execute), -(no permission) 
#next 3 = group permission
#final 3 = rest of the world permission
#first - owner of file
#second - group the file belongs to #groups <username> to get groups memmbership
**change permission**
chmod 664 test.html ( rw-rw-r-- )
#0(---), 1(--x), 2(-w-), 3(-wx), 4(r--), 5(r-x), 6(rw-), 7(rwx)
chown <username> -R filename		#take ownership of file

#add user to group 
usermod -aG sudo <username>
passwd

#move file across ssh
scp /pwd/fileName amaskey@ip:pwd/fileName


