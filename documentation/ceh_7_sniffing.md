
# Sniffing

1. Sniffing passwords using wireshark
* sniffing clear text http traffic for passwords in local interface
* remote machine sniffing with wireshark --> start remote packet capture protocol (experimental) service in remote windows --> wireshark option  to capture packets in remote interface

2. Analyzing a network using Capsa Network Analyzer
* Capsa - packet capturing, network monitoring, protocol analysis, packet decoding, diagnosis
* sniffs packets an generate meaningful information
* capture packet on interface with capsa --> 
  * get dashboard summary, diagnostic info, protocol info, 
  * mac and IP address in the network order by number of bytes, 
  * traffic between 2 machines, 
  * TCP conversation transaction details between two nodes, 
  * UDP conversation between two nodes,
  * graphical matrix connected nodes with weighted traffic volume between nodes
  * details of captured packets
  * log of http, email, dns etc
  * out of the box reports

3. Spoofing MAC Address Using SMAC
* hackers can monitor a switch activity and spoof a legitimate mac address 
* all traffic destined to target machine redirected to attackers machine
* SMAC
  * generate random mac address or choose legitimate mac address from the network
  * spoof mac address
  * attack other machines in the network
  * get traffic destined for other machine without revealing attackers mac

4. Perform Man-in-the-middle-Attach using Cain & Abel
* install cain & abel
* install winpcap
* select network adapter
* scan network for mac address
* select two machines for ARP poisoning
* make attacker MITM --> packets between those two machines are captured by cain & abel installed in attackers machine

5. Detecting Systems running in Promiscuous mode in a network using PromqryUI
* query machine(s) using PromqryUI
* detect any machines running in promiscuous mode

6. Detectng ARP Poisoning in switch based network
* APR poisoning - update target machine's arp cache with forged arp request and reply packets
* ARP resolves IP to MAC to send data
* install cain & abel for arp poisoning
* install wireshark to detect arp poisoning
* select two machines for arp poisoning and setting up MITM
* use Kali to send aro message while wireshark is capturing packets
* wireshark --> analyze --> expertinfo --> wireshark detects duplicate IP for one mac address

7. Detecting ARP attack with XArp Tool
* arp attacks not detected by firewalls
* xarp can help with that
* can monitor whole subnet from arp attack
* security level - basic but as soon as arp attack is detected, security level set to aggressive
* setup MITM with cain & abel, detect with xarp

Summary
* wireshark and capsa can be useful tool for attacks as well and system administrator
