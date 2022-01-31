---
title: Commandes de bases
description: 
published: true
date: 2022-01-31T10:42:49.926Z
tags: 
editor: markdown
dateCreated: 2022-01-18T11:58:32.113Z
---

# 1. La Navigation
|     |     |
| --- | --- |
| `ls` | liste le contenue du répertoire courant |
| `-a` | voir les fichiers cachés |
| `-h` | affiche la taille du fichier lisible par un humain |
| `-l` | voir plus de propriétés du fichiers (propriétaires, droit appliqués) |
 
 
|     |     |
| --- | --- |
| `cd /dossier` | Se déplacer dans un répertoire |
| `cd ./dossier` | naviguer à partir du répertoire courant |
| `cd ..` | Se déplacer dans le répertoire parent |
| `cd /` | Se déplacer à la racine de la partition système |
 
# 2. Fichiers et Dossiers
## 2.1 Écrire et afficher des fichiers
 
### touch

|     |     |
| --- | --- |
| `touch fichier` | créer un fichier |
 
### cat
 
|     |     |
| --- | --- |
| `cat fichier.txt` | affiche le contenue du fichier |
| `cat > fichier.txt` | écrire dans le fichier |
| `cat >> fichier.txt` | écrire à la suite dans le fichier |
 
 
### head
|     |     |
| --- | --- |
| `head fichier.txt` | affiche les 10 première ligne du fichier |
| `head -n 4 fichier.txt` | affiche les 4 première ligne |
| `head -n -16 fichier.txt` | affiche toutes les lignes en excluant les 16 dernières |
 
 
### tail
|     |     |
| --- | --- |
| `tail fichier.txt` | affiche les 10 dernières lignes du fichier |
| `tail -n 4 fichier.txt` | affiche les 4 dernières lignes |
| `tail -n +18 fichier.txt` | affiche toutes les lignes à partir de la 18 |
| `tail -f fichier.txt` | affiche les 10 dernière lignes + celle ajouter de manière dynamique |
 
## 2.2 Archivage
### tar
|     |     |
| --- | --- |
| `tar -cvf archive1.tar dossier1 dossier2` | Créer une archive nommé archive1.tar |
| `-c` | Créer une archive |
| `-f` | Permet de nommer l'archive |
| `-v` | Affiche une indication écrite de l'archivage en tant réel |
| `-z` | compresse l'archive avec gzip (.tar.gz / .tgz) |
| `-j` | compresse l'archive avec bz2 (.bz2) |
| `-J` | compresse l'archive avec xz (.xz) |
| --------------- |  |
| `tar -tf archive1.tar` | Voir les fichiers dans l'archive |
| `-f` | voir les fichiers dans l'archive |
| `-v` | équivalent au ls -l |
| --------------- |  |
| `tar -xzvf archive.tgz` | Décompresse l'archine dans le répertoire courant |
| `-z` | décompresse avec gzip |
 
# 3. La Recherche
### find
|     |     |
| --- | --- |
| `find -name "fichier.txt"` | recherche un fichier dans le répertoire courant |
| `find /usr/share -name "fichier.txt"` | recherche dans le répertoire indiqué |
| `find -name "fichier.*"` | recherche avec le caractère "joker" |
 
 
### grep
|     |     |
| --- | --- |
| `grep [mot à recherche] [fichier où il faut rechercher]` | recherche un contenue dans un fichier |
| `-i` | ignore la casse |
| `-r /home/test` | recherche de manière récursive |
 
 
### autres
|     |     |
| --- | --- |
| `which [commande]` | recherche où est situé une commande |
| `whereis` | which mais avec le manuel/source |
 
 
# 4. Le Réseau
|     |     |
| --- | --- |
| `ip a` | affiche la liste des interface réseau |
| `ip route` | affiche les routes disponibles |
| `ping [ip ou dns]` | savoir si une machine est joignable  |
| `-c 5` | envoie 5 requêtes ICMP |
| `dig [dns]` | donne la liste des enregistrement |
| `wget [lien]` | télécharge un fichier sur le web |
| `-r` | télécharge de manière récursive |
| `curl` | affiche le contenue du lien/site |
| `-o [nouveau nom]` | change le nom du fichier récupérer |
| `ssh [user]@[ip ou dns]` | se connecter en ssh |
| `-p` | spécifier le port |
 
