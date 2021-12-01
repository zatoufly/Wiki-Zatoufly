---
title: WatchTower
description: 
published: 1
date: 2021-12-01T22:40:21.258Z
tags: 
editor: markdown
dateCreated: 2021-12-01T22:40:21.258Z
---

![watchtower-banner.png](/wiki-assets/watchtower-banner.png)

# Présentation
**Watchtower** permet de mettre à jour automatiquement vos conteneurs docker. Il va simplement comparer votre image et la dernière disponible sur le docker hub, si il détecte une différence watchtower va pull l'image et mettre à jour le conteneur.

Site officiel : [containrrr.dev](https://containrrr.dev/watchtower/)


# Installation

## Docker-Compose ([Plus d'informations](https://docs.linuxserver.io/general/docker-compose))
```yaml
version: '3'
services:
  watchtower:
    image: containrrr/watchtower
    container_name: watchtower
    restart: unless-stopped
    environment:
      WATCHTOWER_SCHEDULE: "0 0 4 * * *"
      WATCHTOWER_CLEANUP: "true"
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock

```
## Docker cli ([Plus d'informations](https://docs.docker.com/engine/reference/commandline/cli/))

```bash
docker run -d \
    --name watchtower \
    --restart=unless-stopped \
    -e WATCHTOWER_SCHEDULE="0 0 4 * * *" \
    -e WATCHTOWER_CLEANUP="true" \
    -e TZ="Europe/Paris" \
    -v /var/run/docker.sock:/var/run/docker.sock \
    containrrr/watchtower
```
# Configurations
|     |     |
| --- | --- |
| `WATCHTOWER_SCHEDULE` | Permet de modifier le fréquences des mises à jour (tous les jour à 4h par défaut) |
| `WATCHTOWER_CLEANUP` | Supprimer les anciennes images non utiliser |


