# 11 - move_to_truenas.sh Script

This script runs automatically when Transmission finishes downloading a torrent. It mounts the TrueNAS SMB shares and notifies **Radarr, Sonarr, and Lidarr** via their APIs to scan and import the completed files.

## Full Script (`scripts/move_to_truenas.sh`)

```bash
#!/bin/bash

# ==================== CONFIGURATION ====================
RADARR_API_KEY="YOUR_RADARR_API_KEY_HERE"
SONARR_API_KEY="YOUR_SONARR_API_KEY_HERE"
LIDARR_API_KEY="YOUR_LIDARR_API_KEY_HERE"

RADARR_URL="http://192.168.10.101:7878/api/v3/command"
SONARR_URL="http://192.168.10.101:8989/api/v3/command"
LIDARR_URL="http://192.168.10.101:8686/api/v3/command"

# SMB Credentials
SMB_USER="mediauser"
SMB_PASS="DNguyen1206"
# =====================================================

# Create credentials file if it doesn't exist
if [ ! -f /home/pi/.smbcredentials ]; then
    echo "username=$SMB_USER" | sudo tee /home/pi/.smbcredentials > /dev/null
    echo "password=$SMB_PASS" | sudo tee -a /home/pi/.smbcredentials > /dev/null
    sudo chmod 600 /home/pi/.smbcredentials
fi

# Ensure mount points exist
sudo mkdir -p /mnt/truenas/Movies /mnt/truenas/Shows /mnt/truenas/Music

# Mount TrueNAS SMB shares
sudo mount -t cifs //192.168.10.101/Movies /mnt/truenas/Movies -o credentials=/home/pi/.smbcredentials,uid=1000,gid=1000,vers=3.0 2>/dev/null || true
sudo mount -t cifs //192.168.10.101/Shows /mnt/truenas/Shows -o credentials=/home/pi/.smbcredentials,uid=1000,gid=1000,vers=3.0 2>/dev/null || true
sudo mount -t cifs //192.168.10.101/Music /mnt/truenas/Music -o credentials=/home/pi/.smbcredentials,uid=1000,gid=1000,vers=3.0 2>/dev/null || true

# Notify *arr applications to scan completed downloads
echo "Notifying Radarr, Sonarr, and Lidarr..."

curl -X POST "$RADARR_URL" \
     -H "X-Api-Key: $RADARR_API_KEY" \
     -H "Content-Type: application/json" \
     -d '{"name":"DownloadedMoviesScan","path":"/downloads"}' --silent --output /dev/null

curl -X POST "$SONARR_URL" \
     -H "X-Api-Key: $SONARR_API_KEY" \
     -H "Content-Type: application/json" \
     -d '{"name":"DownloadedEpisodesScan","path":"/downloads"}' --silent --output /dev/null

curl -X POST "$LIDARR_URL" \
     -H "X-Api-Key: $LIDARR_API_KEY" \
     -H "Content-Type: application/json" \
     -d '{"name":"DownloadedAlbumsScan","path":"/downloads"}' --silent --output /dev/null

echo "Scan notifications sent to *arr apps."
```

## How to Use

1. Replace the API keys with your actual keys from each *arr app (Settings → General).
2. Make the script executable:Bash

```bash
chmod +x /home/pi/move_to_truenas.sh
```

3. Configure Transmission to use the script
- Open Transmission settings (`~/.config/transmission/settings.json`)
- Ensure this line exists:
```JSON
"script-torrent-done-filename": "/home/pi/move_to_truenas.sh",
"script-torrent-done-enabled": true
```

4. Test the script
```bash
TR_TORRENT_DIR="/media/pi/SSD1/Downloads/complete" \
TR_TORRENT_NAME="testfile.mkv" \
/home/pi/move_to_truenas.sh
```