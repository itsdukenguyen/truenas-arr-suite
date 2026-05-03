# 01 - Prerequisites

## Hardware Used

- **TrueNAS SCALE** server
- **Raspberry Pi 4** (running Transmission + `move_to_truenas.sh`)
- **TL-SG3428XMP** PoE Switch
- **Ubiquiti U6+** Access Points (x3)
- **EdgeRouter 4** (primary + cold backup)

## EdgeRouter 4 Firewall Rules (Relevant)

- **Rule 19**: Allow SMB (445), 9000, 7878, 20489 from VPN (`100.64.0.0/10`) → VLAN 10
- **Rule 30**: Allow VLAN 10 (Servers) → Internet
- **Rule 40**: Allow VLAN 20 (IoT) → Internet

## Required Accounts

- OpenSubtitles.com (for Bazarr)
- Prowlarr indexers (1337x, RARBG, etc.)
- Jellyfin admin account

## Assumptions

- VLAN 10 (Servers) is already configured
- Media user `mediauser` (UID 1003) and group `mediausers` (GID 1003) exist
- Transmission is running on Raspberry Pi at `192.168.10.115`