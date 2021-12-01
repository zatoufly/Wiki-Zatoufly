---
title: FreshRSS
description: 
published: 1
date: 2021-12-01T09:10:33.180Z
tags: 
editor: markdown
dateCreated: 2021-12-01T09:10:33.180Z
---

![wikijs-logo.png](/wiki-assets/wikijs-logo.png)

# Présentation
**FreshRSS** est un agrégateur de Flux RSS à l'instar du celèbre Feedly. C'est un excellente solution pour faire votre vieille technologique. Fresh RSS est rapide, responsive pour une utilisation sur smartphone.

C'est la solution que j'utilise au quotidien, le mien est d'ailleur public : news.zatoufly.fr

Site officiel : [freshrss.org](https://www.freshrss.org/)

<div class="video-responsive">
<iframe width="560" height="315" src="https://www.youtube.com/embed/Cisg9bLhLkk" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>


# Installation
## Bare Metal
[Tuto sur mon Blog](https://zatoufly.fr/installer-freshrss-sur-debian/)
## Docker-Compose ([Plus d'informations](https://docs.linuxserver.io/general/docker-compose))
```
version: "2.1"
services:
  wikijs:
    image: lscr.io/linuxserver/wikijs
    container_name: wikijs
    environment:
      - PUID=1000
      - PGID=100
      - TZ=Europe/Paris
    volumes:
      - <path to config>:/config
      - <path to data>:/data
    ports:
      - 3000:3000
    restart: unless-stopped
```
## Docker cli ([Plus d'informations](https://docs.docker.com/engine/reference/commandline/cli/))
```
docker run -d \
  --name=wikijs \
  -e PUID=1000 \
  -e PGID=100 \
  -e TZ=Europe/Paris \
  -p 3000:3000 \
  -v <path to config>:/config \
  -v <path to data>:/data \
  --restart unless-stopped \
  lscr.io/linuxserver/wikijs
```
# Configurations
## Github en stockage

Vous pouvez stocker toutes vos pages, images sur Github. Pour ce faire allez dans le panneau d'administration de WikiJS puis dans stockage séléctionnez git. Oubliez pas d'appliquer une fois la configuration terminer

Il vous faudra créer un repository sur votre compte github, ainsi qu'un token avec les permissions repo uniquement. [Comment créer un token sur github](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token)

![wikijs-git-config.jpg](/wiki-assets/wikijs-git-config.jpg)

## Enlever la table des matières

Pour enlever la table des matières d'une page, éditer la page en question et cliquez sur le bouton "page" en haut à droite, dans l'onglet "styles" insérez le code CSS ci-dessous :

![wikijs-table-des-matieres.jpg](/wiki-assets/wikijs-table-des-matieres.jpg)

Pour enlever la table des matières :

```
.page-col-sd {
  margin-top: 0;
  align-self: flex-start;
  position: sticky;
  top: 64px;
  max-height: calc(100vh - 64px);
  overflow-y: auto;
  -ms-overflow-style: none;
  display: none
}
.flex.lg9 {
  flex-basis: 100%!important;
  flex-grow: 0;
  max-width: 100%!important
}
```
Pour enlever la table des matières et le bandeau de titre :
```
.page-col-sd {
  margin-top: 0;
  align-self: flex-start;
  position: sticky;
  top: 64px;
  max-height: calc(100vh - 64px);
  overflow-y: auto;
  -ms-overflow-style: none;
  display: none
}
.flex.lg9 {
  flex-basis: 100%!important;
  flex-grow: 0;
  max-width: 100%!important
}
.row.no-gutters.align-content-center {
  display: none
}
```
