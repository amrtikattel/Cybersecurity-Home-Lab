# Resouce Abuse

## 1. Overview

- **Objective:** Resouce monitoritng & Baseline Behavior
- **Framework Mapping:** N/A
## 2. Environment Details

| **Role / Component**   | **System / OS**            | **Tool / Software**                  |
| ---------------------- | -------------------------- | ------------------------------------ |
| **Source / Generator** | Parrot OS                  | N/A                                  |
| **Target Asset**       | Debian Server/Wazuh Agent  | Stress                               |
| **Detection / SIEM**   | Wazuh / Central Log Server | Monitoring system resouces and usage |

## 3. Execution & Telemetry

- **Activity Summary:** The first thing i did was install the package called stress then ran a command in order to stress test my server
```bash 
sudo apt instal stress 
```

```bash 
stress --cpu 4 --timeout 60
```
I then after that decided to look at the cpu usuage, process acitivity and the system performance changes on wazuh. Using another ssh terminal, i then used btop or top in order to see how heavy the usuage is on my current server
## 4. Detection & Analysis

- **Alert Triggered:** No
- **Rule ID:** T1499- Endpoint Denial of Service 
- **Rule Description:** High System Load 
- **Severity Level:** Server
- **Key Indicators (IOCs):**
	- Process/Command: stress --cpu 4 --timeout 60
	- Cpu/Load Average: 50%
    - Source IP: Parrot OS IP 
    - Target User/Asset: Debian Server 
    - Timestamp: Time when the attack happpened 