---
title: LibreSpeed
description: 
published: 1
date: 2022-01-06T19:08:39.429Z
tags: 
editor: markdown
dateCreated: 2022-01-06T19:08:39.429Z
---

# Présentation
**LibreSpeed** est une solution de speedtest pour tester la vitesse de son réseau.
 
On peut l'installer sur une machine sur son réseau local pour tester la vitesse de son réseau local. On peut également l'installer sur un serveur distant pour avoir sa propre solution de speedtest et connaître la vitesse de sa connexion internet.
 
# Installation
# Tabs {.tabset}
## Docker-Compose
```yaml
version: "2.1"
services:
  librespeed:
    image: lscr.io/linuxserver/librespeed
    container_name: librespeed
    environment:
      - PUID=100
      - PGID=1000
      - TZ=Europe/Paris
      - PASSWORD=PASSWORD
      - CUSTOM_RESULTS=false #optional
      - DB_TYPE=sqlite #optional
      - DB_NAME=DB_NAME #optional
      - DB_HOSTNAME=DB_HOSTNAME #optional
      - DB_USERNAME=DB_USERNAME #optional
      - DB_PASSWORD=DB_PASSWORD #optional
      - DB_PORT=DB_PORT #optional
    volumes:
      - /path/to/appdata/config:/config
    ports:
      - 5353:80
    restart: unless-stopped
```
## Docker cli
```bash
docker run -d \
  --name librespeed \
  -e PUID=1000 \
  -e PGID=100 \
  -e TZ=Europe/Paris \
  -e PASSWORD=PASSWORD
  -e CUSTOM_RESULTS=false #optional
  -e DB_TYPE=sqlite #optional
  -e DB_NAME=DB_NAME #optional
  -e DB_HOSTNAME=DB_HOSTNAME #optional
  -e DB_USERNAME=DB_USERNAME #optional
  -e DB_PASSWORD=DB_PASSWORD #optional
  -e DB_PORT=DB_PORT #optional
  -p 5353:80 \
  -v /path/to/appdata/config:/config \
  --restart unless-stopped \
  lscr.io/linuxserver/librespeed
```