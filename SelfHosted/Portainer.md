---
title: Portainer
description: 
published: 1
date: 2021-12-04T14:50:20.934Z
tags: 
editor: markdown
dateCreated: 2021-12-04T14:50:20.934Z
---

# Présentation

Site officiel : []()

# Installation
## Docker-Compose ([Plus d'informations](https://docs.linuxserver.io/general/docker-compose))
```yaml 
```
## Docker cli ([Plus d'informations](https://docs.docker.com/engine/reference/commandline/cli/))
```bash
docker run -d \
	--name portainer \
	-p 9000:9000 \ # port http
	-p 9443:9443 \ # port https
	-v /var/run/docker.sock:/var/run/docker.sock \
	-v /path/to/data:/data \
	--restart=unless-stopped \
	portainer/portainer-ce
```
