---
title: Funkwhale
description: 
published: 1
date: 2021-12-02T22:12:18.434Z
tags: 
editor: markdown
dateCreated: 2021-12-02T22:12:18.434Z
---

![funkwhale-banner.png](/wiki-assets/funkwhale-banner.png)

# Présentation
**Funkwhale** est un lecteur de musique open source dévellopé par des français "The Funkwhale Collective". Il permet d'accéder à toute votre bibliothèque via une interface web plutôt agréable à l'oeil, pas d'app malheureusement pour le moment.

Site officiel : [funkwhale.audio](https://funkwhale.audio/)

# Installation

## Docker-Compose ([Plus d'informations](https://docs.linuxserver.io/general/docker-compose))
```yaml
version: "3"
services:
  funkwhale:
    container_name: funkwhale
    restart: unless-stopped
    image: funkwhale/all-in-one:latest
    env_file: .env
    environment:
      - PUID=1000
      - PGID=100
    volumes:
      - /path/to/data:/data
      - /path/to/music:/music:ro
    ports:
      - "5000:80"
```
## Docker cli ([Plus d'informations](https://docs.docker.com/engine/reference/commandline/cli/))
```bash
docker run -d \
	--name funkwhale \
	-e PUID=1000 \
	-e PGID=100 \
	-p 5000:80 \
	-v /path/to/data:/data \
	-v /path/to/music:/music:ro \
	--restart unless-stopped \
	funkwhale/all-in-one:latest
```

Pour se connecter à l'interface web, il vous faudra créer un compte administrateur avant avec cette commande qui devrait êtr éxécuter sur la machine hôte du conteneur

```bash
docker exec -it funkwhale manage createsuperuser
```
Inscrivez le nom d'utilisateur, un mail et un mot de passe comme demandé lors de l'éxécution de la commande

> Vous pouvez vous connecter à l'interface de Funkwhale à l'adresse http://ip-hote:5000
{.is-success}