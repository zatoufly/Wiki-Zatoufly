---
title: QNAP - iSCSI
description: 
published: 1
date: 2021-12-21T19:18:19.265Z
tags: 
editor: markdown
dateCreated: 2021-12-21T19:18:19.265Z
---

# Connecter une cible iSCSI
Connectez vous sur l'interface web de votre NAS, puis ouvrez l'application "Stockage et Snapshot".
 
Allez dans l'onglet "Disque Distant" puis cliquez sur "Ajouter un disque virtuel"
 
![qnap-connecter-iscsi-1.png](/nas/qnap/qnap-connecter-iscsi-1.png)
 
Mettez y l'ip du serveur qui possède la cible iSCSI (dans mon cas mon open media vault) ainsi que le port du protocole, 3260 par défaut.
 
Cliquez sur "Obtenir le disque distant", il devrait trouver le nom de la cible iSCSI par lui-même.
 
![qnap-connecter-iscsi-2.png](/nas/qnap/qnap-connecter-iscsi-2.png)
 
Nommez le disque virtuel et indiquez le système de fichier que vous souhaitez.
 
![qnap-connecter-iscsi-3.png](/nas/qnap/qnap-connecter-iscsi-3.png)
 
Cliquez sur Terminer, votre disque virtuel à été créé.
 
![qnap-connecter-iscsi-4.png](/nas/qnap/qnap-connecter-iscsi-4.png)
 
Dans File Station, vous pourrez voir votre disque virtuel et y créer des dossiers partager dans les paramètres.
 
> Félicitation, vous avez connecté votre cible iSCSI
{.is-success}