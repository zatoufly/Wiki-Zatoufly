---
title: Serveur RADIUS
description: 
published: true
date: 2022-02-26T21:45:57.922Z
tags: 
editor: markdown
dateCreated: 2022-02-26T21:45:57.922Z
---

# Introduction
**RADIUS** (Remote Authentication Dial-In User Service) est un protocole d'authentification client/serveur.  
 
# Prérequis
- un domaine Active Directory fonctionnel
 
# Installation
 
Sur Windows Server, le serveur RADIUS s'installe via le rôle NPS (Network Policy Server).
 
Dans le gestionnaire de serveur, cliquez sur "Gérer" puis "Ajouter des rôles et fonctionnalités"
![winsrv2022_install_radius_01.jpg](/microsoft/windows_server_2022/radius/winsrv2022_install_radius_01.jpg)
 
Cliquez sur "Suivant"
 
![winsrv2022_install_radius_02.jpg](/microsoft/windows_server_2022/radius/winsrv2022_install_radius_02.jpg)
 
Sélectionner le type d'installation "Installation basée sur un rôle ou une fonctionnalité"
 
![winsrv2022_install_radius_03.jpg](/microsoft/windows_server_2022/radius/winsrv2022_install_radius_03.jpg)
 
Sélectionner le serveur de destination (où sera installer le serveur RADIUS)
 
![winsrv2022_install_radius_04.jpg](/microsoft/windows_server_2022/radius/winsrv2022_install_radius_04.jpg)
 
Ajouter le rôle "Services de stratégie et d'accès réseau"
 
![winsrv2022_install_radius_05.jpg](/microsoft/windows_server_2022/radius/winsrv2022_install_radius_05.jpg)
 
Nous n'avons pas besoin de fonctionnalités supplémentaires, cliquez sur "Suivant"
 
![winsrv2022_install_radius_06.jpg](/microsoft/windows_server_2022/radius/winsrv2022_install_radius_06.jpg)
 
Cliquer sur "Suivant"
 
![winsrv2022_install_radius_07.jpg](/microsoft/windows_server_2022/radius/winsrv2022_install_radius_07.jpg)
 
Confirmer l'installation du rôle
 
![winsrv2022_install_radius_08.jpg](/microsoft/windows_server_2022/radius/winsrv2022_install_radius_08.jpg)
 
L'installation du rôle est terminée.
 
![winsrv2022_install_radius_09.jpg](/microsoft/windows_server_2022/radius/winsrv2022_install_radius_09.jpg)
 
# Configuration du rôle
## Création d'un profil
 
Une fois le rôle installer dans le gestionnaire de serveur cliquez sur "Outils" puis sur "Serveur NPS (Network Policy Server)"
 
![winsrv2022_radius_profil_01.jpg](/microsoft/windows_server_2022/radius/winsrv2022_radius_profil_01.jpg)
 
La fenêtre d'administration de RADIUS se lance. Pour ce tutoriel, on configure une stratégie de connexion à un réseau Wi-Fi. Dépliez le menu "Stratégie" et ajoutez une nouvelle stratégie.
 
![winsrv2022_radius_profil_02.jpg](/microsoft/windows_server_2022/radius/winsrv2022_radius_profil_02.jpg)
 
Nommez le nom de votre stratégie.
 
![winsrv2022_radius_profil_03.jpg](/microsoft/windows_server_2022/radius/winsrv2022_radius_profil_03.jpg)
 
Ajoutez une condition, et ajoutez "Groupes Windows"
 
![winsrv2022_radius_profil_04.jpg](/microsoft/windows_server_2022/radius/winsrv2022_radius_profil_04.jpg)
 
Ajoutez un nouveau groupe
 
![winsrv2022_radius_profil_05.jpg](/microsoft/windows_server_2022/radius/winsrv2022_radius_profil_05.jpg)
 
