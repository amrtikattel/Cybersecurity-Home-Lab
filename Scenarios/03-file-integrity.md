# File Integrity Monitoring (FIM)

## 1. Overview

- **Objective:** FIle Monitoring & Change Detection
- **Framework Mapping:** T1565 - Data Manipulation 

## 2. Environment Details

| **Role / Component**   | **System / OS**         | **Tool / Software**                |
| ---------------------- | ----------------------- | ---------------------------------- |
| **Source / Generator** | Parrot OS               | Echo/File changing or manipulation |
| **Target Asset**       | Debian Server           | Another directory/ a text file     |
| **Detection / SIEM**   | Linux Mint/Wazuh Server | ID 553 OR ID 554                   |

## 3. Execution & Telemetry

- **Activity Summary:** the first thing that I did was to make a directory for testing, I then created a file using the echo command.
```bash 
mkdir ~/important-files
```

```bash 
echo "testing" > ~/importan-files/test.txt
```
After that I then sshed, into the my server using the parrot OS
```bash 
ssh labuser@server-ip
```
Then I ran a command in order to change the file
```bash 
echo "change" >> ~/important-files/test.txt
```

## 4. Detection & Analysis

- **Alert Triggered:** Yes but after having to turn on real-time detection (will be in report)
- **Rule ID:** 550
- **Rule Description:** File Modification
- **Severity Level:** Medium
- **Key Indicators (IOCs):**
	- File Path: /home/labuser/important-files/test.tct
	- Change Type: Modifying text
	- File Hash: d3bfe01c6e34d5042be2dd5dddd7a7924e315d1833039f6863905431cfc625c8 
    - Source IP: PARROT-OS
    - Target User/Asset: Debian Server
    - Timestamp: About the time the detection happened 2:55 
      
      

