# 02 - Network & VLAN Setup

## VLAN Configuration
- **VLAN 1** (Management)
- **VLAN 10** (Servers) ← Radarr, Sonarr, Lidarr, Bazarr, Transmission
- **VLAN 20** (IoT)
- **VLAN 30** (Clients)
- **VLAN 40** (Guests)

## Key Firewall Rules
- Port 445 (SMB) allowed from Raspberry Pi (`192.168.10.115`) to TrueNAS
- Transmission RPC port `9091` accessible from VLAN 10

## IP Addresses
- TrueNAS: `192.168.10.101`
- Raspberry Pi (Transmission): `192.168.10.115`