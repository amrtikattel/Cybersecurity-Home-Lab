# Triggering Canary Token

## 1. Overview

- **Objective:** Deploy canary tokens on the Debian Server to detect unauthrized access to files or resources that should not normally be accessed 
- **Framework Mapping:** T1083- Files and Directory Discovery
## 2. Environment Details

| **Role / Component**   | **System / OS**            | **Tool / Software**                                                                           |
| ---------------------- | -------------------------- | --------------------------------------------------------------------------------------------- |
| **Source / Generator** | Parrot OS                  | Generates the Logs and opening the web Canary Token                                           |
| **Target Asset**       | Debian Server/Wazuh Agent  | The Canary Token link is put into a text file.                                                |
| **Detection / SIEM**   | Wazuh / Central Log Server | Monitored some of the logs                                                                    |
| Host Machine           | Arch Linux                 | Goes on Canary Tokens websites, gets generated token then uses wormhole to transfer over link |

## 3. Execution & Telemetry

- **Activity Summary:** So this is in order to monitor the Canary Token Access, Source I, Access timestamp, Hostname, Process/user reponsible, where avaliable, Unxpected access to decoy files. 
- As for how I set it up, it would be going to the Canary Tokens website then got the web bug and I put in the email and the alert. I then wormholed the link from my Arch Host to my Debian Host, then put that link in a text file called something important.
- Some of the commands I used would be 
```bash 
wormhole send --text "canary-token-link"
```
Then on the other machine, you receive it then you copy and pasted the link into it
```bash
wormhole receive wormhole-code
nano important.txt
```

Then from the Parrot OS vm ssh in, you copy and paste the link into a browser in order to trigger the token
## 4. Detection & Analysis

- **Alert Triggered:** YES
- **Rule ID:** NO
- **Rule Description:** Carnary Token to get  
- **Severity Level:** N/A
- **Key Indicators (IOCs):**
	- Carnary Link: http://canarytokens.com/images/frbas6um523g8bhp9jp38gsep/submit.aspx
	- Full File Path: ~/home/labuser/important.txt
	- File Hash:ed075b687fcc6c9d06173204c5c20a440eeb8c0fa702d27529901a1506e3e28
    - Source IP: Parrot OS IP 
    - Target User/Asset: Debian Server 
    - Timestamp: Time when the attack happpened 
