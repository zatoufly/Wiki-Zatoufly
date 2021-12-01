---
title: Uptime-Kuma
description: 
published: 1
date: 2021-12-01T16:08:57.680Z
tags: 
editor: markdown
dateCreated: 2021-12-01T16:08:57.680Z
---

![uptime-kuma-banner.png](/wiki-assets/uptime-kuma-banner.png)

# Présentation
**Uptime Kuma** est un service qui permet de faire de monitoring que se soit en local ou sur internet pour vos sites. Il dispose de sonde http(s), TCP, Ping, DNS, Push et même Steam Game Server, oui oui !

Il dispose également d'un système de notifications avec de très nombreuses intégrations. Vous pouvez notifier lors d'un incident via : Discord, SMTP, Telegram, Signal, Microsoft Teams, Slack, et bien plus. Bref il est simple et très complet.

C'est la solution que j'utilise pour mes sites, disponible ici : status.zatoufly.fr

Site officiel : [github.com/louislam/uptime-kuma](https://github.com/louislam/uptime-kuma)

# Installation
## Docker-Compose ([Plus d'informations](https://docs.linuxserver.io/general/docker-compose))
```yaml
---
version: "2.1"
services:
  uptime-kuma:
    image: louislam/uptime-kuma
    container_name: uptime-kuma
    volumes:
      - /path/to/data:/app/data
    ports:
      - 3001:3001
    restart: always
```
## Docker cli ([Plus d'informations](https://docs.docker.com/engine/reference/commandline/cli/))
```bash
docker run -d \
	--name uptime-kuma \
	-p 3001:3001 \
	-v /path/to/data:/app/data \
	--restart=always \
	louislam/uptime-kuma
```

