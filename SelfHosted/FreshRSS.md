---
title: FreshRSS
description: 
published: 1
date: 2021-12-01T09:46:42.183Z
tags: 
editor: markdown
dateCreated: 2021-12-01T09:10:33.180Z
---

![freshrss-logo.png](https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Ffreshrss.github.io%2FFreshRSS%2Fen%2Fimg%2Flogo_freshrss.png&f=1&nofb=1)

# Présentation
**FreshRSS** est un agrégateur de Flux RSS à l'instar du celèbre Feedly. C'est une excellente solution pour faire votre vieille technologique. Fresh RSS est rapide, responsive pour une utilisation sur smartphone.

C'est la solution que j'utilise au quotidien, le mien est d'ailleur public : news.zatoufly.fr

Site officiel : [freshrss.org](https://www.freshrss.org/)

# Installation
## Bare Metal
- [:memo: Tuto sur mon blog *zatoufly.fr*](https://zatoufly.fr/installer-freshrss-sur-debian)
- [:camera: Tuto en vidéo *sur youtube*](https://www.youtube.com/watch?v=VXPtwcxRf1E)
{.links-list}
## Docker-Compose ([Plus d'informations](https://docs.linuxserver.io/general/docker-compose))
```yaml
---
version: "2.1"
services:
  freshrss:
    image: lscr.io/linuxserver/freshrss
    container_name: freshrss
    environment:
      - PUID=1000
      - PGID=100
      - TZ=Europe/Paris
    volumes:
      - <path to config>:/config
    ports:
      - 3001:80
    restart: unless-stopped
```
## Docker cli ([Plus d'informations](https://docs.docker.com/engine/reference/commandline/cli/))
```bash
docker run -d \
  --name=freshrss \
  -e PUID=1000 \
  -e PGID=100 \
  -e TZ=Europe/Paris \
  -p 3001:80 \
  -v <path to config>:/config \
  --restart unless-stopped \
  lscr.io/linuxserver/freshrss
```
# Configurations
Si vous avez effectuer une installation via Docker, séléctionnez LiteSQL lors de la configuration de la base de données.  

