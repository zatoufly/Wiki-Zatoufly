---
title: Installation Docker sur OMV
description: Installation Docker sur OMV
published: true
date: 2022-01-16T20:58:37.997Z
tags: docker, portainer, openmediavault, omv-extras
editor: markdown
dateCreated: 2022-01-15T09:41:27.367Z
---



# Installation du plugin OMV-Extras




Avant de pouvoir installer docker proprement sur Openmediavault, nous devons lui ajouter une extension




Pour commencer, télécharger l'extension correspondant a votre version de openmediavault:


OMV4 : [https://github.com/OpenMediaVa…extrasorg_latest_all4.deb](https://github.com/OpenMediaVault-Plugin-Developers/packages/raw/master/openmediavault-omvextrasorg_latest_all4.deb)


OMV5 : [https://github.com/OpenMediaVa…extrasorg_latest_all5.deb](https://github.com/OpenMediaVault-Plugin-Developers/packages/raw/master/openmediavault-omvextrasorg_latest_all5.deb)




Une fois l'extension télécharger , rendez vous sur l'interface web de votre openmediavault, puis rendez-vous dans les plugins




![omv1.png](/nas/omv/docker/omv1.png)




Puis cliquer sur "Télécharger"




![omv2.png](/nas/omv/docker/omv2.png)




Une fois cela fait, une fenêtre apparaît vous demandant l'emplacement du fichier, indiquer lui l'emplacement du fichier d'extension précedement télécharger, puis cliquer sur "ok"




![omv3.png](/nas/omv/docker/omv3.png)




Ce qui lancera l'upload de l'installateur de ce plugin sur votre OMV




![omv4.png](/nas/omv/docker/omv4.png)




Une fois celui-ci terminé, chercher tout en bas de la liste des plugins, et cocher "openmediavault-omvextrasorg..." et cliquer sur "installer" en haut de la page




![omv5.png](/nas/omv/docker/omv5.png)




Confirmé puis patienté, l'installation peu prendre plusieurs minutes




![omv6.png](/nas/omv/docker/omv6.png)


![omv7.png](/nas/omv/docker/omv7.png)


![omv8.png](/nas/omv/docker/omv8.png)




Après la fin de l'installation, vous pouvez fermer le popup , et vous devriez remarquer l'ajout de "OMV-extras" sous "plugins" , dans le menu latéral.


Cliquez dessus.




![omv9.png](/nas/omv/docker/omv9.png)




Ce qui vous mènera sur cette page:




![omv9.png](/nas/omv/docker/omv10.png)




Cliquez sur l'onglet "Docker" , puis sur le bouton "Docker" , et pour finir, "Installer"




![omv9.png](/nas/omv/docker/omv11.png)




Une fois l'installation terminée , vous pouvez fermer le Popup, docker est maintenant fonctionnel sur votre serveur




![omv9.png](/nas/omv/docker/omv12.png)




## Optionnel : installer Portainer




Exactement dans le même onglet que pour docker, vous pouvez également installer portainer (qui permet d'avoir une interface graphique pour la gestion de vos conteneurs)



Il vous suffit de cliquer sur le bouton "Portainer" , puis "Installer"




![omv9.png](/nas/omv/docker/omv13.png)




Une fois l'installation finie, vous aurez accès à portainer via l'adresse ip de votre Openmediavault, mais sur le port 9000


Par exemple : 192.168.1.51:9000