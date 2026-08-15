## What machines exist? 
For my Homelab, I have 4 machines being an Arch Linux Host machine, a Debian Home Server(Wazuh-agent), and a Linux Mint Wazuh Server Host. On the Arch Linux Host, I have a Virutal Machine using QEMU/Virt Manager running Parrot OS home edition
## How are they connected?
The Arch Linux Host is connected via ethernet and so is the Parrot OS machine. The Linux Mint host is using wifi, and the Debian Home Server is using ethernet.
A diagram of this will be provided below 
Arch Linux:
	Parrot-OS VM via QEMU/Virt Manager
Debian Server:
	Wazuh-Agent
Linux Mint
	Wazuh-Server

## What is each machine responsible for?

Parrot OS (Activity Generator) on Arch Linux using VM
        |
        v
Debian Server (Target + Logs)
        |
        v
Wazuh Server (Detection + Reporting)

| System        | Purpose                             |
| ------------- | ----------------------------------- |
| Parrot OS     | Generate controlled security events |
| Debian Server | Host services and collect logs      |
| Wazuh Server  | Monitor, detect, alert, and report  |