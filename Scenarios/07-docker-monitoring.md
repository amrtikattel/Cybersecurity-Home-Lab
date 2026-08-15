# Docker Monitoring

## 1. Overview

- **Objective:** Container monitoring & Process activity
- **Framework Mapping:** N/A
## 2. Environment Details

| **Role / Component**   | **System / OS**            | **Tool / Software**                 |
| ---------------------- | -------------------------- | ----------------------------------- |
| **Source / Generator** | Parrot OS                  | N/A                                 |
| **Target Asset**       | Debian Server/Wazuh Agent  | Runs docker contrianer program      |
| **Detection / SIEM**   | Wazuh / Central Log Server | Checks to see if a container is ran |

## 3. Execution & Telemetry

- **Activity Summary:** I had to install docker then i ran and started up a docker container that has a small hello world program then using the Wazuh Dashboard I would be able to see the container, the docker daemon, and the resouce usage.

## 4. Detection & Analysis

- **Alert Triggered:** Yes 
- **Rule ID:** 87903
- **Rule Description:** Docker: Container test-container started 
- **Severity Level:** Level 3 
- **Key Indicators (IOCs):**
	- Container name:eager_booth
	- Docker Image: Hello wolrd
	- Action: prints out the hello world command on docker
    - Source IP: Parrot OS IP 
    - Target User/Asset: Debian Server 
    - Timestamp: Time when the attack happpened 
