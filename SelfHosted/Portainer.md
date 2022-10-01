---
title: Portainer
description: 
published: true
date: 2022-10-01T19:28:45.095Z
tags: 
editor: markdown
dateCreated: 2022-01-18T11:59:56.767Z
---

![portainer_banner.png](/wiki-assets/portainer_banner.png)

# Présentation

Site officiel : [portainer.io](https://www.portainer.io/)

**portainer** est un outil très populaire sur docker car il permet de donner une interface web à docker. Vous pouvais créer et gérer vos containers docker sur votre navigateur web. C'est un outil très complet et très pratique au quotidien.

# Installation
# Tabs {.tabset}
## Docker-Compose
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
## Docker cli
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

# Portainer-Agent
```bash
version: '3.3'
services:
  agent:
    ports:
      - '9001:9001'
    container_name: portainer_agent
    restart: always
    volumes:
      - '/var/run/docker.sock:/var/run/docker.sock'
      - '/var/lib/docker/volumes:/var/lib/docker/volumes'
    image: 'portainer/agent:latest'
```