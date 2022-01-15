---
title: WikiJS
description: 
published: true
date: 2022-01-15T09:11:49.708Z
tags: 
editor: markdown
dateCreated: 2022-01-14T20:22:17.789Z
---

![wikijs-logo.png](/wiki-assets/wikijs-logo.png =400x){.align-center}
 
 
# Présentation
**Wiki.js** comme son nom l’indique est une solution pour créer un wiki open source coder en javascript. Il est très moderne et facile d’utilisation. Avec quelques compétences en Markdown et en CSS on peux faire de très jolie wiki, et facile d'utilisation que se soit pour le lecteur mais également pour l'administrateur.
 
Il dispose d'intégration très intéressante comme Google Analytics, Github pour le stockage des données ou encore disqus pour le système de commentaire. 
 
C'est d'ailleurs la solution que j'ai choisit pour créer ce wiki. 
 
Site officiel : [js.wiki](https://js.wiki/)
 
 
# Installation
# Tabs {.tabset}
## Bare Metal
> Ce tutoriel est effectué sur une Debian 11
{.is-info}
 
### Prérequis
- Adresse IP fixe
 
### Installation des paquets requis
```bash
apt update && full-upgrade -y
apt install nodejs apache2 postgresql -y
```
### Configuration de PostgreSQL
```bash
su - postgres
createuser -d -P wikijsuser
createdb -O wikijsuser wikijs
su - root
```
### Installation de Wiki.js
```bash
> Vous pouvez trouver la dernière version ici : https://github.com/Requarks/wiki/releases
{.is-info}
 
cd /tmp
wget https://github.com/Requarks/wiki/releases/download/2.5.201/wiki-js.tar.gz
mkdir /var/www/wikijs
tar xzf wiki-js.tar.gz -C /var/www/wikijs
rm wiki-js.tar.gz
 
cd /var/www/wikijs
mv config.sample.yml config.yml
vim config.yml
```
Dans le fichier config.yml renseignez :
- user: wikijsuser
- pass: le mot de passe créer précédemment
- db: wikijs
 
```bash
cd /var/www/wikijs/data
mkdir cache
mkdir uploads
chmod -R 777 ./cache
chmod -R 777 ./uploads
```
### Créer un service systemd
```bash
vim /etc/systemd/system/wiki.service
```
![wikijs-1.jpg](/self-hosted/wikijs/wikijs-1.jpg)
 
```bash
systemctl daemon-reload
systemctl start wiki
systemctl enable wiki
```
 
> WikiJS est installé, vous pouvez y accéder à l'adresse : http://votre_ip:3000
{.is-success}
 
> Pour avoir un certificat SSL, vous pouvez utiliser un reverse proxy.
{.is-info}
 
 
 
## Docker-Compose
```yaml
version: "3"
services:
  db:
    image: postgres:11-alpine
    environment:
      POSTGRES_DB: wiki
      POSTGRES_PASSWORD: wikijsrocks
      POSTGRES_USER: wikijs
    logging:
      driver: "none"
    restart: unless-stopped
    volumes:
      - db-data:/var/lib/postgresql/data
 
  wiki:
    image: requarks/wiki:2
    depends_on:
      - db
    environment:
      DB_TYPE: postgres
      DB_HOST: db
      DB_PORT: 5432
      DB_USER: wikijs
      DB_PASS: wikijsrocks
      DB_NAME: wiki
    restart: unless-stopped
    ports:
      - "80:3000"
 
volumes:
  db-data:
```
## Docker cli 
```bash
docker run -d \
  --name=wikijs \
  -e PUID=1000 \
  -e PGID=100 \
  -e TZ=Europe/Paris \
  -p 3000:3000 \
  -v /path/to/config:/config \
  -v /path/to/data:/data \
  --restart unless-stopped \
  lscr.io/linuxserver/wikijs
```
 
> Utiliser cette commande uniquement pour du test (stack docker-compose pour la prod).
{.is-warning}
 
 
# Configurations
## Github en stockage
 
Vous pouvez stocker toutes vos pages, images sur Github. Pour ce faire, allez dans le panneau d'administration de WikiJS puis dans stockage sélectionnez git. N'oubliez pas d'appliquer une fois la configuration terminée
 
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