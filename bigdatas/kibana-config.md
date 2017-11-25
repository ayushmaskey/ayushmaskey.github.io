---
layout: bigdata
type: bigdata
published: true
image: images/elk.png
title: kibana dashboard
permalink: bigdatas/kibana-config
date: 2017
labels:
  - kibana
summary: kibana dashboard
---

One the logstash is getting data and dumping them into elasticsearch, we are able to view those data in kibana. Kibana web interface is on port 5601 of the docker host as defined when kibana container was initially created. The management port will look for list of field that have been recorded in elasticsearch. Since we used logstash to populate elasticsearch, all the fields will be populated with prefix **logstash***. Management page will then show all fields that have been defined in logstash config. I have 84 fields but I will only a small subset of the project.

I know I want a snapshot of ongoing traffic flow. Looking at the options in kibana creating a dashboard with relevant information would probably be my best bet. The dashboard will hopefully give me enough information that will help be identify security vulnerabilities. Dashboard in Kibana is made of multiple visuals which can be created in visualize tab. Visuals are created using data in the discover tab. Raw data from firewall is processed in logstash filter and to create structured data which is saved in elasticsearch. That structured data is available in kibana discover tab as raw data.

Firewall generates more that 2.5Gb of data for each working day and weekends generate half the traffic. It is quite interesting that only half of traffic generated on any given day can be directly attributed to aprrox. 250 users browsing internet during work hours. The other half is generated even when there is no user activity. This is scary and satisfying at the same time. Scary because why would there be so much traffic generated when there are no users and satisfying because blocking social media, youtube and Korean drama has had some positive effects. It probably gives some insight into users at my work. They are health professionals and do not care much about internet beyond social media and videos.

Going through 2.5Gb of data everyday is not possible so the best option is get some insight into what kind of traffic is being genrated. This can be done in kibana visualize tab. I saved a search in disconvery tab with source and destination IP and port and use bar gram with count on y-axis, aggregating each term in saved seach one at the time. After quick summary and count, it looks like DNS query is one of the biggest traffic generator. There are two kinds of DNS query passing through firewall, IP 8.8.8.8 on UDP port 53 and machines in DMZ querying LDAP inside the network. DNS query is expected but I was definitely suprised by the number of queries. I can safely ignore these traffic from further analysis.

Besides DNS query, I will be ignoring the following traffic using elasticsearch query DLS

* ignore

|source machine   | Port | destination machine | Reason  |
|-----------------|:----:|:-------------------:|--------:|
|LDAP		  |53    |8.8.8.8      	       |DNS query|
|DMZ 		  |53    |LDAP      	       |DNS query|






