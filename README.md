# TrueNAS SCALE *arr Suite Setup

[![TrueNAS SCALE](https://img.shields.io/badge/TrueNAS-SCALE-00b2a9?style=for-the-badge&logo=truenas)](https://www.truenas.com/)
[![Radarr](https://img.shields.io/badge/Radarr-FF0000?style=for-the-badge)](https://radarr.video/)
[![Sonarr](https://img.shields.io/badge/Sonarr-00AEEF?style=for-the-badge)](https://sonarr.tv/)
[![Lidarr](https://img.shields.io/badge/Lidarr-4CAF50?style=for-the-badge)](https://lidarr.audio/)
[![Bazarr](https://img.shields.io/badge/Bazarr-9C27B0?style=for-the-badge)](https://bazarr.media/)
[![Jellyfin](https://img.shields.io/badge/Jellyfin-00B5E5?style=for-the-badge)](https://jellyfin.org/)

Complete, battle-tested documentation for my automated media server stack on **TrueNAS SCALE**.

### Stack Includes:
- **Radarr** — Movies
- **Sonarr** — TV Shows  
- **Lidarr** — Music
- **Bazarr** — Subtitles
- **Transmission** (on Raspberry Pi) + custom move script
- **Jellyfin** — Media Server

## Table of Contents

- [Prerequisites](./docs/01-prerequisites.md)
- [Network & VLAN Setup](./docs/02-network-setup.md)
- [Datasets & Permissions](./docs/03-datasets-and-permissions.md)
- [SMB Shares](./docs/04-smb-shares.md)
- [Transmission on Raspberry Pi](./docs/05-transmission-rpi.md)
- [Radarr Setup](./docs/06-radarr-setup.md)
- [Sonarr Setup](./docs/07-sonarr-setup.md)
- [Lidarr Setup](./docs/08-lidarr-setup.md)
- [Bazarr Subtitles](./docs/09-bazarr-subtitles.md)
- [Jellyfin Integration](./docs/10-jellyfin-integration.md)
- [Move Script](./docs/11-move-script.md)
- [Troubleshooting](./docs/12-troubleshooting.md)

## Screenshots
See the [`screenshots/`](./screenshots/) folder.

## Apps Export
See the [`apps/`](./apps/) folder for exported TrueNAS App configurations.

**Last Updated**: May 2026