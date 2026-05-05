# 05 - Transmission on Raspberry Pi

**Host:** `rpi-torrent` @ `192.168.10.115`  
**Last Updated:** May 2026

Transmission runs as the `pi` user using **transmission-gtk** (GUI + Web UI).

## Configuration Summary

| Item                      | Value                                      |
|---------------------------|--------------------------------------------|
| **Download Directory**    | `/media/pi/SSD1/Downloads/complete`        |
| **Incomplete Directory**  | `/media/pi/SSD1/Downloads/incomplete`      |
| **Web Interface**         | `http://192.168.10.115:9091`               |
| **SMB Share**             | `//192.168.10.115/Downloads`               |

---

## 1. SSD Mount (Persistent)

```bash
# Create mount point
sudo mkdir -p /media/pi/SSD1

# Mount manually (replace /dev/sda1 with your SSD)
sudo mount /dev/sda1 /media/pi/SSD1

# Make mount permanent
sudo blkid | grep sda1
sudo nano /etc/fstab
```

Add this line to /etc/fstab:

```bash
UUID=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx /media/pi/SSD1 ext4 defaults,noatime 0 2
```

```bash
sudo mkdir -p /media/pi/SSD1/Downloads/{complete,incomplete}
sudo chown -R pi:pi /media/pi/SSD1/Downloads
sudo chmod -R 775 /media/pi/SSD1/Downloads
```

## 2. Transmission Setup
```bash
# Stop Transmission if running
killall transmission-gtk

# Edit settings
nano ~/.config/transmission/settings.json
```

Key settings:

```bash
{
  "download-dir": "/media/pi/SSD1/Downloads/complete",
  "incomplete-dir": "/media/pi/SSD1/Downloads/incomplete",
  "incomplete-dir-enabled": true,
  "script-torrent-done-enabled": true,
  "script-torrent-done-filename": "/home/pi/move_to_truenas.sh",
  "rpc-enabled": true,
  "rpc-port": 9091,
  "rpc-whitelist-enabled": false,
  "rpc-authentication-required": true,
  "rpc-username": "transmission",
  "rpc-password": "YourStrongPassword"
}
```

## 3. Start & Access
- Launch GUI: transmission-gtk &
- Web UI: http://192.168.10.115:9091

## 4. Samba Share (for *arr apps)
```bash
sudo nano /etc/samba/smb.conf
```

Add at the bottom:
```ini
[Downloads]
path = /media/pi/SSD1/Downloads
browseable = yes
writable = yes
guest ok = no
valid users = pi
create mask = 0775
directory mask = 0775
```

```bash
sudo smbpasswd -a pi
sudo systemctl restart smbd
```