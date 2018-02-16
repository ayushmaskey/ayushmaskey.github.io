
##Table of content
 * 
 * [foot printing and reconnaissance](#foot-printing-and-reconnaissance) 
 * 
 * 
 * 
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




