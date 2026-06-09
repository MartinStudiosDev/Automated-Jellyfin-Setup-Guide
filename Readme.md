# Beginner Jellyfin + Arr Stack Guide (Debian 13)

This guide is for beginners who want:

- Jellyfin
- Sonarr
- Radarr
- Prowlarr
- SabNZB
- Seerr

running on a PC using Debian 13 and Docker.

No Linux experience required.

---

# Hardware Used

- GMKtec N95 Mini PC
- Debian 13 (Trixie)
- External USB SSDs
- Ethernet connection

---

# Step 1 — Install Debian 13

Download the Debian 13 amd64 netinst ISO.

Flash it to a USB using:
- Ventoy
OR Rufus
- Boot your PC and enter the Boot Menu to select the USB
---

# Debian Install Settings

During install:

## Select ONLY:
- SSH server
- Standard system utilities

## DO NOT select:
- desktop environment
- GNOME
- KDE
- web server, etc.

---

# Step 2 — Find Your Server IP

After install finishes and you reach the terminal:

```bash
ip addr
```
Find your IP address that looks like 192.168.1.XXX, make sure to write this down

---

# Step 3 — Reserve your IP Address

- On another computer type your IP address into the seacrh bar of a seacrh engine
- You can then log into your router with the username and password on the back of your router
- Find the option to reserve the IP of your PC running Debian. This way it will never change
- You can now remove the peripherals of your PC running Debian, they will no longer be needed. 
---

# Step 4 — SSH Into your PC

-On another PC, go to your CMD or terminal and type:
 ```bash
ssh username@192.168.1.xxx
```
- Replace "username" with the username you setup during the Debian installation
- Replace the IP address after the "@" with the IP you reserved for your Debian PC

You will then be prompted to enter your password. From here you can completely controll the PC! This is how you will controll your server until we setup a dashboard down the road. 

# Step 5 - Install Docker

- While SSH'd into the Debian PC, paste the code below
  ```bash
  sudo apt update && sudo apt upgrade -y
  ```
- Run this to install Docker
  ```bash
  curl -fsSL https://get.docker.com | sh
  ```
- Enable Docker without Sudo
  ```bash
  sudo usermod -aG docker $USER
  ```
- Paste below to reboot, then SSH back into the PC
  ```bash
  sudo reboot
  ```
- Test that Docker is working. If no Errors appear after this command, all is well!
   ```bash
  docker ps
  ```
# Step 5 — Stick around for daily additions!

This guide will be updated daily alongside my TikTok tutorial series! 
