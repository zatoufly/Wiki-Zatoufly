---
title: Dydns OVH sur Pfsense
description: Configuration d'un Dydns OVH sur Pfsense
published: true
date: 2022-02-07T12:30:03.204Z
tags: ovh, pfsense, firewall, dydns, dns dynamique, ddns
editor: markdown
dateCreated: 2022-01-18T12:00:25.117Z
---

# Introduction

Un DNS dynamique est une méthode pour mettre à jour automatiquement un serveur DNS, souvent en temps réel.


Dans notre cas, il sert plus précisément à mettre à jour la liaison entre votre nom de domaine, et votre ip, en temps réel




# Configuration sur OVH




Une fois votre nom de domaine acheté , et activer chez ovh, vous aurez accès a une page regroupant tous les noms de domaines et hébergement vous appartenant, cliqué sur le domaine que vous voulez lier à votre réseau :




![1.png](/reseau/pare-feu/ovh-pfsense/1.png)




Ce qui vous redirige sur une nouvelle page, cliqué sur "Dynhost":




![2.2.png](/reseau/pare-feu/ovh-pfsense/2.2.png)




Ce qui affichera cette page :




![3.png](/reseau/pare-feu/ovh-pfsense/3.png)




Dans un premier temps, nous allons créer le DynHost, pour cela, cliquer sur "Ajouter un DynHost":




![4.png](/reseau/pare-feu/ovh-pfsense/4.png)




Vous allez donc indiquez un sous-domaine qui sera utilisé pour la redirection, et votre ip public :




![5.png](/reseau/pare-feu/ovh-pfsense/5.png)




Puis cliquer sur "valider", nous allons ensuite créer un accès pour notre pfsense, pour cela, cliquer sur "Gérer les accès":




![6.png](/reseau/pare-feu/ovh-pfsense/6.png)




Puis sur "Créer un identifiant":




![7.png](/reseau/pare-feu/ovh-pfsense/7.png)




Sur cette page, vous allez donc crée un identifiant (qui commencera par le nom de domaine), indiquer le sous-domaine précédemment crée et crée un mot de passe :




![8.png](/reseau/pare-feu/ovh-pfsense/8.png)




Une fois ce formulaire rempli, il ne vous reste plus qu'à valider.




# Configuration sur Pfsense




Maintenant que nous avons un compte pour gérer ce domaine, il faut vous rendre sur l'interface de votre Pfsense personnel, allez dans "Services", puis dans "DNS Dynamique"




![9.png](/reseau/pare-feu/ovh-pfsense/9.png)




Cliquez sur "ajouter"




![10.png](/reseau/pare-feu/ovh-pfsense/10.png)




Vous allez donc mettre, si elle n'est pas mise par défaut, votre interface Wan dans "interface à superviser", indiquez également les informations que vous avez précédemment configurées sur votre domaine.


Donc dans "nom d'hôte" , indiquez votre nom de domaine précédé du sous-domaine crée précédemment , puis indiquer le "nom d'utilisateur"  ainsi que le "mot de passe" que vous avez créés sur ovh , deux fois.


Et pour finir, Enregistrer




![11.png](/reseau/pare-feu/ovh-pfsense/11.png)


![12.png](/reseau/pare-feu/ovh-pfsense/12.png)




Ce qui devrait vous afficher un état vert sur la page précédente.




![13.png](/reseau/pare-feu/ovh-pfsense/13.png)
