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
Intrusion detection system (IDS) are hardware or software that monitor suspicious traffic. There are two general types of IDS, network based intrusion detection system (NIDS) and host based detection system (HIDS). NIDS are deployed in specific area of the network to monitor all incoming and outgoing traffic. Some of the popular open source NIDS are snort, suricata and bro. HIDS, on other hand, are installed in individual machines and monitor changes and compromises of the local files. Together HIDS and NIDS constitute layers of security that protect a network from wide variety of threats and attacks. It is essential to include HIDS and NIDS in the comprehensive security architecture, and may help catch threats that may have been missed by other layers of security.

Snort is open source NIDS developed by sourcefire that perform real-time traffic analysis and packet logging. Traffic passing through the snort are analyzed against set of rule defined by sourcefire which can be complimented with user defined rules. Snort is a reliable and trusted NIDS that is deployed in organizations as one of the layers of security. Installing snort from source in Ubuntu was fairly straightforward process. It was as simple as downloading the latest tar for daq and snort and compiling them. Once a files and permissions were in place, I was going through some of the preinstalled config files and they seem comprehensive. Since I am not hosting a mail server or a web server in my personal computer, I removed them those rules from the config file. I had to tweak few other rules to match my home network.

Snort like most IDS uses signature based and anomaly based techniques to detect malicious traffic. For signature based detection, snort stores signatures patterns of known malicious traffic which needs to be updated frequently. As network traffic passes through snort, signature of each packet is compared to that of known malicious traffic. If and when there is match, action is taken by snort which depends on rules set by the user. Snort can be used for logging all packets passing through, or it can be used as intrusion prevention system (IPS) or simply send an alert message.

For anomaly based detection, snort learns about normal traffic pattern of a network and applies heuristics to find traffic anomaly. This assumes network has not been compromised before the deployment of snort. Snort may learn malicious traffic as normal if there is malicious traffic already present but the signature based detection may flag those traffic if those patterns are available in snort database. On the other hand, a zero day breach may not be detected by signature based method since zero day vulnerability patterns are obviously not available in snort database. In this scenario, anomaly based method may successfully detect this new malicious traffic.

For testing, I created an alert in local.rules file as described in installation documentation. It was a simple alert for incoming and outgoing icmp packets. I ran snort in terminal which is basic packet sniffer mode. I pinged the computer running snort from other machines and lo and behold, snort was displaying those traffic in the terminal. I was happy to see snort running successfully. When I stopped snort, it gave a summary of all the traffic passing through my machine in that time frame and icmp was only 0.5% of the total traffic. Snort was capturing all traffic in my network interface but icmp traffic was the only type displayed because that is the only rule I had. It was alarming that without any browsers open and no user activity, snort was able to capture so much data flowing through my computer. After closer look at the resulting stats, over third those packets were ARP which can be safely ignored. There were lot of TCP and UDP packets and some bad checksum. This is when I realized, I need to be running IDS in my home network.

Writing my own rules is very interesting challenge but I do not have enough network and security acumen to write a comprehensive rules for snort. After a quick search I came across crowdsource rules maintained by security community. Rather than reinvent the wheel, I deployed rules provided by snort in conjunction with crowdsource rules. After letting it run for few days and logging each piece of information, there were lot of logs generated. Most of the traffic seems to be DNS lookup and google ads. There were some traffic going to xerox network and I do not have xerox printer or any other xerox product installed. There were traffic to ip addresses on weird port number but i do not have enough understanding to classify it as legitimate or not. While snort makes capturing traffic is easy, understanding those traffic to create actionable item takes better understanding and experience.


References
https://www.lifewire.com/introduction-to-intrusion-detection-systems-ids-2486799 
https://snort.org 
https://www.techrepublic.com/article/solutionbase-use-snort-to-find-out-whos-trying-to-break-in-to-your-network/ 
https://www.upguard.com/articles/top-free-network-based-intrusion-detection-systems-ids-for-the-enterprise 

