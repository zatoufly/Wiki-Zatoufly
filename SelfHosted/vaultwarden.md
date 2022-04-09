---
title: VaultWarden
description: 
published: true
date: 2022-04-09T11:26:00.174Z
tags: 
editor: markdown
dateCreated: 2022-04-09T11:26:00.174Z
---

# Présentation
**Vaultwarden** est une solution de gestionnaire de mot de passes. Vaultwarden est le projet open source de la société Bitwarden.
 
Vaultwarden peux donc s'installer gratuitement sur son propre serveur et permet d'avoir ses mot de passes héberger chez soi. Il s'installe via Docker.
 
# Installation
# Tabs {.tabset}
## Docker-Compose
```yaml
version: '3.3'
services:
  server:
    restart: always
    container_name: vaultwarden
    volumes:
      - '/srv/docker/vaultwarden/data:/data/'
    ports:
      - '8000:80'
    image: vaultwarden/server:1.24.0
```