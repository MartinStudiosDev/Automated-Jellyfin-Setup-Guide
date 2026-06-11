# Beginner Jellyfin + Arr Stack Guide (Debian 13)

This guide is for beginners who want:

- Jellyfin
- Sonarr
- Radarr
- Prowlarr
- Qbittorent
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

- On another computer type your IP address into the seacrh bar of a search engine
- You can then log into your router with the username and password on the back of your router
- Find the option to reserve the IP of your PC running Debian. This way it will never change
- You can now remove the peripherals of your PC running Debian, they will no longer be needed. 
---

# Step 4 — SSH Into your PC

- On another PC, go to your CMD or terminal and type:
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
# Step 5 — Create Media Folders

Now that Docker is installed, we need to create folders for:
- Movies
- TV shows
- Downloads
- Docker app data

Run:

```bash
sudo mkdir -p /media/movies
sudo mkdir -p /media/tv
sudo mkdir -p /media/downloads
sudo mkdir -p /srv/docker
```

---

# Step 6 — Create a Docker Stack Folder

```bash
mkdir ~/media-stack
cd ~/media-stack
```

---

# Step 7 — Create a YAML File

- Run:

```bash
nano docker-compose.yml
```
- Replace the contents of the file with this code
  
```bash
services:

  sonarr:
    image: lscr.io/linuxserver/sonarr:latest
    container_name: sonarr
    ports:
      - "8989:8989"
    volumes:
      - /srv/docker/sonarr:/config
      - /media/tv:/tv
      - /media/downloads:/downloads
    restart: unless-stopped

  radarr:
    image: lscr.io/linuxserver/radarr:latest
    container_name: radarr
    ports:
      - "7878:7878"
    volumes:
      - /srv/docker/radarr:/config
      - /media/movies:/movies
      - /media/downloads:/downloads
    restart: unless-stopped

  prowlarr:
    image: lscr.io/linuxserver/prowlarr:latest
    container_name: prowlarr
    ports:
      - "9696:9696"
    volumes:
      - /srv/docker/prowlarr:/config
    restart: unless-stopped

  qbittorrent:
    image: lscr.io/linuxserver/qbittorrent:latest
    container_name: qbittorrent
    ports:
      - "8080:8080"
    volumes:
      - /srv/docker/qbittorrent:/config
      - /media/downloads:/downloads
    restart: unless-stopped

  jellyseerr:
    image: fallenbagel/jellyseerr:latest
    container_name: jellyseerr
    ports:
      - "5055:5055"
    volumes:
      - /srv/docker/jellyseerr:/app/config
    restart: unless-stopped
```

- Save the file by pressing "Ctrl + X" then "Y" followed by "Enter"

---

# Step 8 — Start your stack and open the services!

- Run:

```bash
docker compose up -d
```

- Your services should install, give it a few minutes for the first time.

- Visit your services in a browser using these links:
  
```bash
# Sonarr
http://yourIP:8989
# Radarr
http://yourIP:7878
# Prowlarr
http://yourIP:9696
# Qbittorent
http://yourIP:8080
# Jellyseer
http://yourIP:5055
```
