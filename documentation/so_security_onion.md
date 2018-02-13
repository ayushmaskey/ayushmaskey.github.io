## Security Onion
 * [security_onion](#security-onion)
  * [overview](#overview)
  * [services running](#services-running)
  * [so update](#so-update)
  * [interfaces](#interfaces)
  * [docker containers](#docker-containers)
  * [so_firewall](#so-firewall)
  * [access components](#access-components)
  * [config files](#config-files)
  * [log files](#log-files)
 * [SGUIL](#squil)
 * [SQUERT](#squert)
 * [ossec](#ossec)
 * [beat](#beat)
 * [BRO](#bro)
 * [SNORT](#snort)
 * [LOGSTASH](#logstash)
 * [ELASTICSEARCH](#elasticsearch)
 * [KIBANA](#kibana)
 * [pulled port](#pulled-pork)
 * [banyard2-1](#banyard2-1)
 * [pf_ring](#pf_ring)
 * [CapMe](#capme)
 * [apache](#apache)
 * [my-sql](#my-sql)
 
## security_onion

## overview 
* linux distro build on ubuntu
* includes tools like snorby, 
## services running
```bash
sudo sostat |less
```
data source available from elastic search
```
curl 'localhost:9200/_cat/indices?v'
```

## [so update](https://github.com/Security-Onion-Solutions/security-onion/wiki/Upgrade)
```
#byobu before updating
# install byobu
sudo apt-get install byobu
# enable byobu
byobu-enable
# you're now ready to update


#ubuntu and security onion
sudo soup
#snort/suricata rules
sudo rule-update
#bro
sudo nsm_sensor_ps-restart --only-bro

#update pf_ring 
sudo apt-get update ; sudo apt-get install securityonion-pfring-module ; sudo apt-get dist-upgrade

#if snort dails after update
sudo apt-get install --reinstall securityonion-pfring-module
```

## services
* squil-server
* ossec_agent
* bro
* betsniff-ng
* pcap_agent
* snort_agent-1
* snort-1
banyard2-1

## interfaces
docker0 --> elk docker
eth0 --> management (lot of incoming and outgoing)
eth1 --> some incoming, 0 outgoing
eth2 --> 0, 0
eth3 --> most active incoming, 0 outgoing
eth4 --> some incoming, 0 outgoing
eth5 --> 0, 0
eth6 --> 0, 0
eth7 --> 0, 0
eth8 --> 0, 0
eth9 --> 0, 0
lo --> 17.2GB in, 17.2GB out

## docker containers 
**so-curator**
**so-elastalert**
**so-kibana**
**so-logstash**
**so-elasticsearch**
**so-domainstats**
**so-freqserver** 

## [so_firewall](https://github.com/Security-Onion-Solutions/security-onion/wiki/firewall)
```
sudo ufw  allow proto tcp from ip_address to any port 22,443,7734,514,5601
sudo ufw  allow proto udp from ip_address to any port 1514

sudo ufw delete allow proto tcp from ip_address to any port 22,443,7734,514,5601
sudo ufw delete allow proto udp from ip_address to any port 1514

sudo ufw status

#
5601: Kibana
1514: ossec data collection
22: ssh
443: https
514: 
444: 
7734: 
```

## access components

https://localhost/apt/kibana

Snort GUI
web interface: https://localhost/squert
desktop client: [Download squil client](https://bammv.github.io/sguil/index.html) --> install gui based on tcl/tk --> point to security onion machine --> login

[SO Best Practives](https://github.com/Security-Onion-Solutions/security-onion/wiki/Best-Practices)
## changes
> sensor.conf
```bash
grep ENABLED /etc/nsm/server-eth0/sensor.conf
disable PRADS, PADS and sancp and http_agent just coz
```
> snort.conf
```bash
/etc/nsm/server-eth0/snort.conf
ipvar EXTERNAL_NET !$HOME_NET
```

## config files
```
# ELK
/etc/kibana/kibana.yml

/opt/elastic/src/etc/kibana
/opt/elastic/src/configfiles
/opt/elastic/src/etc/elastalert/rules
/opt/elastic/src/etc/curator/config

/etc/nsm/pulledpork
/etc/nsm/administration.conf
/etc/nsm/securityonion.conf

/etc/logstash
```
## /etc/nsm/rules
```
WHITE_LIST_PATH
BLACK_LIST_PATH
RULE_PATH
SO_RULE_PATH
PREPROC_RULE_PATH
```
## log files
```
#snort logs - giberish
/nsm/sensor_data/host3-eth3/dailylogs

#bro logs - separate logs for each type of data (ssh, smtp, edp etc)
/nsm/bro/logs
```


## [SGUIL](https://bammv.github.io/sguil/index.html)
* [github](https://github.com/bammv/sguil)
* should not change time. It should be in UTC for updates
* ctrl + click on alert ID
* right click on IP --> quick query --> query Sancp Table --> Query DestIP 
	* my sql / db server: table 'securityonion.db.sancp does not exisits
	* need to setup mysql

## [SQUERT](http://www.squertproject.org/)
* [github](https://github.com/int13h/squert)

## [ossec](http://ossec-docs.readthedocs.io/en/latest/manual/agent/agent-management.html)
```bash
#add agent to server
sudo /var/ossec/bin/manage_agent
# add agent 
A --> name, IP, 8 digit Number
E --> 8 digit number --> copy key

#install in client
install .exe --> IP of server --> 8 digit number
manage --> restart

#firewall rule to allow port 1514
```

## [beat](https://logz.io/blog/windows-event-log-analysis/)
* copy beats folder to c:\
```powershell
PowerShell.exe -ExecutionPolicy Unrestricted -File .\install-beat.ps1
```

* onion server
```bash
so-allow
option - b
ip of client
```


## [BRO](https://www.bro.org/)
* [github](https://github.com/bro)

## [SNORT](https://snort.org/)
* [github](https://github.com/snortadmin/snort3)

## [LOGSTASH](https://www.elastic.co/products/logstash)
* [logstash plugins](https://github.com/logstash-plugins/logstash-output-elasticsearch)

> /etc/logstash/conf.d/  


## [ELASTICSEARCH](https://github.com/elastic/elasticsearch)
* [github](https://github.com/elastic/elasticsearch)

## [KIBANA](https://www.elastic.co/products/kibana)
* [github](https://github.com/elastic/kibana)
 
## [pulled pork](#https://github.com/shirkdog/pulledpork)
* downloaded at 7:01 UTC everyday
* using https://evergingthreats.net

## [banyard2-1]
* [github](https://github.com/firnsy/barnyard2)
## [pf_ring]
* [github](https://github.com/ntop/PF_RING)
## [CapMe]
* [github](https://github.com/int13h/capme)
* [SO implementation](https://github.com/Security-Onion-Solutions/security-onion/wiki/CapMe)
* view pcap rendered with bro
* Pivot from squert to CapMe
## [apache]

## [my-sql]
* [mysql turing](https://github.com/Security-Onion-Solutions/security-onion/wiki/MySQLTuning)
* my sql / db server: table 'securityonion.db.sancp does not exisits
* /etc/nsm/server-eth0/sensor.conf --> enable PRADS for mysql