# Denial of service

very popular these days

1. SYN Flodding a Target Host using hping3
* send succession of SYN request to target and comsume all its resource to make system unresponsive to legitimate traffic
  * either send SYN from spoofed IP or don't reply to ACK after target replied to SYN
  * if there are multiple half-open connection caused by these SYN, machine cannot make any new connection
```
from kali
hping3 -S 172.17.19.61 (target) -a 172.17.18.67(attacker) -p 22 --flood
```
* target machine crashes because of huge number of continuous SYN packets

2. HTTP Flooding using DoSHTTP
* send enormous useless HTTP packets
* DoSHTTP in windows --> set target URL --> start Flood

3. Performing Distributed Denial of Service Attack Using HOIC
* DDoS - more sophisticated form of DoS --> difficult to trace attacker
  * large scale coordinated attack launched indirectly through many compromised machines in the internet

* hoic (high orbit ion cannon) --> target IP as url (http:\\172.17.19.66)
  * "fire teh lazer" in hoic from multiple computers on same target
  * run sniff-o-matic in target machine --> see traffic from all the ips
  * larger the  number of attacking machines, higher the impact

4. Detecting DoS Attack Traffic Using KFSensor
* KFSensor: windows based honeypot IDS
  * acts as a honeypot: attracts hackers and worms by acting as vulnerable system
  * attacting attacks give more information than firewall and NIDS
  * also diverts attack from critical machines
* set up monitoring on all the ports available --> email alerts

* kali
  * check if port 21 is open
  * nmap -p 21 target_ip
  * SYN flooding on port 21
    * hping -d 100 (each pkt 100 byte) -S (SYN flood) -p 21 (port 21) --flood target_ip

* details of DoS attack in KFSensor including attackers IP

