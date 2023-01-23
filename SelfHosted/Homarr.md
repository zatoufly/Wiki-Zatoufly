---
title: Homarr
description: 
published: true
date: 2023-01-23T20:55:23.066Z
tags: 
editor: markdown
dateCreated: 2023-01-23T20:55:23.065Z
---

Site du projet : [homer.dev](https://homarr.dev/)

# Autres contenus
- [📽️ Youtube *Titre vidéo*](https://youtube.com/@zatoufly)
- [📄 Article *Titre article*](https://zatoufly.fr)
{.links-list}

# Installation
# Tabs {.tabset}

## Docker Compose 
```yaml
version: '3'
services:
  homarr:
    container_name: homarr
    image: ghcr.io/ajnart/homarr:latest
    restart: unless-stopped
    volumes:
      - config:/app/data/configs
      - icons:/app/public/icons
    ports:
      - '7575:7575'

volumes:
  config:
  icons:
```
## Docker CLI

## Serveur dédié
