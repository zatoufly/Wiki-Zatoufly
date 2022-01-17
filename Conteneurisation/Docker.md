---
title: Docker
description: 
published: true
date: 2022-01-17T09:51:10.452Z
tags: 
editor: markdown
dateCreated: 2022-01-17T09:51:10.452Z
---

# Introduction
Docker est la solution de conteneurisation la plus populaire. Il permet d'isoler des applications de la machine hôte et fait preuve d'une grande facilité de déploiement et de gestion des conteneurs.
 
# Installation
```bash
apt install docker.io
```
 
# Commandes
```bash
docker ps # liste les containers démarrer
docker ps -a # liste tous les containers
docker exec -ti [nom] sh # se connecter à un container
docker inspect [nom] # affiche la propriété du container
docker start [nom] # démarre un container
docker stop [nom] # arrête un container
docker rm [nom] # supprime un container
-f # forcer la suppression
docker rm -f ${docker ps -aq} # supprime tous les conteneurs   
 
docker system prune # Fait le ménage (containeur arrêter et image non utiliser)
-a # mêmes choses avec volume + images pas utilisé
docker search [app] # cherche une image dans le hub docker
 
docker run [image]:[version] # lance une image
-d # Détache le conteneur du processus principal de la console
-i # interactive
--name [nom] # nomme le container
-p [port hôte]:[port container] # rédigez un port du container vers l'hôte
-v [/path_local]:[/path_docker] # Monter un volume (la data de /chemin_docker est stocké sur l'hôte)
--mount source=[nom_volume],target=/usr/share/nginx/html # monte un volume local sur le container
-e [nom variable]="contenue variable" # passez un variable d'environnement 
--env-file [nom_fichier] # passez un fichier qui contient des variables d'environnement
--hostname [nom_host] # définit un hostname pour le container
 
 
# docker volume 
docker volume create [nom_volume] # créer un volume
docker volume ls # liste les volume
docker volume inspect [nom_volume] # affiche les propriété du volume
docker volume rm [nom_volume] # supprimer un volume non utiliser
docker volume prune # supprimer les volumes non utilisé
 
 
# docker image
docker commit -m "commentaire" [ID container] [nomimage]:[version] # créer une image à partir d'un container
docker image ls # voir les images disponible sur l'hôte
docker history [nomimage] # voir l'historique de l'image
docker image rm [IDimage] # supprime une image
docker rmi [image] # supprimer une image
```
 
## Docker File
Le Dockerfile est un fichier de configuration qui a pour objectif de créer une image docker. Il dispose de plusieurs séquences d'instruction (layers) afin de créer l'image de manière ordonnée.
 
```bash
FROM ubuntu:latest     # Définie l'image utiliser pour la base de l'image
MAINTAINER zatoufly
COPY # copie entre host et conteneur
ENV # variables d'environnement                
RUN apt update \       # Exécute des commandes dans le conteneur
&& apt install -y vim git
ADD . /app/ # copie ou télécharge des fichiers dans l'image 
WORKDIR /app # modifie le répertoire courant (équivalent cd)
EXPOSE # exposer des ports
VOLUME /var/www/html   # définition de volumes
CMD ["--help"] # Commande exécuter lors du démarrage / paramètre par défaut lors du démarrage
ENTRYPOINT ["ping"] # processes maître / processus de base du conteneur
```
```bash
docker build -t monimage:v1.0 . # Créer une image à partir du dockerfile
```
 
## Réseau
Les conteneurs docker ne possèdent pas d'ip fixe, l'ip changera une fois un conteneur redémarrer.
L'interface par défaut de docker est nommé "Docker0" on l'appel également le "bridge docker"
 
# Docker-Compose
## Introduction
Docker-Compose permet de lancer un ensemble de conteneurs appelés "services". Les services du docker-compose sont dans le même réseau et peuvent ainsi communiquer pour se partager des données entre eux.
 
Pour créer un docker compose, il faut créer un fichier au format .yaml et y noter les services (conteneurs) que l'on souhaite exécuter. Une stack connue est par exemple une application web avec sa base de données.
 
il est possible de transformer une "commande docker" pour lancer un conteneur en service docker compose via ce projet : https://www.composerize.com/
 
Voici un exemple de stack docker compose wordpress au format yaml :
```yaml
# définition de la version de docker compose
version: "2" 
 
# définition des différent services
services: 
   # service mysql pour la bdd de wordpress
   wordpress-db:
     container_name: wordpress-db
     image: mysql:5.7
     volumes:
       - /path/to/db:/var/lib/mysql
     restart: unless-stopped
     environment:
       MYSQL_ROOT_PASSWORD: root-password
       MYSQL_DATABASE: wordpress
       MYSQL_USER: utilisateur
       MYSQL_PASSWORD: password
       
   # service qui exécute un serveur web et wordpress
   wordpress:
     container_name: wordpress
     # option qui permet d'attendre que le service "wordpress-db" soit exécuté avant de démarrer
     depends_on:
       - wordpress-db
     image: wordpress:latest
     ports:
       - 80:80
     restart: unless-stopped
     volumes:
       - /path/to/uploads.ini:/usr/local/etc/php/conf.d/uploads.ini
       - /path/to/html:/var/www/html
     environment:
       WORDPRESS_DB_HOST: wordpress-db:3306
       WORDPRESS_DB_USER: utilisateur
       WORDPRESS_DB_PASSWORD: password
       WORDPRESS_DB_NAME: wordpress
```
 
 
## Installation
```bash
apt install docker-compose
```
 
## Commandes
```bash
docker-compose build # construit les images du yml
docker-compose up # build et run le simages
docker-compose up -d # mode détaché
 
docker-compose ps # état des services
docker-compose start # redémarre les conteneurs du service
docker-compose stop # stop les conteneurs du service
docker-compose rm # supprimer les services
 
docker-compose pull # met à jour les images 
```