# 5. Processus
|     |     |
| --- | --- |
| `ps` | affiche les processus en cours |
| `ps aux` | affiche tous les processus |
| `ps aux | grep galculator` | affiche les processus contenant galculator |
| `pidof galculator` | affiche le PID de galculator |
| `kill [PID]` | tue le processus |
| `kill [PID] [PID]` | tue plusieurs processus |
| `killall [galculator]` | tue tous les processus dont le nom contient galculator |
 
# 6. Informations systèmes
```bash
date # affiche la date
cal # afficher le calendrier du mois
uptime # affiche depuis combien de temps la machine est démarrée
w # affiche les utilisateur connecté à la machine
env # voir les variables d'environnement
 
df # affiche tout les systèmes de fichier monter
-h # affiche les taille visible par humain
 
du -sh [dossier] # affiche la taille du dossier
 
hostname # affiche le hostname
hostname -I # affiche l'adresse IP de l'hôte
 
uname -a # affiche affiche les informations systèmes de linux
uname -r # affiche la version du noyau
 
cat /etc/debian_version # affiche la version de Debian
 
MATÉRIEL
lspci -tv # affiche les périphériques PCI
lsusb -tv # affiche les périphériques USB
more /proc/cpuinfo # affiche les infos du processeur
more /proc/meminfo # affiche les informations relative à la mémoire
 
last reboot # afficher l'historique des redémarrages
reboot # redémarre la machine
shutdown -now # éteint sans délai
```
 
# 7. Utilisateurs et Groupes
> Les utilisateurs sont stockés dans /etc/passwd
{.is-info}
 
|     |     |
| --- | --- |
| `useradd utilisateur` | créer un utilisateur |
| `-d` | créer un répertoire home à l'utilisateur |
| --------------- |  |
| `userdel utilisateur` | supprimer un utilisaleur |
| `usermod [option] [user]` | modifier un utilisateur |
| `usermod -aG sudo utilisateur` | ajoute un utilisateur un groupe sudo |
| `passwd utilisateur` | créer/modifier le mdp d'un utilisateur |
 
# 8. Permissions
On peut voir les permissions avec la commande <kbd>ls -l</kbd>
 
example : 
```bash
drwxr-xr-x 2 admin   administrators 4096 2022-01-12 18:52 fichier.txt
```
le premier caractère indique le type du fichier
d -> répertoire
l -> lien symbolique
 
Les permissions rwx (read,write,execute)
tiret -> pas attribué
 
il y a 3 groupes de 3 lettres (rwx)
ils signifie respectivement les permissions attribuées aux propriétaire / groupe propriétaire / autres
 
### chown
|     |     |
| --- | --- |
| `chown utilisateur.groupe /mondossier` | change le propriétaire du répertoire |
| `-R` | de manière récursive |
 
 
### chmod
|     |     |
| --- | --- |
| `chmod 777 /mondossier` | change les droits du répertoire |
| `-R` | de manière récursive |
 
1 ->
2 ->
3 ->
4 ->
5 -> r-x
6 -> rw-
7 -> rwx

# 9. APT
apt ou advanced packaging Tool est un gestionnaire de paquets utilisé sous Debian.

|   commandes | |
| --- | --- |
| `apt update` | met à jour la liste des paquets disponibles |
| `apt upgrade` | met à jour les paquet du systèmes |
| `apt full-upgrade` | apt upgrade + supprimer les dépenses inutilisés / obsolètes |
| `apt search [paquet]` | cherche les paquets |
| `apt show [paquet]` | affiche les informations sur un paquet |
| `dpkg -l` | liste tout les paquets installé sur le système |
 
 
|  Installation de paquet   |     |
| --- | --- |
| `apt install [paquet]` | installer un paquet |
| `dpkg -i [ficher .deb]` | installe un paquet en .deb |
| `apt install -f` | installe les dépenses en cas d'erreur du fichier .deb |
 
 
|  Désinstallation de paquet   |     |
| --- | --- |
| `apt remove [paquet]` | désinstalle le paquet |
| `apt autoremove [paquet]` | désinstalle le paquet et ses dépendances |
| `--purge` | supprime les fichier de configuration |
