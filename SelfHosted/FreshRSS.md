---
title: FreshRSS
description: 
published: 1
date: 2021-12-31T15:58:45.823Z
tags: 
editor: markdown
dateCreated: 2021-12-01T09:10:33.180Z
---

![freshrss-logo.png](https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Ffreshrss.github.io%2FFreshRSS%2Fen%2Fimg%2Flogo_freshrss.png&f=1&nofb=1){.align-center}


# Présentation
**FreshRSS** est un agrégateur de Flux RSS à l'instar du célèbre Feedly. C'est une excellente solution pour faire votre veille technologique. Fresh RSS est rapide mais également responsive pour une utilisation sur smartphone.

C'est la solution que j'utilise au quotidien, le mien est d'ailleur public : news.zatoufly.fr

Site officiel : [freshrss.org](https://www.freshrss.org/)

# Installation
# Tabs {.tabset}
## Bare Metal
- [:memo: Tuto sur mon blog *zatoufly.fr*](https://zatoufly.fr/installer-freshrss-sur-debian)
- [:camera: Tuto en vidéo *sur youtube*](https://www.youtube.com/watch?v=VXPtwcxRf1E)
{.links-list}
## Docker-Compose
```yaml
version: '3.3'
services:
    freshrss:
        container_name: freshrss
        environment:
            - PUID=1000
            - PGID=100
            - TZ=Europe/Paris
        ports:
            - '3001:80'
        volumes:
            - '/path/to/data:/var/www/FreshRSS/data'
            - '/path/to/extensions:/var/www/FreshRSS/extensions'
        restart: unless-stopped
        image: freshrss/freshrss
```
## Docker cli
```bash
docker run -d \
  --name=freshrss \
  -e PUID=1000 \
  -e PGID=100 \
  -e TZ=Europe/Paris \
  -p 3001:80 \
  -v /path/to/data:/var/www/FreshRSS/data \
  -v /path/to/extensions:/var/www/FreshRSS/extensions \
  --restart unless-stopped \
  freshrss/freshrss
```
# Configurations
Si vous avez effectué une installation via Docker, sélectionnez liteQL lors de la configuration de la base de données.  


