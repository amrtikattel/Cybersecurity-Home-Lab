Issue 1: Stop ssh brute forces
First I would go to the sshd_config file then turn off password authentication, Kbd interactive Authentication, Permit Root Login and Pub key Authenticaiton as well then restart my ssh 

Issue 2: Must turn on Nmap monitoring 
I change my ufw settings in order  to secure it more then after that I then decided to add and install crowdsec and turned it on as well. Then after that I decided to instal a firewall bouncer as well. Alongside this I then installed suricata, updated the rules and populated it as well 

Issue 3: Had to turn on/config which file directory needed which is bad, stop some users from changing files
Had to manually go into wazuh config, then realt-time monitor which directory I needed monitoring 

Issue 4: Must turn on Docker Container listner as well
Had to go through Wazuh Config's again in order to turn on Docker Container Listner too as well

Issue 5: Must turn on Apache2 data protection
Had to enable apache2 mod_headers then create a config file then paste in the rules to ServerTokens Prod, Server Signature OFF, and also Header always unsert X-Powered-BY. then enable it.

Issue 6: Including Canary Tokenes would help
The inclusion of Canary Token Honeypots would greatly help in the dectection of a data breach or leak.

Issue 7: Need alerts for service manipulation & Need alerts for Resource Abuse/DDOS attacks
Wazuh, Crowdsec, and suricata can handle this. But I did install auditd, and then I added a custom rule to add a high severity  alert for service manipulation, ddos, or resouce abuse. 

Issue 8: Must include static ips 
I need to make my machines have static ips to make it easier to connect and defend easier

Issue 10: Reverse Proxy
I installed nginx, then configure my applcications to use it for a reverse proxy


This should stop all of the either the lack of alerts or the continuation of security risks on my physical machine. And this is the end of the home lab.