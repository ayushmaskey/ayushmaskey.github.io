---
layout: bigdata
type: bigdata
published: true
image: images/cotton-square.png
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
capture <filename1> interface inside match ip 192.168.10.10 255.255.255.255 203.0.113.3 255.255.255.255
capture <filename2> interface outside match ip 192.168.10.10 255.255.255.255 203.0.113.3 255.255.255.255
{% endhighlight %}

Getting down to the specifics is useful when troubleshooting specific issue with a machine but for the project we need capture all traffic from all machines on all interfaces. Tweaking the above command slightly can achieve this.

{% highlight bash %}
capture <filename1>interface inside match ip any any
capture <filename2>interface outside match ip any any
{% endhighlight %}

We can monitor the data collection using following commands
{% highlight bash %}
show capture                	#shows number of packets captured in each interface
show capture <filename1>        #shows all the data capture in inside interface
show capture <filename2>        #shows all the data captured in outside interface
{% endhighlight %}

The raw data captured can saved in the tfpt sever using following commands
{% highlight bash %}
copy /pcap capture:<name1> tftp://<server-ip-address>		# move data to tftp server
no capture <filename1>						#stop capture
no capture <filename2>
clear capture							# clear firewall flash cache
{% endhighlight %}

Now that we have the files in our tftp server, we can start writing a simple python script to move pcap data generated from firewall into a sqlite3 database. 

{% highlight py %}
import sqlite3
from scapy.all import rdpcap
from datetime import datetime
from pprint import pprint

db = '../db/firewall.db'

conn = sqlite3.connect(db) 
c = conn.cursor()

capin = "../tftp/in"
capout = "../tftp/out"

inside_tbl = 'inside_tbl'
outside_tbl = 'outside_tbl'

internal_tbl_cleanup = 'inside_ip_warehouse'
external_tbl_cleanup = 'outside_ip_warehouse'

# create table for pcp data
def create_table(tbl_name):
	sql = 'create table if not exists ' + tbl_name + \
		'(sDate datetime, eth_dst varchar(17), eth_src varchar(17), eth_type varchar(4), \
		ip_ver smallint, ip_ihl smallint, ip_tos varchar(5), ip_len int, ip_id int, ip_flags varchar(3), \
		ip_frag smallint, ip_ttl int, ip_proto varchar(5), ip_chksum varchar(6), ip_src varchar(15), ip_dst varchar(15), \
		tcp_sPort varchar(5), tcp_dPort varchar(5), tcp_seq int, tcp_ack int, tcp_dataofs int, tcp_reserved int, tcp_flags varchar(3), \
		tcp_window int, tcp_chksum varchar(6), tcp_urgptr int)'
	c.execute(sql)

# create table of internal and external ip sorted warehouse
def create_ip_warehouse_tbl(tbl_name):
	sql = 'create table if not exists ' + tbl_name + \
			'(sDate datetime, ip_src varchar(15), tcp_sPort varchar(5), ip_dst varchar(15), tcp_dPort varchar(5), \
			ip_len int, ip_id int, ip_flags varchar(3), ip_proto varchar(5) ) '
	c.execute(sql)

# all pcap data into list of tuples
def pcap_into_list_of_tuples(file_name):
	pkts = rdpcap(file_name)
	row = []
	tuples = ()

	for pkt in pkts:
	    timestamp = datetime.fromtimestamp(pkt.time).strftime('%Y-%m-%d %H:%M:%S')
	   
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

	    tuples = (timestamp, eth_dst, eth_src, eth_type, ip_ver, ip_ihl, ip_tos, ip_len, ip_id, ip_flags, ip_frag, ip_ttl, ip_proto, ip_chksum, ip_src, ip_dst, tcp_sPort, tcp_dPort, tcp_seq, tcp_ack, tcp_dataofs, tcp_reserved, tcp_flags, tcp_window, tcp_chksum, tcp_urgptr)
	    row.append(tuples)
		# print(pkt.id)
	return row

# insert pcap data into sqlite3
def insert_generic_table(pLists, tbl_name):
	    sql = 'insert into ' + tbl_name + ' values (?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?,?, ?, ?, ?, ?, ?, ?, ?, ?, ?)'
	    c.executemany(sql, pLists)
	    conn.commit()

# convert pcap to list of tuples and then into sqlite3
def pcap_into_db(file_name, tbl_name):
	pcap_into_lists = pcap_into_list_of_tuples(file_name)
	insert_generic_table(pcap_into_lists, tbl_name)

# move all 10. ip into internal and all else into external column
def sort_col_by_internal_external(src_tbl, dst_tbl):
	src_rows, dst_rows, dst_tuple = [], [], ()

	sql = 'select sDate, ip_src, tcp_sPort, ip_dst, tcp_dPort, ip_len, ip_id, ip_flags, ip_proto from ' + src_tbl
	src_rows = c.execute(sql)

	for src_row in src_rows:
		if(src_row[1][:3] == '10.' or src_row[1][:3] == '192' or src_row[1][:3] == '172' or src_row[1] == '72.253.69.200' ):
			dst_tuple = (src_row[0], src_row[1], src_row[2], src_row[3], src_row[4], src_row[5], src_row[6], src_row[7], src_row[8])
		else:
			dst_tuple = (src_row[0], src_row[3], src_row[4], src_row[1], src_row[2], src_row[5], src_row[6], src_row[7], src_row[8])
		dst_rows.append(dst_tuple)
	
	sql = 'insert into ' + dst_tbl + ' values (?, ?, ?, ?, ?, ?, ?, ?, ?)'
	c.executemany(sql, dst_rows)
	conn.commit()

# drop one table
def drop_table(tbl_name):
	sql = 'drop table ' + tbl_name
	c.execute(sql)

# drop all table
def drop_all_table():
	drop_table(inside_tbl)
	drop_table(outside_tbl)
	drop_table(internal_tbl_cleanup)
	drop_table(external_tbl_cleanup)

# create one table
def create_all_tbls():
	create_table(inside_tbl)
	create_table(outside_tbl)
	create_ip_warehouse_tbl(internal_tbl_cleanup)
	create_ip_warehouse_tbl(external_tbl_cleanup)

# all pcap data in sqlite3
def all_pcap_db(): 
	pcap_into_db(capin, inside_tbl)
	pcap_into_db(capout, outside_tbl)

def warehousing():
	sort_col_by_internal_external(inside_tbl, internal_tbl_cleanup)
	sort_col_by_internal_external(outside_tbl, external_tbl_cleanup)

# get th script started
def main():
	create_all_tbls()
	all_pcap_db()
	warehousing()

drop_all_table()

main()

def test_main():
	sort_col_by_internal_external()

#test_main()
"""
S: SYN - 3 way handshake
A: ACK -success
F: FIN - finish
R: RESET - denied
P: PUSH - similar to urgent
U: URGENT - process this packet before any other
E: ECE - ECN capable
C: CWR - recieved packet with ECE flag
.: ACK
"""


c.close()
conn.close()
{% endhighlight %}

