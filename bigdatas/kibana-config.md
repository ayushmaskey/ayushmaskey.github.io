---
layout: bigdata
type: bigdata
published: true
image: images/elk.png
title: logstash.conf
permalink: bigdatas/data-kibana-config
date: 2017
labels:
  - kibana
summary: kibana configuration
---

One the logstash is getting data and dumping them into elasticsearch, we are able to view those data in kibana. Kibana web interface is on port 5601 of the docker host as defined when kibana container was initially created. The management port will look for list of field that have been recorded in elasticsearch. Since we used logstash to populate elasticsearch, all the fields will be populated with prefix **logstash**. Management page will then show all fields that have been defined in logstash config. I have 84 fields but I will only a small subset of the project.

My goal is to create a dashboard with relevant information that will help be identify security vulnerabilities. Dashboard in Kibana is made of multiple visuals in visualize tab  which in turn can build by selecting the fields in discover tab.

Starting with the discover tab, I first created a filter with basic fields I am familiar with. 

Discover, 
Visualize
dashboard



