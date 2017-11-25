---
layout: bigdata
type: bigdata
published: true
image: images/sqlite3.png
title: cisco asa to sqlite3
permalink: bigdatas/data-asa-sqlite3
date: 2017
labels:
  - cisco asa 5510
  - sqlite3
  - python3
summary: asa data collection - sqlite3.
---

Capturing data from firewall to a database is fairly straight-forward process. For this project I am using cisco asa 5510 firewall but this process should work for any firewall regarless of brand or model. Ofcourse the actual command will be different for each brand of firewall. I will setup a simple tftp server in ununtu machine and to save the data captured from the firewall.

#### tftp server
To install and test tftp server in ubuntu, two command below are sufficient. Further details on the tftp server can be found in [ubuntu community page](https://help.ubuntu.com/community/TFTP). 

{% highlight bash %}
sudo apt-get install tftp-hpa
sudo service tftp-hpa status
{% endhighlight %}

#### cisco firewall
Data can be collected from asa in one of two ways, ssh into the firewall or gui. I will be using ssh since it is easier to automate continuous flow of data. The first step is to make sure firewall is accepting ssh connections.
{% highlight bash %}
ssh username@firewall_ip	# ssh into firewall
enable				# priviledge mode in firewall
{% endhighlight %}

Once inside the firewall, we can capture traffic data filtered by firewall interface, internal machine and/or external server. Below are the command to capture all traffic from my machine to a specific ip in the inside and outside interface of firewall.
{% highlight bash %}
capture <filename1> interface inside match ip \
192.168.10.10 255.255.255.255 203.0.113.3 255.255.255.255

capture <filename2> interface outside match ip \
192.168.10.10 255.255.255.255 203.0.113.3 255.255.255.255
{% endhighlight %}

Getting down to the specifics is useful when troubleshooting specific issue with a machine but for the project we need capture all traffic from all machines on all interfaces. Tweaking the above command slightly can achieve this.

{% highlight bash %}
capture <filename1>interface inside match ip any any
capture <filename2>interface outside match ip any any
{% endhighlight %}

We can monitor the data collection using following commands
{% highlight bash %}
show capture                	# num of pkts in each interface
show capture <filename1>        # pkts in inside interface
show capture <filename2>        # pkts in outside interface
{% endhighlight %}

The raw data captured can saved in the tfpt sever using following commands
{% highlight bash %}
copy /pcap capture:<name1> tftp://<server-ip-address>
no capture <filename1>	
no capture <filename2>
clear capture
{% endhighlight %}

Now that we have the files in our tftp server, we can start writing a simple python script to move pcap data generated from firewall into a sqlite3 database. 

#### create table
```python
import sqlite3

def create_table(tbl_name):
  sql = 'create table if not exists ' + tbl_name + \
    '(sDate datetime, eth_dst varchar(17), eth_src varchar(17), \
    eth_type varchar(4), ip_ver smallint, ip_ihl smallint, \
    ip_tos varchar(5), ip_len int, ip_id int, ip_flags varchar(3), \
    ip_frag smallint, ip_ttl int, ip_proto varchar(5), \
    ip_chksum varchar(6), ip_src varchar(15), ip_dst varchar(15), \
    tcp_sPort varchar(5), tcp_dPort varchar(5), tcp_seq int, \
    tcp_ack int, tcp_dataofs int, tcp_reserved int, tcp_flags varchar(3), \
    tcp_window int, tcp_chksum varchar(6), tcp_urgptr int)'
  c.execute(sql)
```

#### pcap file into list of tuples ready to insert into sqlite
```
from scapy.all import rdpcap
from datetime import datetime as dt

def pcap_into_list_of_tuples(file_name):
  pkts = rdpcap(file_name)
  row = []
  tuples = ()

  for pkt in pkts:
    timestamp = dt.fromtimestamp(pkt.time).strftime('%Y-%m-%d %H:%M:%S')
	   
    eth_dst = pkt.sprintf("%Ether.dst%")
    eth_src = pkt.sprintf("%Ether.src%")
    eth_type = pkt.sprintf("%Ether.type%")
	    
    ip_ver = pkt.sprintf("%IP.version%")
    ip_ihl = pkt.sprintf("%IP.ihl%")
    ip_tos = pkt.sprintf("%IP.tos%")
    ip_len = pkt.sprintf("%IP.len%")
    ip_id = pkt.sprintf("%IP.id%")
    ip_flags = pkt.sprintf("%IP.flags%")
    ip_frag = pkt.sprintf("%IP.frag%")
    ip_ttl = pkt.sprintf("%IP.ttl%")
    ip_proto = pkt.sprintf("%IP.proto%")
    ip_chksum = pkt.sprintf("%IP.chksum%")
    ip_src = pkt.sprintf("%IP.src%")
    ip_dst = pkt.sprintf("%IP.dst%")

    tcp_sPort = pkt.sprintf("%TCP.sport%")
    tcp_dPort = pkt.sprintf("%TCP.dport%")
    tcp_seq = pkt.sprintf("%TCP.seq%")
    tcp_ack = pkt.sprintf("%TCP.ack%")
    tcp_dataofs = pkt.sprintf("%TCP.dataofs%")
    tcp_reserved = pkt.sprintf("%TCP.reserved%")
    tcp_flags = pkt.sprintf("%TCP.flags%")
    tcp_window =  pkt.sprintf("%TCP.window%")
    tcp_chksum = pkt.sprintf("%TCP.chksum%")
    tcp_urgptr = pkt.sprintf("%TCP.urgptr%")

    tuples = (timestamp, eth_dst, eth_src, eth_type, ip_ver, \
	ip_ihl, ip_tos, ip_len, ip_id, ip_flags, ip_frag, ip_ttl, \
	ip_proto, ip_chksum, ip_src, ip_dst, tcp_sPort, tcp_dPort, \
	tcp_seq, tcp_ack, tcp_dataofs, tcp_reserved, tcp_flags, \
	tcp_window, tcp_chksum, tcp_urgptr)
    row.append(tuples)
	
  return row
```


#### insert list of tuples into sqlite3
````
def insert_generic_table(pLists, tbl_name):
  sql = 'insert into ' + tbl_name + ' values
    (?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, \
    ?, ?, ?,?, ?, ?, ?, ?, ?, ?, ?, ?, ?)'
  c.executemany(sql, pLists)
  conn.commit()
````

#### TCP Flags
* S: SYN - 3 way handshake
* A: ACK -success
* F: FIN - finish
* R: RESET - denied
* P: PUSH - similar to urgent
* U: URGENT - process this packet before any other
* E: ECE - ECN capable
* C: CWR - recieved packet with ECE flag
* .: ACK



I got firewall traffic imported into the database and it was time to automate the process when I learned about [ELK stack](./dat-asa-elk.md). ELK stack consists of elasticsearch, logstash and kibana. I wanted to give it a try since ELK stack was build to parse logs. I thought I would come back to python and sqlite since I am confortable relational databases. However, after using ELK stack for a day, I hesitate to continue using relational database for log parse.

