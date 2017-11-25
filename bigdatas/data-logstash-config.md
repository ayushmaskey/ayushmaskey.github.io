---
layout: bigdata
type: bigdata
published: true
image: images/elk.png
title: logstash.conf
permalink: bigdatas/data-logstash-config
date: 2017
labels:
  - logstash
summary: logstash config file
---

Config file can be separated into three basic components, input, filter and output. They are all defined in JSON format and wrapped around curly braces. As the name suggest, input takes in data and output spits out the data. In the middle the input can be parsed using filters before the passing the data for output. 

#### Input

```config
input {
  stdin { }
  # Receive Cisco ASA logs on the standard syslog UDP port 5140
  udp {
    host => "firewall IP"
    port => 5140
    type => "cisco-asa"
  }
  
}
```

All possible source of input are defined within input braces. This config file takes in input from two different sources. The first one defined is stdin which takes in input from the terminal and waits for user to enter the data into the terminal. This can be used as a simple test to make sure logstash is running as expected. The second input source is defined on UDP port 5140 for firewall IP. Logstash is listening to the port that is defined in the input and but accects traffic from ip defined by host. For this project I will be shipping logs from firewall to UDP port 5140. Here I have tagged traffic coming in port 5140 from firewall as "cisco-asa" using type key. Tagging will come handy when there are multiple source of input.

#### Output

```config
output {
  stdout {
    codec => rubydebug
  }
  file {
    path => "/config-dir/archive/asa-%{+YYYY-MM-dd}.log"
  }
  elasticsearch { hosts => ["elasticsearch:9200"] }
}
```

I have defined  output for all the incoming data. First is stdout with codec rubydebug. As the name suggests, this is used for debugging and very tool keep handy. This visualizes output data into the terminal before we store it. 

#### Filters

Filter in the logstash are the meat of the config file. I have 5 filters defined as of now. All 4 filters are wrapped around conditional statement checking whether the log is from the firewall. We tagged all incoming data as “cisco-asa”. Now we use this tag to verify right filters apply to the data if there are multiple source of input defined.

```
if [type]=="cisco-asa" {
}
```
There are some hand firewall syslog message patterns predefined in [github](https://github.com/logstash-plugins/logstash-patterns-core) by the active community of logstash. We can use those predefined patterns to tease out the messages we are interested in. Between the braces of the conditional statement we define grok with following patterns.
```
grok {
  match => ["message", "%{CISCO_TAGGED_SYSLOG} \
	%{GREEDYDATA:cisco_message}"]
}
```
Grok is a logstash filter plugin that parse through unstructured syslog syslog data into structured data ready for query. Grok uses regular expression to match logs and and convert into structured key value pair. Grok has predefined patterns built-in and also allows us to define custom regular expressions. Here I used predefined patterns of firewall to get the data I need. Github page of the firewall patterns defined regular expression for CISCO_TAGGED_SYSLOG as following

```
CISCO_TAGGED_SYSLOG:  ^<%{POSINT:syslog_pri}> \
	%{CISCOTIMESTAMP:timestamp}\
	( %{SYSLOGHOST:sysloghost})? ?: %%{CISCOTAG:ciscotag}:
```

These patterns are very modular. For example CISCOTAG and CISCOTIMESTAMP used in CISCO_TAGGED_SYSLOG  are regular expression themselves and is defined as
```
CISCOTAG:  [A-Z0-9]+-%{INT}-(?:[A-Z0-9_]+)
CISCOTIMESTAMP:  %{MONTH} +%{MONTHDAY}(?: %{YEAR})? %{TIME}
```
If there is a pattern match, log will be broken down into specific field and if pattern is not matched logstash tags them as -grokparsefailure


The second filter I used is syslog_pri which is built-in plugin like grok and it identifies severity of the log
```
syslog_pri { }
```
Calling a simple line above is enough to tag severity level of the log. These built-in plugin make logstash easy to use while the third filter below that  identifies date field allows us to build custom filters.Together they make logstash very interesting product

```
date {
  match => ["timestamp",
    "MMM dd HH:mm:ss",
    "MMM  d HH:mm:ss",
    "MMM dd yyyy HH:mm:ss",
    "MMM  d yyyy HH:mm:ss"
  ]
}
```

Finally the following grok parses the details of the firewall log into desired output fields.

```config
 grok {
      match => [
        "message", "%{CISCOFW106001}",
        "message", "%{CISCOFW106006_106007_106010}",
        "message", "%{CISCOFW106014}",
        "message", "%{CISCOFW106015}",
        "message", "%{CISCOFW106021}",
        "message", "%{CISCOFW106023}",
        "message", "%{CISCOFW106100}",
        "message", "%{CISCOFW110002}",
        "message", "%{CISCOFW302010}",
        "message", "%{CISCOFW302013_302014_302015_302016}",
        "message", "%{CISCOFW302020_302021}",
        "message", "%{CISCOFW305011}",
        "message", "%{CISCOFW313001_313004_313008}",
        "message", "%{CISCOFW313005}",
        "message", "%{CISCOFW402117}",
        "message", "%{CISCOFW402119}",
        "message", "%{CISCOFW419001}",
        "message", "%{CISCOFW419002}",
        "message", "%{CISCOFW500004}",
        "message", "%{CISCOFW602303_602304}",
        "message", "%{CISCOFW710001_710002_710003_710005_710006}",
        "message", "%{CISCOFW713172}",
        "message", "%{CISCOFW733100}"
      ]
    }
```
One of the pattern I used above is CISCOFW106001, which gets source IP, source port, destination IP, destination ports and flags from the syslog and it defined in github as below
```
CISCOFW106001: %{CISCO_DIRECTION:direction} \
	%{WORD:protocol} \
	connection %{CISCO_ACTION:action} \
	from %{IP:src_ip}/%{INT:src_port} \
	to %{IP:dst_ip}/%{INT:dst_port} \
	flags %{GREEDYDATA:tcp_flags} \
	on interface %{GREEDYDATA:interface}
```
As with most pattern defined in cisco grok page in github, this pattern was constructed using smaller patterns 

```
CISCO_DIRECTION: Inbound|inbound|Outbound|outbound
CISCO_ACTION: Built|Teardown|Deny|Denied|denied|requested \
	|permitted|denied by ACL|discarded|est-allowed \
	|Dropping|created|deleted
```

 I am not very good with regular so it was trial and error for me. I used a pattern in my config file to see if it gave me any useful output. This is when **--rm** option when creating logstash came in handy. Also the output to console using ruby debug gave me quick view of the expected output. I used many pattern which gave me structure data from the gibberish that was syslog. Without networking or security background I don’t understand all the pieces of information that grok structured for me but I understand enough to make me to use some of the information for the project. 

Some of the data I will be using for the project 
 * source IP
 * source port
 * destination IP 
 * destination ports
 * size of the packets
 * whether the traffic was blocked or not
 * interface the traffic passed through
 * off hour traffic
 * whether the traffic was initialed from inside or outside



