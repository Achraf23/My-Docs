## Securing Apache against Dos attacks
https://www.opensourceforu.com/2011/04/securing-apache-part-8-dos-ddos-attacks/ (2011)

**DoS TCP Syn**
-  open half tcp connections : the client never sends the final ack which consumes the  server's resources since it needs to store information on this half-open connection somewheer

**ICMP smurf**
spoof the victim's IP and send an echo request to the **broadcast** adderss. All the nodes on the network will send echo replies to the victim

**UDP flooding**
overload the victim's resources. TCP and ICMP have been patched to make Dos and Ddos harder. So, UDP flood in some cases is nbetter

### how Ddos attacks are built

-  Central source propagation
Each zombie (part of the Ddos) requests attack tools from a central server. Not used much because easily detectable

-  Back-chaining Propagation
Each zombie, after taking control of a machine, transfert the attack tools to this new machine which will do the same as its predecessor. Therefore, every zombie could propagate the attack tools to other machines

-  autonomous propagation
It's always the attacker that delivers the actual toolkits to compromised machines


Attack toolkits :
-  Trinity, Tribe Flood network
usually a system that controls zombies and sends them command via random ports or IRC channels. Traffic is usually encoded and access to zombies may be password protected.

### Ddos 2.0
Application flooding using Ddos is now common since all network Dos and Ddos are detected using IDS/IPS and access control lists.

**Slowloris** : sends incompletes HTTP headers and keep the connection alive by sending other line headers after some time. Apache patches did not fix once and for all these vulnerabilities

#### Use of Web servers in Ddos 2.0

## Security against Ddos 2.0 attacks
-  captchas
-  bot analysis by extracting out unique characteristics
-  Filter spoofed IPs
-  Install anti-malware and anti-botnet software to prevent installation of malicious toolkits on web server

### Securing Apache against Ddos
-  `MaxClients` directive
-  Use options such as `mod_limitipconn`, `mod_throttle`, `` and `mod_bwshare` tp control incoming traffic per virtual hosts (virtual host = each individual site served by Apache)

https://www.digitalocean.com/community/tutorials/how-to-protect-against-dos-and-ddos-with-mod_evasive-for-apache-on-centos-7 (complet Guide to Mod evasive)

`mod_dosevasive`
-  different than the options abve sicne it's not a traffic shaping technique. More of a blacklist of certain IPs which is risky since it can block a lot of users behind a proxy for example (when many users are behind a proxy, it is perfectly normal that a lot of traffic is emanating from a unique IP)
