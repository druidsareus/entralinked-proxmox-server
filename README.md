<p align="center">
  <img src="https://github.com/druidsareus/entralinked-proxmox-server/blob/main/logo.png" alt="icon"/>
</p>
<h1 align="center">Entralinked ProxMox Server</h1>
<p align="center">
  <a href="https://www.proxmox.com/en/"><img src="https://github.com/druidsareus/entralinked-proxmox-server/blob/main/proxmox-logo-stacked-inverted-color.png" alt="Link"/></a> </p>


## Creating server via ProxMox - Setup and Instructions

## Progress tracker

Last Updated: 02MAR2026 @ 0031 EST
- [X] Create working systemd service
- [x] Working local server on end
- [X] Add tut to readme
- [ ] Upload sanitized vm image
- [ ] Link server with home assitant
- [ ] Add addition ideas of how users could integrate

# Initial setup:

1) Download latest release of entralinked

  Link: https://github.com/kuroppoi/entralinked/releases

  entralinked.+PCN.Skins.zip

2) Follow instructions for first time setup

  Link: https://github.com/kuroppoi/entralinked/wiki/Setup

3) Ensure you have connected all Pokemon games you plan on connecting at least once

4) Backup entire entralinked folder to a safe location

# Server setup:

1) Ensure you have a local version of ProxMox up and running and have a basic understanding of how it works

2) Create new virtual machine in ProxMox with the following

  ProxMox Virtual System info
  OS: Debian 13 (Linux)
  CPU: 1 Core
  RAM: 512mb
  HDD: 12gb

3) Download and use provided image of virtial machine

4) Assign Static IP

  Satic IP: xxx.xxx.xxx.xxx (this is the IP you will use as your DNS for the DS, DSi, and 3DS)

5) Copy over your local working version of entralinked to /root/entralinked and replace all

6) Reboot server

7) Profit


## Accessing server from web browser on same network

Game Sync GUI: http://xxx.xxx.xxx.xxx/dashboard/login.html (The xxx.xxx.xxx.xxx is the Static IP you set earlier)

Game Sync ID's: Save your Game Sync ID's here for future use
Pokemon Black Game Sync ID: xxxxxxxxxx
Pokemon White Game Sync ID: xxxxxxxxxx
Pokemon Black 2 Game Sync ID: xxxxxxxxxx
Pokemon White 2 Game Sync ID: xxxxxxxxxx


##  Control the server:

# login cmd: 

Using your terminal of choice (I use Kitty)
```
ssh root@xxx.xxx.xxx.xxx
```
password: xxxxxxxxxxxxxx

# Start service: 
```
systemctl start entralinked.service
```
# Check status: 
```
systemctl status entralinked.service
```
# View logs: 
```
journalctl -u entralinked.service -f
```
# Stop service: 
```
systemctl stop entralinked.service
```

## Backup of systemd service:

service doc loacted in /etc/systemd/system

file name: entralinked.service

file contents:
```
[Unit]
Description=Entralinked Java Service
After=network.target

[Service]
# Ensure the service runs from the correct directory
WorkingDirectory=/root/entralinked/
# Use the full path to the java executable
ExecStart=/usr/bin/java -jar /root/entralinked/entralinked.jar disablegui
# Restart automatically if the process crashes
Restart=always
RestartSec=5
# Treat exit code 143 (SIGTERM) as a clean exit
SuccessExitStatus=143
# Standard output/error will go to the system journal
StandardOutput=journal
StandardError=journal

[Install]
WantedBy=multi-user.target
```
