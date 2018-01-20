---
layout: essay
type: essay
published: true
title: snort
date: 2017-01-11
labels:
  - ICS425
  - snort
---

Intrusion detection system (IDS) are hardware or software that monitor suspicious traffic. There are two general types of IDS, network based intrusion detection system (NIDS) and host based detection system (HIDS). NIDS are deployed in specific area of the network to monitor all incoming and outgoing traffic. Some of the popular open source NIDS are snort, suricata, ossec, bro and security onion. HIDS are installed in individual machines and they protect individual devices from malicious traffic. Together HIDS and NIDS create layers of security that protect a network from wide variety of threats and attacks. These layers are important to catch threat that may have been missed by other layers of security.
Snort is open source NIDS developed by sourcefire that perform real-time traffic analysis and packet logging. Traffic passing though the snort are analyzed against set of rule defined by sourcefire which can be complimented with user defined rules. Snort is a reliable and trusted NIDS that can be deployed in an organization as one of the layers of security.
Installing snort from source in Ubuntu was fairly straight forward process. It was as simple as downloading the latest tar for daq and snort and compiling them. Once a files and permissions were in place, I was going through some of the preinstalled config files and they seem comprehensive. Since I am not hosting a mail server or a web server in my personal computer, I removed them those rules from the config file. I had to tweak few other rules to match my home network.
Snort like most IDS, stores signatures of known malicious traffic. As network traffic passes through snort, signature of each packet is compared to that of known malicious traffic. If and when there is match, action taken by snort depends on rules set by the user. Snort can be used for logging all packets passing through, or it can be used as intrusion prevention system (IPS) or simply send an alert message. 
For testing, I created an alert in local.rules file. It was a simple alert for incoming and outgoing icmp packets. I ran snort in terminal which is basic packet sniffer mode. I pinged the computer running snort from other machines and lo and behold, snort was displaying those traffic in the terminal. I was happy to see snort running successfully. When I stopped snort, it gave a summary of all the traffic passing through my machine in that time frame and icmp was just 0.5% of the total traffic. Snort was capturing all traffic in my network interface but icmp traffic was the only type displayed because, that is the only rule I had. It was alarming that without any browsers open and no user activity, snort was able to capture so much data flowing though my computer. After closer look at the resulting stats, over third those packets were ARP which can be safely ignored. There were lot of TCP and UDP packets and some bad checksum. This is when I realized, I need to be running IDS in my home network.


how does IDS detect? signature based, anomaly based

snort rules
what I found

snort is a part of security onion.


References
https://www.lifewire.com/introduction-to-intrusion-detection-systems-ids-2486799 
https://snort.org 
https://www.techrepublic.com/article/solutionbase-use-snort-to-find-out-whos-trying-to-break-in-to-your-network/ 


https://www.upguard.com/articles/top-free-network-based-intrusion-detection-systems-ids-for-the-enterprise 
http://techgenix.com/why_is_a_firewall_alone_not_enough_what_are_idses_and_why_are_they_worth_having/ 
http://techgenix.com/hids_vs_nids_part1/
http://resources.infosecinstitute.com/snort-rules-workshop-part-one/ 


