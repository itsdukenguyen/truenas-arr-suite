# 05 - Transmission on Raspberry Pi

**Last Updated:** July 2025

This guide covers a clean, reliable setup for **Transmission** on the Raspberry Pi (`rpi-torrent` @ `192.168.10.115`) using a dedicated 2TB SSD.

## Configuration Summary

| Item                        | Path / Value                              |
|-----------------------------|-------------------------------------------|
| **Download Directory**      | `/mnt/SSD1/Downloads/complete`            |
| **Incomplete Directory**    | `/mnt/SSD1/Downloads/incomplete`          |
| **Web Interface**           | `http://192.168.10.115:9091`              |
| **RPC Port**                | `9091`                                    |
| **SMB Share**               | `\\192.168.10.115\SSD1`                   |

---

## SSD Setup - Clean Mount at `/mnt/SSD1`

### 1. Prepare the SSD (One-time)

```bash
# Wipe and partition SSD1
sudo wipefs -a /dev/sda
sudo fdisk /dev/sda
# Inside fdisk: o → n → p → 1 → Enter → Enter → w

sudo mkfs.ext4 /dev/sda1

# Create mount point and mount
sudo mkdir -p /mnt/SSD1
sudo mount /dev/sda1 /mnt/SSD1

# Get UUID for persistent mount
lsblk -f | grep sda1


sudo nano /etc/fstab


UUID=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx /mnt/SSD1 ext4 defaults,noatime 0 2


sudo mkdir -p /mnt/SSD1/Downloads/{complete,incomplete}
sudo chown -R debian-transmission:debian-transmission /mnt/SSD1/Downloads
sudo chmod -R 775 /mnt/SSD1/Downloads

# Clean up old stale mount points
sudo rm -rf /media/pi/SSD* /mnt/SSD2


# 1. Purge old installation
sudo apt purge transmission-* -y
sudo apt autoremove -y
sudo rm -rf /etc/transmission-daemon ~/.config/transmission

# 2. Fresh install
sudo apt update
sudo apt install transmission-daemon transmission-gtk -y


sudo systemctl stop transmission-daemon
sudo nano /etc/transmission-daemon/settings.json


{
  "download-dir": "/mnt/SSD1/Downloads/complete",
  "incomplete-dir": "/mnt/SSD1/Downloads/incomplete",
  "incomplete-dir-enabled": true,
  "rpc-authentication-required": true,
  "rpc-username": "transmission",
  "rpc-password": "YourStrongPasswordHere",
  "rpc-port": 9091,
  "rpc-whitelist-enabled": false,
  "rpc-bind-address": "0.0.0.0",
  "rpc-enabled": true
}


sudo chown -R debian-transmission:debian-transmission /etc/transmission-daemon
sudo systemctl enable --now transmission-daemon


transmission-gtk


Go to Edit → Preferences → Remote
Check Enable remote control
Host: 192.168.10.115
Port: 9091
Username: transmission
Password: (the one you set)

Verify both interfaces show the same torrents.