Ici je sélectionne "Utilisateur du domaine" qui contient tous les utilisateurs du domaine pour le tuto. Une bonne pratique serait de créer un groupe nommé "Accès Wi-Fi" et y insérer les utilisateurs souhaités par exemple.
 
Oublier pas de cliquez sur "Vérifier les noms" avant de cliquez sur "OK"  
 
![winsrv2022_radius_profil_06.jpg](/microsoft/windows_server_2022/radius/winsrv2022_radius_profil_06.jpg)
 
Mon groupe à bien été ajouté.
 
![winsrv2022_radius_profil_07.jpg](/microsoft/windows_server_2022/radius/winsrv2022_radius_profil_07.jpg)
 
Ajouter une seconde condition  en cliquant une nouvelle fois sur "Ajouter"
 
![winsrv2022_radius_profil_08.jpg](/microsoft/windows_server_2022/radius/winsrv2022_radius_profil_08.jpg)
 
Sélectionnez cette fois "Type de port NAS", il se situe en bas de la liste.
 
![winsrv2022_radius_profil_09.jpg](/microsoft/windows_server_2022/radius/winsrv2022_radius_profil_09.jpg)
 
Sélectionnez les options "Sans fil - IEEE 802.11" et "Sans fil - Autre". 
 
![winsrv2022_radius_profil_10.jpg](/microsoft/windows_server_2022/radius/winsrv2022_radius_profil_10.jpg)
 
La partie des conditions est configurer, cliquez sur "Suivant"
 
![winsrv2022_radius_profil_11.jpg](/microsoft/windows_server_2022/radius/winsrv2022_radius_profil_11.jpg)
 
Laissez la configuration sur "Accès accordé".
 
![winsrv2022_radius_profil_12.jpg](/microsoft/windows_server_2022/radius/winsrv2022_radius_profil_12.jpg)
 
Ajouter une méthode d'authentification.
 
![winsrv2022_radius_profil_13.jpg](/microsoft/windows_server_2022/radius/winsrv2022_radius_profil_13.jpg)
 
Sélectionnez "Microsoft PEAP" et cliquez sur "OK"
 
![winsrv2022_radius_profil_14.jpg](/microsoft/windows_server_2022/radius/winsrv2022_radius_profil_14.jpg)
 
Configurez des contraintes si besoin.
 
![winsrv2022_radius_profil_15.jpg](/microsoft/windows_server_2022/radius/winsrv2022_radius_profil_15.jpg)
 
De même pour les paramètres au besoin.
 
![winsrv2022_radius_profil_16.jpg](/microsoft/windows_server_2022/radius/winsrv2022_radius_profil_16.jpg)
 
Notre profil est maintenant terminé. Cliquez sur "Terminer"
 
![winsrv2022_radius_profil_17.jpg](/microsoft/windows_server_2022/radius/winsrv2022_radius_profil_17.jpg)
 
## Ajout de la borne Wi-Fi
 
Dans l'outil de gestion de RADIUS, dépliez "Client et serveurs RADIUS" et ajoutez un nouveau "Clients RADIUS"
 
![winsrv2022_radius_client_01.jpg](/microsoft/windows_server_2022/radius/winsrv2022_radius_client_01.jpg)
 
Ici plusieurs paramètres à configurer :
- Nom convivial : Nom d'hôte de la borne Wi-Fi.
- Adresse IP : Renseignez l'adresse IP ou le nom DNS de la borne.
- Pour le secret partagé, cochez "Manuel" et renseignez la clé qui devra être également saisie sur la borne Wi-Fi.
- Laissez coché "Activer ce client RADIUS".
 
![winsrv2022_radius_client_02.jpg](/microsoft/windows_server_2022/radius/winsrv2022_radius_client_02.jpg)
 
Le client est configuré côté serveur. Il vous reste à configurer la borne elle même, les marques et modèles étant nombreux, je n'irais pas plus loin dans ce tutoriel, je vous invite à vous référez à la documentation technique de votre matériel.
 
