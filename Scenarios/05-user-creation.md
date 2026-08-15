# User Creation 

## 1. Overview

- **Objective:** Account Monitoring and Privilege changes 
- **Framework Mapping:** T1136- Create Account 
## 2. Environment Details

| **Role / Component**   | **System / OS**            | **Tool / Software**                     |
| ---------------------- | -------------------------- | --------------------------------------- |
| **Source / Generator** | Parrot OS                  | Doesn't Do anything in this test        |
| **Target Asset**       | Debian Server/Wazuh Agent  | Creates another account & adds the user |
| **Detection / SIEM**   | Wazuh / Central Log Server | Detects the new user account            |

## 3. Execution & Telemetry

- **Activity Summary:** On my debian server I ran this command 
```bash 
	sudo adduser testadmin 
```
This should show on the wazuh detection would be New accounts, Accounts changes, Privelege changes 
## 4. Detection & Analysis

- **Alert Triggered:** New user added to the system
- **Rule ID:** 5902
- **Rule Description:** New user added to the system 
- **Severity Level:**  Level 8 
- **Key Indicators (IOCs):**
	- New Username: testadmin
	- UID:1003
	- Creating User:labuser
    - Source IP: Parrot OS IP 
    - Target User/Asset: Debian Server 
    - Timestamp: Time when the command happpened 
