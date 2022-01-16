---
title: Installation Docker sur OMV
description: Installation Docker sur OMV
published: true
date: 2022-01-16T20:36:01.591Z
tags: docker, openmediavault, portainer
editor: markdown
dateCreated: 2022-01-15T09:41:27.367Z
---

# Installation de OMV-Extras

Avant de pouvoir installer docker proprement sur Openmediavault, nous devons lui ajouter une extention 

Pour commencer,  télécharger l'extention correspondant a votre version de openmediavault:
OMV4 : [https://github.com/OpenMediaVa…extrasorg_latest_all4.deb](https://github.com/OpenMediaVault-Plugin-Developers/packages/raw/master/openmediavault-omvextrasorg_latest_all4.deb)
OMV5 : [https://github.com/OpenMediaVa…extrasorg_latest_all5.deb](https://github.com/OpenMediaVault-Plugin-Developers/packages/raw/master/openmediavault-omvextrasorg_latest_all5.deb)

Une fois l'extention telecharger , rendez vous sur l'interface web de votre openmediavault, puis rendez-vous dans les plugins

![omv1.png](/nas/nas/omv/docker/omv1.png)

Puis cliquer sur "Télécharger" 

![omv2.png](/nas/nas/omv/docker/omv2.png)

Une fois cela fait, une fenetre apparait vous demandant l'emplacement du fichier, indiquer lui l'emplacement du fichier d'extention precedement telecharger, puis cliquer sur "ok"

![omv3.png](/nas/nas/omv/docker/omv3.png)

Ce qui lancera l'upload de l'installateur de ce plugin sur votre OMV

![omv4.png](/nas/nas/omv/docker/omv4.png)

Une fois celui ci terminé, chercher tout en bas de la liste des plugins, et cocher "openmediavault-omvextrasorg..." et cliquer sur "installer" en haut de la page

![omv5.png](/nas/nas/omv/docker/omv5.png)

Confirmé puis patienté , l'installation peu prendre plusieurs minute

![omv6.png](/nas/nas/omv/docker/omv6.png)
![omv7.png](/nas/nas/omv/docker/omv7.png)
![omv8.png](/nas/nas/omv/docker/omv8.png)

Apres la fin de l'installation , vous pouvez fermer le popup , et vous devriez remarquer l'ajout de "OMV-extras" sous "plugins" , dans le menu latéral.
Cliquez dessus.

![omv9.png](/nas/nas/omv/docker/omv9.png)