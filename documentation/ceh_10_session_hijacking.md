# Session Hijacking

intercept session that is already autheticated and active
active session can contain credit card info, password etc

1. Session hijacking using Zed Attack Proxy (ZAP)
* for the lab --> configure chrome attacker machine as proxy server 
  * target --> chrome://settings --> show advanced settings --> network --> change proxy settings 
    --> internet properties --> connection tab 
    --> LAN Settings --> check use proxy server for LAN --> IP and port of attacker
  * attacker --> install ZAP --> and configure with proxy
  * target browse internet --> attacker see traffic in ZAP 
    * see all request and response
    * modify any part of request or response --> user go to google.com --> they get amazon.com
    * drop any request or response
    
2. Hijacking user session with firebug
* session hijacking using cross-site scripting attack

* start by ARP poisoning using cain & abel and run wireshark
* target logon to website
* attacker can filter wireshark on target_ip & http.cookie
* packet details --> hypertext transfer protocol --> cookie --> copy cookie with sessionID
* open firebug in firefox --> cookie tab --> enable --> create cookie
* edit cookie --> name: ASP.NET_sessionID --> host: website.com --> value: sessionID
* now go website.com/index.aspx --> logged in as target user
