---
title: DuckDNS
description: 
published: true
date: 2022-02-08T12:47:06.945Z
tags: 
editor: markdown
dateCreated: 2022-02-08T12:47:06.945Z
---

# Introduction
DuckDNS est un DDNS gratuit est auto hébergeable qui permet de lié un adresse IP dynamique à un nom DNS fixe. On l'utilise souvent pour une utilisation domestique

# Installation
# Tabs {.tabset}
## Docker Compose
```yml
version: "2.1"
services:
  duckdns:
    image: lscr.io/linuxserver/duckdns
    container_name: duckdns
    environment:
      - TZ=Europe/Paris
      - SUBDOMAINS=mondomaine,mondomaine2
      - TOKEN=token #insérez votre token
      - LOG_FILE=false #optional
    volumes:
      - /path/to/duckdns/config:/config #optional
    restart: unless-stopped
```