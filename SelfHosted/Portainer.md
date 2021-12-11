---
title: Portainer
description: 
published: 1
date: 2021-12-11T23:30:35.985Z
tags: 
editor: markdown
dateCreated: 2021-12-04T14:50:20.934Z
---

![portainer_banner.png](/wiki-assets/portainer_banner.png)

# Présentation

Site officiel : [portainer.io](https://www.portainer.io/)

**portainer** est un outil très populaire sur docker car il permet de donner une interface web à docker. Vous pouvais créer et gérer vos containers docker sur votre navigateur web. C'est un outil très complet et très pratique au quotidien.

# Installation
## Docker-Compose ([Plus d'informations](https://docs.linuxserver.io/general/docker-compose))
```yaml
version: '3.3'
services:
    portainer-ce:
        container_name: portainer
        ports:
            - '9000:9000' # port http
            - '9443:9443' # port https
        volumes:
            - '/var/run/docker.sock:/var/run/docker.sock'
            - '/path/to/data:/data'
        restart: unless-stopped
        image: portainer/portainer-ce
```
## Docker cli ([Plus d'informations](https://docs.docker.com/engine/reference/commandline/cli/))
```bash
docker run -d \
	--name portainer \
	-p 9000:9000 `# port http` \ 
	-p 9443:9443 `# port https` \ 
	-v /var/run/docker.sock:/var/run/docker.sock \
	-v /path/to/data:/data \
	--restart=unless-stopped \
	portainer/portainer-ce
```
