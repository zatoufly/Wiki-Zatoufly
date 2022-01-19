---
title: diun
description: 
published: true
date: 2022-01-19T11:16:25.902Z
tags: 
editor: markdown
dateCreated: 2022-01-18T12:00:20.870Z
---

# Introduction
Diun est une solution qui permet de vous envoyer des notifications lorsque qu'il détecte une nouvelle version d'une image sur un de vos conteneurs.

Contraitement à watchtower il vous envoyer uniquement des notifications mais il ne met pas à jour les conteneurs. 

# Installation
# Tabs {.tabset}
## Docker Compose

Il faudra créer le fichier diun.yml avant le lancement du conteneurs. Sinon docker va créer un répoertoire et non un fichier.

```yml
version: "3.5"

services:
  diun:
    image: crazymax/diun:latest
    container_name: diun
    command: serve
    volumes:
      - /path/to/diun/data:/data
      - /path/to/diun/data/diun.yml:/diun.yml:ro
      - /var/run/docker.sock:/var/run/docker.sock
    environment:
      - TZ=Europe/Paris
      - LOG_LEVEL=info
      - LOG_JSON=false
      - DIUN_WATCH_WORKERS=20
      - DIUN_WATCH_SCHEDULE=0 20 * * *
      - DIUN_PROVIDERS_DOCKER=true
    labels:
      - "diun.enable=true"
      - "diun.watch_repo=true"
    restart: always
```
