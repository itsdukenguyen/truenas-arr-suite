# 12 - Troubleshooting

**Last Updated:** July 2025

## Common Issues & Solutions

| Issue                              | Possible Cause                     | Solution |
|------------------------------------|------------------------------------|--------|
| Mount disappears after reboot      | Missing `/etc/fstab` entry        | Add UUID mount and run `sudo mount -a` |
| Transmission daemon won't start    | Permission or config error         | Check `journalctl -u transmission-daemon` |
| GUI and Web not syncing            | GUI using local config             | Clear `~/.config/transmission` and connect remotely |
| Path does not exist in *arr apps   | Incorrect Remote Path Mapping      | Map `/mnt/SSD1/Downloads/complete` → `/mnt/TrueNAS/Downloads/complete` |
| SMB mount fails on RPi             | Credentials or permissions         | Verify `/root/.smbcredentials` and `uid=pi,gid=pi` |
| Firewall / Port 9091 blocked       | ER-4 or local firewall             | Check LAN_IN Rule 19 + `sudo iptables -L` |
| Downloads not moving to TrueNAS    | Post-processing script or mapping  | Verify move script and Remote Path Mapping |

## Transmission GUI + Web Sync Issues

1. Check running processes:
   ```bash
   ps aux | grep transmission
   sudo systemctl status transmission-daemon
   
   
rm -rf ~/.config/transmission