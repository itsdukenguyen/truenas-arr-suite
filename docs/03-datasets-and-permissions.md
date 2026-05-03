# 03 - Datasets and Permissions

## Dataset Structure
- Apps: `DataPool/apps/radarr`, `/sonarr`, `/lidarr`, `/bazarr`
- Media: `DataPool/Media/Movies`, `/Shows`, `/Music`

## Screenshots
![Jellyfin](../screenshots/01-jellyfin-dataset-structure.png)
![Radarr](../screenshots/01-radarr-dataset-structure.png)
![Sonarr](../screenshots/01-sonarr-dataset-structure.png)
![Lidarr](../screenshots/01-lidarr-dataset-structure.png)
![Bazarr](../screenshots/01-bazarr-dataset-structure.png)

## Permissions
```bash
chown -R mediauser:mediausers /mnt/DataPool/Media
chmod -R 775 /mnt/DataPool/Media