# \# 11 - move\_to\_truenas.sh Script

# 

# This script runs automatically when Transmission finishes downloading a torrent. It mounts the TrueNAS SMB shares and notifies Radarr, Sonarr, and Lidarr via their APIs to scan the completed downloads.

# 

# \## Full Script (`scripts/move\_to\_truenas.sh`)

# 

# ```bash

# \#!/bin/bash

# 

# \# ==================== CONFIGURATION ====================

# RADARR\_API\_KEY="YOUR\_RADARR\_API\_KEY\_HERE"

# SONARR\_API\_KEY="YOUR\_SONARR\_API\_KEY\_HERE"

# LIDARR\_API\_KEY="YOUR\_LIDARR\_API\_KEY\_HERE"

# 

# RADARR\_URL="http://192.168.10.101:7878/api/v3/command"

# SONARR\_URL="http://192.168.10.101:8989/api/v3/command"

# LIDARR\_URL="http://192.168.10.101:8686/api/v3/command"

# 

# \# SMB Credentials (for mounting TrueNAS shares)

# SMB\_USER="mediauser"

# SMB\_PASS="DNguyen1206"

# \# =====================================================

# 

# \# Create credentials file if it doesn't exist

# if \[ ! -f /home/pi/.smbcredentials ]; then

# &#x20;   echo "username=$SMB\_USER" | sudo tee /home/pi/.smbcredentials > /dev/null

# &#x20;   echo "password=$SMB\_PASS" | sudo tee -a /home/pi/.smbcredentials > /dev/null

# &#x20;   sudo chmod 600 /home/pi/.smbcredentials

# fi

# 

# \# Ensure mount points exist

# sudo mkdir -p /mnt/truenas/Movies /mnt/truenas/Shows /mnt/truenas/Music

# 

# \# Mount TrueNAS SMB shares

# sudo mount -t cifs //192.168.10.101/Movies /mnt/truenas/Movies -o credentials=/home/pi/.smbcredentials,uid=1000,gid=1000,vers=3.0 2>/dev/null || true

# sudo mount -t cifs //192.168.10.101/Shows /mnt/truenas/Shows -o credentials=/home/pi/.smbcredentials,uid=1000,gid=1000,vers=3.0 2>/dev/null || true

# sudo mount -t cifs //192.168.10.101/Music /mnt/truenas/Music -o credentials=/home/pi/.smbcredentials,uid=1000,gid=1000,vers=3.0 2>/dev/null || true

# 

# \# Notify \*arr applications to scan completed downloads

# echo "Notifying Radarr, Sonarr, and Lidarr..."

# 

# curl -X POST "$RADARR\_URL" \\

# &#x20;    -H "X-Api-Key: $RADARR\_API\_KEY" \\

# &#x20;    -H "Content-Type: application/json" \\

# &#x20;    -d '{"name":"DownloadedMoviesScan","path":"/downloads"}' --silent --output /dev/null

# 

# curl -X POST "$SONARR\_URL" \\

# &#x20;    -H "X-Api-Key: $SONARR\_API\_KEY" \\

# &#x20;    -H "Content-Type: application/json" \\

# &#x20;    -d '{"name":"DownloadedEpisodesScan","path":"/downloads"}' --silent --output /dev/null

# 

# curl -X POST "$LIDARR\_URL" \\

# &#x20;    -H "X-Api-Key: $LIDARR\_API\_KEY" \\

# &#x20;    -H "Content-Type: application/json" \\

# &#x20;    -d '{"name":"DownloadedAlbumsScan","path":"/downloads"}' --silent --output /dev/null

# 

# echo "Scan notifications sent to \*arr apps."

