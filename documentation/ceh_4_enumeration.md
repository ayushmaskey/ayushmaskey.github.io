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

