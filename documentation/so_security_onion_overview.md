
# [Security Onion Introduction](https://github.com/Security-Onion-Solutions/security-onion/wiki/IntroductionToSecurityOnion)

Network Security Monitoring
 * monitoring network for security related events
 * proactive or reactive
   * proactive: identify vilnerabilities, expiring certificates
   * reactive: incidence response, network forensics

Core Components
 * full packet capture
 * network-based and host-based detection system (NIDS and HIDS)
 * analysis tools

## Full packet capture: [netsniff-ng](./so_netsniff-ng.md)
 * "packet sniffing beast"
 * captures all traffic seen by Security Onion sensors
 * stores as much as disk can hold
   * old data automatically purged before disk is full
 * full packet capture shows who came and went
   * where they went
   * what they brought
   * what they took

## Rule driven NIDS: ```[snort](./so_snort.md)``` or [suricata](http://suricata-ids.org/)
 * cisco firepower
 * rule based system
 * looks at network traffic fingerprint and identifiers that match known malicious, anamalous or suspicious traffic
 * akin to antivirus signatures for network

## Analysis driven NIDS: [bro-ids](./so_bro.md)
 * developed and maintained by UC Berkley
 * monitors network activity and logs 
   * any connection
   * DNS requests
   * detected network services and software
   * SSL cert
   * HTTP, FTP, IRC, SMTP, SSH, SSL, Syslog
 * checks MD5 sums for http file downloads agains Team Cymru's Malware Hash registry project
 * extensible way to analyze network data in real time
 * integrated with [REN-ISAC's Collective Intelligence Framework](./so_cif.md)
   * provides real-time correlation of network activity
   * up-to-date community intelligence feeds to alert when users access know malicious IPs, domains and URLs
  * Input framework
    * feed data into bro, which can be scripted
    * get employee usernames and correlat that against other activity like download exe file
  * file analysis framework
    * protocol independent file analysis
    * capture files as they pass through network

## HIDS: [ossec](./so_ossec.md)
 * Trend micro acquired: feww version
 * open source HIDS for Windows, Linuxm and Mac
 * performs log analysis
 * file integrity check
 * policy monitoring
 * rootkit detection
 * real-time alerting
 * active response
 * corelate host-based events with network-based events to identify attack

## Analysis Tool: [sguil](./so_sguil.md)
 * provides visibility into event data being collected and context to validate the detection
 * GUI to view snort, suricata, ossec and bro HTTP and PRADS (passive real-time asset detection system) alerts
 * allows pivot from alert into packet capture via wireshark or networkMiner
 * provides transcript of the full session that triggered the alert
 * view all associated traffic
 * query all packets captured
 * primary tool of so to provide context around given alert

## Analysis tool: [squert](./so_squert.md)
 * query sguil database
 * provide visualization 

## [ELSA](https://code.google.com/p/enterprise-log-search-and-archive/)

## [ELK](./so_elk.md)



# Deployment
 * distributed client-server model
 * sensors --> client
 * can be run on single physical machine or virtual machine
 * distributed sensors throughout infrastructure and report back to designated server

 * Standalone
 * Server-sensor
 * Hybrid















