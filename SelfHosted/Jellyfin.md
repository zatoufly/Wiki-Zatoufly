---
title: Jellyfin
description: 
published: 1
date: 2021-12-12T10:59:09.002Z
tags: 
editor: markdown
dateCreated: 2021-12-12T10:56:23.231Z
---

# Présentation
**Jellyfin** est un serveur multimédia, fork de Emby. C'est un projet open source et une très bonne alternative à plex.

Site officiel : [jellyfin.org](https://jellyfin.org/)

# Installation
# Tabs {.tabset}
## Bare Metal

- [:memo: Tuto sur mon site *zatoufly.fr*](https://zatoufly.fr/comment-installer-jellyfin-sur-debian/)
{.links-list}

## Docker-Compose
```yaml
version: '3.3'
services:
  jellyfin:
      container_name: jellyfin
      volumes:
          - '/path/to/config:/config'
          - '/path/to/cache:/cache'
          - '/path/to/media:/media'
      network_mode: host
      restart: unless-stopped
      image: jellyfin/jellyfin
```
Pour la configuration sur l'interface web :
- [:memo: Tuto sur mon site *zatoufly.fr*](https://zatoufly.fr/comment-installer-jellyfin-sur-debian/)
{.links-list}

## Docker cli
```bash
docker run -d \
--name=jellyfin \
--user 1000:100 \
-v /path/to/config:/config \
-v /path/to/cache:/cache \
-v /path/to/media:/media \
--net="host" \
--restart=unless-stopped \
jellyfin/jellyfin
```
Pour la configuration sur l'interface web :
- [:memo: Tuto sur mon site *zatoufly.fr*](https://zatoufly.fr/comment-installer-jellyfin-sur-debian)
{.links-list}