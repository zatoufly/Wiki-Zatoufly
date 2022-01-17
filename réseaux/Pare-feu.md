---
title: Dydns OVH sur Pfsense
description: Configuration d'un Dydns OVH sur Pfsense
published: true
date: 2022-01-17T16:45:31.845Z
tags: ovh, pfsense, firewall, dydns, dns dynamique, ddns
editor: markdown
dateCreated: 2022-01-17T16:41:03.934Z
---

# Introduction

Un DNS dynamique est une méthode pour mettre à jour automatiquement un serveur DNS, souvent en temps réel. 
Dans notre cas , il sert plus precisement à mettre à jour la liaison entre votre nom de domaine et votre ip à jour en temps réel

# Configuration sur OVH

Une fois votre nom de domaine acheter , et activer chez ovh, vous aurez acces a une page regroupant tout les noms de domaines et hébergement vous appartenant , cliqué sur le domaine que vous voulez lier à votre réseau:

![1.png](/reseau/pare-feu/ovh-pfsense/1.png)

Ce qui vous redirige sur une nouvelle page, cliqué sur "Dynhost":

![2.2.png](/reseau/pare-feu/ovh-pfsense/2.2.png)

Ce qui affichera cette page:

![3.png](/reseau/pare-feu/ovh-pfsense/3.png)

Dans un premier temps, nous allons crée le DynHost, pour cela , cliquer sur "Ajouter un DynHost":

![4.png](/reseau/pare-feu/ovh-pfsense/4.png)

Vous allez donc indiquez un sous domaine qui sera utiliser pour la redirection , et votre ip public:

![5.png](/reseau/pare-feu/ovh-pfsense/5.png)

Puis cliquer sur "valider", nous allons ensuite crée un accès pour notre pfsense, pour cela, cliqueé sur "Gérer les accès":

![6.png](/reseau/pare-feu/ovh-pfsense/6.png)

Puis sur "Créer un identifiant":

![7.png](/reseau/pare-feu/ovh-pfsense/7.png)

Sur cette page, vous allez donc crée un identifiant (qui commencera par le nom de domaine), indiquer le sous domaine precedement crée et crée un mot de passe:

![8.png](/reseau/pare-feu/ovh-pfsense/8.png)

Une fois ce formulaire remplis, il ne vous reste plus qu'a validé. 

# Configuration sur Pfsense

Maintenant que nous avons un compte pour gerer ce domaine, il faut vous rendre sur l'interface de votre Pfsense personnel, allez dans "Services", puis dans "DNS Dynamique"

![9.png](/reseau/pare-feu/ovh-pfsense/9.png)

Cliquez sur "ajouter"

![10.png](/reseau/pare-feu/ovh-pfsense/10.png)

Vous allez donc mettre , si elle n'est mise par defaut, votre interface Wan dans "interface à superviser", inquez egalement les informations que vous avez precedement configurer sur ovh.
Donc dans "nom d'hote" , indiquez votre nom de domaine precedé du sous-domaine crée precedement, puis indiquer le "nom d'utilisateur" crée precedement ainsi sur le "mot de passe" , deux fois.
Et pour finir, Enregistrer

![11.png](/reseau/pare-feu/ovh-pfsense/11.png)
![12.png](/reseau/pare-feu/ovh-pfsense/12.png)

Ce qui devrais vous afficher un état vert sur la page precedente.

![13.png](/reseau/pare-feu/ovh-pfsense/13.png)
