# Web Server Activity Testing
## 1. Overview

- **Objective:** Service Monitoring and Web Log collection
- **Framework Mapping:** T1190 Explioit Public Facing Applications 
## 2. Environment Details

| **Role / Component**   | **System / OS**            | **Tool / Software**                                                    |
| ---------------------- | -------------------------- | ---------------------------------------------------------------------- |
| **Source / Generator** | Parrot OS                  | curl in order to genrate requsts for the web server                    |
| **Target Asset**       | Debian Server/Wazuh Agent  | The server runs an apache2 web server, then puts the activity in a log |
| **Detection / SIEM**   | Wazuh / Central Log Server | Logs the activity                                                      |

## 3. Execution & Telemetry

- **Activity Summary:** So the first thing i do is I install apache2 using this command 
```bash 
sudo apt install apache2 
```

After that I then start the apache2 webserver
```bash 
sudo systemctl enable --now apache2
```
Then after doing that, using my Parrot OS VM I then generate requests via this command 
```bash 
curl https://<debian.ip>
```

Then also I make sure to Log to monitor 

There wasn't any large requst volumes, nor where there invalid urls, as for suscipous requests, I think it would be suscipous to have a random ip curl and gett information regarding your webpage
## 4. Detection & Analysis

- **Alert Triggered:** Yes, but need to configure in Wazuh
- **Rule ID:** N/A
- **Rule Description:** Web Serveer Activity Tessting/ Web Log Collection
- **Severity Level:**  n/A
- **Key Indicators (IOCs):**
	- HTTP Method: Get
	- Reqeust URL: http://serverip
	- HTTP Status Code: 200 
    - Source IP: Parrot OS IP 
    - Target User/Asset: Debian Server 
    - Timestamp: Time when the attack happpened 
