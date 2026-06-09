# Beginner Jellyfin + Arr Stack Guide (Debian 13)

This guide is for beginners who want:

- Jellyfin
- Sonarr
- Radarr
- Prowlarr
- qBittorrent
- Jellyseerr

running on a mini PC using Debian 13 and Docker.

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
OR
- Rufus

---

# Debian Install Settings

During install:

## Select ONLY:
- SSH server
- standard system utilities

## DO NOT select:
- desktop environment
- GNOME
- KDE
- web server

---

# Step 2 — Find Your Server IP

After install finishes and you reach the terminal:

```bash
ip addr
