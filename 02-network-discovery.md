# Network Discovery/ Port Scanning

## 1. Overview

- **Objective:** Using Nmap in order to check Network Visbility & Reconnaissance detection
- **Framework Mapping:** T1046 — Network Service Discovery

## 2. Environment Details

| **Role / Component**   | **System / OS**      | **Tool / Software**                                        |
| ---------------------- | -------------------- | ---------------------------------------------------------- |
| **Source / Generator** | Parrot OS            | NMAP                                                       |
| **Target Asset**       | Debian               | JournalCTL checking UFW for attempts at logging port scans |
| **Detection / SIEM**   | Wazuh Server or SIEM | Monitoring my system for port scans and such               |

## 3. Execution & Telemetry

- **Activity Summary:** I installed and ran nginx on my debian server, and then installed nmp trying to do port scans and to scan all of the ports of the debian server. Wazuh was unable to pick up on the attempts at scans on the server, which serves a bit of a vulnerability. Forutnately UFW blocked some of the attempts at scans using NMAP so i had to use -pn in order to get any good information. I was unsucessful at looking at the nginx information too as it seems.
```bash
sudo nmap -sV -pN debian-ip
nmap -Pn ip
nmap -p- ip
nmap -s V ip
```
## 4. Detection & Analysis

- **Alert Triggered:** NO, What should of triggered would be a firewall event from UFW logs
- **Rule ID:** 5700
- **Rule Description:** Firewall Event
- **Severity Level:**  Low-Medium
- **Key Indicators (IOCs):**
    - Source IP: Parrot OS IP
    - Target User/Asset: Debian Server IP
    - Timestamp: Right when the nmap scan triggered
    - Protcol:TCP


