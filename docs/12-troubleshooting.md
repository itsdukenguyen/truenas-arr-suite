# 12 - Troubleshooting

## Common Issues & Solutions

| Issue                              | Solution |
|------------------------------------|--------|
| Mount disappears after reboot      | Use **Init/Shutdown Script** in TrueNAS |
| Path does not exist in *arr apps   | Check **Remote Path Mapping** (`/downloads`) |
| Duplicates in library              | Enable **Remove** in Completed Download Handling |
| Firewall / SMB issues              | Verify ER-4 **LAN_IN Rule 19** (port 445) |
| Subtitles not downloading          | Check Bazarr providers and API keys |
