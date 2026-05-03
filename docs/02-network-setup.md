\# 02 - Network \& VLAN Setup



\## VLAN Configuration



\- \*\*VLAN 10 (Servers)\*\*: Radarr, Sonarr, Lidarr, Bazarr, Transmission (`192.168.10.115`)



\## Key EdgeRouter 4 Firewall Rules



| Rule | Description                              | Source          | Destination     | Ports          |

|------|------------------------------------------|-----------------|-----------------|----------------|

| 19   | Allow VPN → VLAN10 Services              | `100.64.0.0/10` | VLAN 10         | 445, 9000, etc.|

| 30   | Allow Servers → Internet                 | VLAN 10         | Internet        | Any            |

| 40   | Allow IoT → Internet                     | VLAN 20         | Internet        | Any            |



\## SMB Requirements

\- Port \*\*445\*\* must be allowed from Raspberry Pi to TrueNAS

