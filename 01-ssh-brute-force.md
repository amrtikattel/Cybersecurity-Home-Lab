## Objective 
Simulate repeated failed SSH authentication attempts against a controlled test account and investigate the resulting Wazuh alerts.
## MITRE ATT&CK 
- T1110 — Brute Force
## Environment
| System        | Purpose                                                 |
| ------------- | ------------------------------------------------------- |
| Parrot OS     | THC-Hydra &  Metasploit Framework Common roots wordlist |
| Debian Server | Labuser, using the log source in auth.log               |
| Wazuh Server  | Monitoring my Debian Server                             |

# Observations
One of the first things I made sure to do on Parrot-OS was to download THC-Hydra then I also made a test user on my Debian Server environment called Lab User in order to keep my actual root/admin account safe. 
The command for hydra would be 
```bash 
hydra -l <username> -P </path/to/password_list.txt> ssh://<target_ip>
```

For my specific Purposes it would be 
```bash 
hydra -l <labuser> -P >/usr/share/metasploit-framework/data/wordlists/common_roots.txt> ssh://server_ip
```

As for the wordlist, it came from the metasploit framework that comes pre-installed with Parrot-OS. I have now ran my command, and Hydrax did not guess my passoword using the common_roots.txt. It ran over 268 Credential Accesses before it lost connection to my computer.
## Expected Telemetry
- SSH authentication failures (Failed Password/Invalid user)
- Source IP: Parrot OS address
- Target username: labuser
- Timestamp: Exact date and time of each requst
- Authentication method: Passsword-based SSH attempt
## Wazuh Detection 
- Alert - Rule ID: 5710 (SSHD brute force) or 5720 (Multiple SSH authentication failures)
- Rule description: [SSHD] Multiple authentication failures or brute force attempt detected.
- Severity: Medium-High (Typically Level 10 on Wazuh's 0-15 scale)
- Timestamp: Matches the active window of the Hydra execution
- Source IP: Parrot OS IP address
- Destination host: Debian Server IP
- Log Source: JournalCTL  -u ssh
  
  
  
  
  
