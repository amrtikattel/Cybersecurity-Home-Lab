# Service-Manipulation

## 1. Overview

- **Objective:** Service Monitioring & System event detection 
- **Framework Mapping:** T1489 - Service Stop 
## 2. Environment Details

| **Role / Component**   | **System / OS**            | **Tool / Software**                                            |
| ---------------------- | -------------------------- | -------------------------------------------------------------- |
| **Source / Generator** | Parrot OS                  | Does nothing here                                              |
| **Target Asset**       | Debian Server/Wazuh Agent  | This would be using Nginx in order to stop and start a service |
| **Detection / SIEM**   | Wazuh / Central Log Server | This detects the service stopping and starting                 |

## 3. Execution & Telemetry

- **Activity Summary:** First since I already have nginx then I towuld repeatedly start and stop the serivce using these commands 
```bash 
sudo apt install nginx 
sudo systemctl start nginx 
sudo systemctl stop ginx 
```

## 4. Detection & Analysis

- **Alert Triggered:** No, it didn't trigger
- **Rule ID:** T1489
- **Rule Description:** Starting and stopping a service 
- **Severity Level:** N/A
- **Key Indicators (IOCs):**
	- Service Name:Nginx
	- Action: Both started and stopped
	- User:Lab User
    - Source IP: Parrot OS IP 
    - Target User/Asset: Debian Server 
    - Timestamp: Time when the attack happpened 