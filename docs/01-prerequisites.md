# 01 - Prerequisites

## Hardware & Software Used
- TrueNAS SCALE
- Raspberry Pi 4 (Transmission)
- TL-SG3428XMP Switch + Ubiquiti APs
- EdgeRouter 4 with VLANs

## Required Accounts
- OpenSubtitles.com (for Bazarr)
- Indexers via Prowlarr (1337x, RARBG, etc.)
- Jellyfin admin account

## Assumptions
- VLANs already configured (Management, Servers, etc.)
- Media user `mediauser` (UID 1003) and group `mediausers` (GID 1003) exist
- Transmission running on Raspberry Pi at `192.168.10.115`