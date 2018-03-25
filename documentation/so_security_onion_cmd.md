## Security Onion

Commands
  * [automating setup](#automating-setup)
  * [services](#services)
  * [config](#config)
  * [new user](#new-user)
  * [firewall](#firewall)
  * [update](#update)
  * [docker containers](#docker-containers)
  * [tools](#tools)
  * [config files](#config-files)
  * [log files](#log-files)
  * [data](#data)
  * [rules](#rules)
  * [alerts](#alerts)


 
## [automating setup](https://github.com/Security-Onion-Solutions/security-onion/wiki/Automating-Setup) 
* automating setup ` sosetup `
* $location `/usr/share/securityonion/sosetup.conf`
* make a copy before ending `cp $location ~ && nano ~/sosetup.conf`
* another option ` sosetup -w ~/sosetup.conf ` and answer questions
* testing / running setup ` sudo sosetup -f ~/sosetup.conf ` 


## services

* general statistics ` sudo sostat | less `

* all services
```bash
sudo services nsm status
sudo service nsm start | stop | restart
```

* squil-server 
```bash 
sudo nsm_server_ps-status
sudo nsm_server_ps-start | stop | restart
```

* sensors
```bash
sudo nsm_sensor_ps-* -?
sudo nsm_sensor_ps-restart
```

* bro
```bash
sudo nsm_sensor_ps-status --only-bro
sudo nsm_sensor_ps-stop --only-bro
```

* ossec_agent
* betsniff-ng
* pcap_agent
* snort_agent-1
* snort-1
* banyard2-1

## config

* sensor config file `bash /etc/nsm/$host-interface/snort.conf`
* update 
```bash 
$HOME_NET 
EXTERNAL_NET
```

* bro config  file ` /opt/bro/etc/network.cfg`

* create IDS alert ` curl http://testmyids.com `

* sguil -->  GUI

* squert --> https://hostname

* squil `/etc/nsm/securityonion.conf` change `DAYSTOKEEP: 30 (default)`

## new user 
add user ` sudo nsm_server_user-add `

## [firewall](https://github.com/Security-Onion-Solutions/security-onion/wiki/firewall)
> new firewall - only 22 open by default

* automate `so-allow`

#### [old firewall](https://github.com/Security-Onion-Solutions/security-onion/wiki/Firewall-old)
* allow
```bash
sudo ufw  allow proto tcp from ip_address to any port 22,443,7734,514,5601
sudo ufw  allow proto udp from ip_address to any port 1514
```
* delete
```bash
sudo ufw delete allow proto tcp from ip_address to any port 22,443,7734,514,5601
sudo ufw delete allow proto udp from ip_address to any port 1514
```
* firewall status `sudo ufw status`

* add rule to docker iptable
```bash
sudo iptables -I DOCKER-USER ! -i docker0 -o docker0 -s ip_address -p tcp --dport 5044 -j ACCEPT
```

* view rule from docker iptable `sudo iptables -L DOCKER-USER rule_num`

* remove rule from docker iptable `sudo iptables -D DOCKER-USER rule_num`

* port number: app
```bash
5601: Kibana
1514/udp: ossec
22: ssh
443: https/ squert/ CapMe / Kibana
514: syslog
9200: elasticsearch
444: 
7734: sguil client
7736: sguil sensor
4505: salt??
4506: salt??
```

## [update](https://github.com/Security-Onion-Solutions/security-onion/wiki/Upgrade)

* byobu --> necessary for updates
  * install byobu `sudo apt-get install byobu`
  * enable byobu `byobu-enable`
* ubuntu and security onion `sudo soup`
* snort/suricata rules `sudo rule-update`
* update pf_ring 
```bash
sudo apt-get update 
sudo apt-get install securityonion-pfring-module 
sudo apt-get dist-upgrade
```
* if snort fails after update `sudo apt-get install --reinstall securityonion-pfring-module`


## [alerts](https://github.com/Security-Onion-Solutions/security-onion/wiki/ManagingAlerts)


## docker containers 
```bash
so-curator
so-elastalert
so-kibana
so-logstash
so-elasticsearch
so-domainstats
so-freqserver 
```


## tools
* kibana `https://localhost/apt/kibana`
* [Snort GUI](https://bammv.github.io/sguil/index.html)
* squert `https://localhost/squert`
* es indices `curl 'localhost:9200/_cat/indices?v'`



## [config files](https://github.com/Security-Onion-Solutions/security-onion/wiki/Cheat-Sheet)

* general `/etc/nsm/securityonion.conf`
* sensor `/etc/nsm/<host-eth0>/sensor.conf`
```bash
grep ENABLED /etc/nsm/server-eth0/sensor.conf
disable PRADS, PADS and sancp and http_agent just coz
```
* maintenance `/etc/cron.d/`
* snort `/etc/nsm/<host-eth0>/snort.conf` `ipvar EXTERNAL_NET !$HOME_NET`
* bro `/opt/bro`
  * bro config `/opt/bro/etc`
  * bro policy `/opt/bro/share/bro/site/local.bro`
* syslog-ng `/etc/syslog-ng/syslog-ng.conf`
* ossec `/var/ossec/etc/ossec.conf`
* squil `/etc/nsm/securityonion/sguid.conf`
  * squil email `/etc/nsm/securityonion/sguid.email`
* pulled pork `/etc/nsm/pulledpork/pulledpork.conf`
* something `/nsm/administration.conf`

## log files
* bro `/nsm/bro/logs/current/stderr.log`
* ossec `/var/ossec/logs/ossec.log`
* sensor `/var/log/nsm/<host-eth0>/snort0-n.log, banyard2-n.log, netsniff-ng.log`

## data
* packets `/nsm/sensor_data/<host-eth0>/dailylogs`
* alerts `/nsm/sensor_data/<host-eth0>`
* bro (archive) `/nsm/bro/logs/yyyy-mm-dd`
* bro (current) `/nsm/bro/logs/current`
* bro extracted files `/nsm/bro/extracted`

## rules 
* IDS (downloaded) `/etc/nsm/rules/downloaded.rules`
* IDS (local) `/etc/nsm/rules/local.rules`


```bash
WHITE_LIST_PATH
BLACK_LIST_PATH
RULE_PATH
SO_RULE_PATH
PREPROC_RULE_PATH
```




* ELK
```bash
/etc/kibana/kibana.yml

/opt/elastic/src/etc/kibana
/opt/elastic/src/configfiles
/opt/elastic/src/etc/elastalert/rules
/opt/elastic/src/etc/curator/config

/etc/logstash
```




