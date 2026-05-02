# 01 - Prerequisites

## Hardware & Software Used
- TrueNAS SCALE
- Raspberry Pi 4 (Transmission)
- TL-SG3428XMP PoE Switch + Ubiquiti U6+ APs
- EdgeRouter 4 with VLAN segmentation

## Required Accounts
- OpenSubtitles.com account (for Bazarr)
- Indexers via Prowlarr (1337x, RARBG, etc.)
- Jellyfin admin account

## Assumptions
- VLANs already configured (VLAN 10 for Servers)
- Media user mediauser (UID 1003) and group mediausers (GID 1003) exist
- Transmission running on Raspberry Pi at 192.168.10.115
- SMB shares working between RPi and TrueNAS
