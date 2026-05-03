# 12 - Troubleshooting

**Last Updated:** July 2025

## Common Issues & Solutions

| Issue                                | Possible Cause                    | Solution |
|--------------------------------------|-----------------------------------|--------|
| Mount disappears after reboot        | Missing fstab entry               | Add UUID mount + `sudo mount -a` |
| Transmission daemon won't start      | Config / permission error         | `journalctl -u transmission-daemon -xe` |
| GUI and Web not syncing              | Local config conflict             | `rm -rf ~/.config/transmission` + configure Remote |
| Path does not exist in *arr apps     | Wrong Remote Path Mapping         | Map `/mnt/SSD1/Downloads/complete` → TrueNAS path |
| SMB mount fails on RPi               | Credentials issue                 | Check `/root/.smbcredentials` |
| Firewall / Port 9091 blocked         | ER-4 or local rules               | Verify LAN_IN Rule 19 |

## Transmission GUI + Web Sync

```bash
ps aux | grep transmission
sudo systemctl status transmission-daemon
rm -rf ~/.config/transmission
transmission-gtk