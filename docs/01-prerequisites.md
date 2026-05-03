# 01 - Prerequisites

## Hardware Used

- **TrueNAS SCALE** server
- **Raspberry Pi 4** (Transmission + move script)
- **TL-SG3428XMP** PoE Switch
- **Ubiquiti U6+** Access Points (x3)
- **EdgeRouter 4** (primary + cold backup)

## Relevant EdgeRouter 4 Firewall Rules

- **Rule 19**: Allow SMB (445) and services from VPN to VLAN 10
- **Rule 30**: Allow VLAN 10 (Servers) to Internet
- **Rule 40**: Allow VLAN 20 (IoT) to Internet

## Required Accounts

- OpenSubtitles.com (Bazarr)
- Prowlarr indexers
- Jellyfin admin account

## Assumptions

- VLAN 10 (Servers) is configured
- Media user `mediauser` (UID 1003) and group `mediausers` (GID 1003) exist