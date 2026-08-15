# My Own Personal Unturned Server

## 1. Overview

- **Objective:** This is a realistic workload in order to pratice Server startup/shutdown, network connections, CPU usage, Memory Usuage and File changes. I hope to make a realistical scenario eventually to simulate a DDOS attack.
- **Framework Mapping:** N/A
## 2. Environment Details

| **Role / Component**   | **System / OS**            | **Tool / Software**                                                                              |
| ---------------------- | -------------------------- | ------------------------------------------------------------------------------------------------ |
| **Source / Generator** | Parrot OS                  | N/A                                                                                              |
| **Target Asset**       | Debian Server/Wazuh Agent  | my own personal bash script for updating unturned, steamCMD, steam, and unturned server headless |
| **Detection / SIEM**   | Wazuh / Central Log Server | Monitors my server                                                                               |

## 3. Execution & Telemetry

- **Activity Summary:** I first run the updated unturned server bash script that i made in order to update the game and to preserve the game files.
```bash 
~/update_unturned.sh
```
within the update_unturned script would be 
```bash 
#!/bin/bash

# Unturned Dedicated Server updater
# Updates game files in place without deleting server configuration

set -e

SERVER_DIR="/home/name/unturned"
STEAMCMD="/home/name/steamcmd/steamcmd.sh"

echo "Stopping Unturned server (if running)..."

# Optional: stop a running server launched with this script/user
pkill -f Unturned_Headless.x86_64 || true

echo "Updating Unturned files in:"
echo "$SERVER_DIR"

"$STEAMCMD" \
    +force_install_dir "$SERVER_DIR" \
    +login anonymous \
    +app_update 1110390 validate \
    +quit

echo "Recreating Steam SDK64 link..."

mkdir -p ~/.steam/sdk64

rm -f ~/.steam/sdk64/steamclient.so

ln -s /home/name/steamcmd/linux64/steamclient.so ~/.steam/sdk64/steamclient.so

echo "Update complete."

echo "Your server files were preserved:"
echo "- Servers/"
echo "- Commands.dat"
echo "- Maps/"
echo "- Workshop/"
echo "- Config files"

echo "Start your server normally."
```
I made sure to ensure that my server mainteance will be easy as it can be.

After that I usually start a tmux session in order to have one window dedicated for unturned and another dedicated to seeing server statistics via btop
I do this via 
```bash 
tmux new -s unturned
./Unturned_Headless.x86_64 -nographics
CTRL + B & C TO MAKE NEW WINDOW
```
after this i just then run btop
Then I am done. As for monitoring, the cpu remains stable consistently and there isn't any sudden exectuable changes, abnormal resource usuage, there will be new network listeners if players join, and there is no service failures when doing the Unturned Server. I hope to model a realistic Unturned game server on a public network via making my own ddos scripts, alongside having network listerners or players.
## 4. Detection & Analysis

- **Alert Triggered:** N/A
- **Rule ID:** N/A
- **Description:** Unturned Server 
- **Severity Level:** NONE
- **Key Indicators (IOCs):**
	- Cpu Usauge: 4%
	- Memory Usuage: 2 gigs/16
    - Source IP: Parrot OS IP 
    - Target User/Asset: Debian Server 
    - Timestamp: Time when the attack happpened 
