\# 02 - Network \& VLAN Setup



\## VLANs

\- VLAN 10: Servers (Radarr, Sonarr, Lidarr, Bazarr, Transmission @192.168.10.115)



\## Key ER-4 Firewall Rules (from config)

\- LAN\_IN Rule 19: Allow VPN → VLAN10 Services (ports 445, 9000, 7878, 20489)

\- LAN\_IN Rule 30: Allow VLAN10 → Internet

\- LAN\_IN Rule 40: Allow VLAN20 → Internet



\## SMB Requirements

\- Port 445 allowed from RPi to TrueNAS

