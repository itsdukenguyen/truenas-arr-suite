# 02 - Network & VLAN Setup

## VLANs in Use
- **VLAN 10 (Servers)**: Radarr, Sonarr, Lidarr, Bazarr, Transmission
- Other VLANs: Management, IoT, Clients, Guests

## Firewall Rules
- Port 445 (SMB) allowed from 192.168.10.115 to TrueNAS
- Port 9091 (Transmission RPC) accessible from VLAN 10

Key IPs:
- TrueNAS: 192.168.10.101
- Raspberry Pi: 192.168.10.115

