\# 01 - Prerequisites



\## Hardware Used

\- TrueNAS SCALE server

\- Raspberry Pi 4 (Transmission + move script)

\- TL-SG3428XMP PoE Switch

\- Ubiquiti U6+ Access Points (x3)

\- EdgeRouter 4 (primary + cold backup)



\## EdgeRouter 4 Firewall Rules (Relevant)

\- Rule 19: Allow SMB (445), 9000, 7878, 20489 from VPN (`100.64.0.0/10`) to VLAN10

\- Rule 30: Allow Servers (VLAN10) to Internet

\- Rule 40: Allow IoT to Internet



\## Required Accounts

\- OpenSubtitles.com (Bazarr)

\- Prowlarr indexers

\- Jellyfin admin



\## Assumptions

\- VLAN 10 (Servers) is set up

\- Media user `mediauser` (UID 1003) + group `mediausers` (GID 1003) exist

