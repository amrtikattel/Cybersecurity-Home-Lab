# Simulated DDOS attack

## 1. Overview

- **Objective:** Simulate a controlled denial-of-service condition against the lab server by consuming CPU resources and deteremine whether Wazuh detects abnormal resource utilization and also my personal Unturned Server will be running 
- **Framework Mapping:** T1499 - Endpoint Denial of Service Attack
## 2. Environment Details

| **Role / Component**   | **System / OS**            | **Tool / Software**                                                                                |
| ---------------------- | -------------------------- | -------------------------------------------------------------------------------------------------- |
| **Source / Generator** | Parrot OS                  | Tool that will be used in order to DDOS my own Server                                              |
| **Target Asset**       | Debian Server/Wazuh Agent  | Server running Wazuh Agent and also running game server with players in order to see real workload |
| **Detection / SIEM**   | Wazuh / Central Log Server | THe server running the manager in order to look at the logs.                                       |
| Additional Pinger      | Arch Linux                 | Another system to monitor the latency                                                              |


## 3. Execution & Telemetry

- **Activity Summary:** I monitored the CPU ulitilization, System load average, Process creatition, Process duration, Service avaliability, Recovery after the test. 
- In order to properly test this, I figured out I needed to use hping3 in order to test this.
```bash 
sudo hping3 -S -p 27015 --flood <myserver-ip>
```
I started up the Unturned Server using the same command as before written in the Unturned Server Guide, then also made another Tmux window in order to see the network usuage on that machine using Btop.
After that I then went over to my parrot os machine and ran the command to flood the server with pings and to test the firewall, and other things as well
Aside from that I also made sure to run a debug command in order to see the server's stats
## 4. Detection & Analysis

- **Alert Triggered:** NO 
- **Rule ID:** T1499
- **Rule Description:** Endpoint Denial of Service Attack
- **Severity Level:** High
- **Key Indicators (IOCs):**
	- CPU Usage: 10%
	- Memory Usage: 1.41 Gigs
	- Network Usuage: 15.7 MiB/s Download, 5.61 KiB/s
    - Source IP: Parrot OS IP 
    - Target User/Asset: Debian Server 
    - Timestamp: Time when the attack happpened 
      Commands: sudo hping3 -S -p 27015 --flood myserver-ip,
    - ping serverip
    - btop
