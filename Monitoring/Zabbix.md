---
title: Zabbix
description: 
published: 1
date: 2021-12-10T17:41:09.140Z
tags: 
editor: markdown
dateCreated: 2021-12-10T11:32:30.444Z
---

![zabbix-banner.jpg](/monitoring/zabbix-banner.jpg){.align-center}

# Présentation
**Zabbix** est une solution de supervision open source
 
# Installation
Pour ce tutoriel j'utilise une j'installe zabbix 5.4 sur une Debian 11, j'utilise un serveur web apache2 ainsi que mariadb pour le serveur de base de données.
> Ce tutoriel présente des failles de sécurité, merci de l'utiliser uniquement pour effectuer des tests ou pour un réseau local.
{.is-danger}

> __Prérequis__
:arrow_right:Adresse ip statique
{.is-info}

---

Pour commencer on met à jour notre système d'exploitation puis on installe quelques dépendances : apache2, mariadb, php etc..

```bash
apt update && apt upgrade
apt install apache2 php php-mysql php-mysqlnd php-ldap php-bcmath php-mbstring php-gd php-pdo php-xml libapache2-mod-php mariadb-server mariadb-client
```

Ensuite je télécharge le dépôt officiel de zabbix.

```bash
cd /tmp
wget https://repo.zabbix.com/zabbix/5.4/debian/pool/main/z/zabbix-release/zabbix-release_5.4-1+debian11_all.deb
```

Une fois téléchargé on installe les dépôts zabbix et on met à jour la liste des dépôts.

```bash
dpkg -i zabbix-release_5.4-1+debian11_all.deb
apt update
```

> Si vous avez une erreur à cette étape, exécuter ces 3 commandes, puis recommencer l'étape précédente.
{.is-warning}

```bash
export PATH=$PATH:/usr/local/sbin
export PATH=$PATH:/usr/sbin
export PATH=$PATH:/sbin
```

Nous pouvons installer maintenant notre serveur zabbix :

```bash
apt install zabbix-server-mysql zabbix-frontend-php zabbix-apache-conf zabbix-sql-scripts zabbix-agent
```

On va maintenant créer une base de données ainsi que son utilisateur : 

```bash
mysql -uroot
```

```SQL
create database zabbix character set utf8 collate utf8_bin;
create user zabbix@localhost identified by 'mon-mdp';
grant all privileges on zabbix.* to zabbix@localhost;
exit
```

Nous pouvons importer le schéma et les données initiales de la base de données. Il faudra entrer le  mot de passe récemment créé.

```bash
zcat /usr/share/doc/zabbix-sql-scripts/mysql/create.sql.gz | mysql -uzabbix -p zabbix
```

Pour renseignez le mot de passe aux serveur zabbix, nous allons éditez la ligne `# DBPassword=` dans le fichier `/etc/zabbix/zabbix_server.conf`

Voici un exemple : 

```bash
DBUser=zabbix

### Option: DBPassword
#       Database password.
#       Comment this line if no password is used.
#
# Mandatory: no
# Default:
DBPassword=mon-mdp
```

Il nous reste qu'à redémarrer quelques services et les activer au démarrage de la machine.

```bash
systemctl restart zabbix-server zabbix-agent apache2
systemctl enable zabbix-server zabbix-agent apache2
```

Sur votre navigateur tapez `http://server_ip/zabbix` pour finaliser l'installation de zabbix.

Sélectionnez la langue souhaitez :

![zabbix-installation-1.jpg](/monitoring/zabbix-installation-1.jpg)

Zabbix vérifie si tous les prérequis sont présent : 

![zabbix-installation-2.jpg](/monitoring/zabbix-installation-2.jpg)

Configurer votre base de données avec le mot de passe créés antérieurement :

![zabbix-installation-3.jpg](/monitoring/zabbix-installation-3.jpg)

Insérez le nom que vous souhaitez donner à votre serveur : 

![zabbix-installation-4.jpg](/monitoring/zabbix-installation-4.jpg)

Indiquer l'UTC où est situé le serveur, vous pouvez aussi modifier le thème de l'interface web :

![zabbix-installation-5.jpg](/monitoring/zabbix-installation-5.jpg)

Il nous reste plus qu'à valider l'installation : 

![zabbix-installation-6.jpg](/monitoring/zabbix-installation-6.jpg)
![zabbix-installation-7.jpg](/monitoring/zabbix-installation-7.jpg)

Maintenant nous pouvons nous connecter à zabbix avec le nom d'utilisateur `Admin` et le mdp `zabbix`

> Félicitation, Zabbix est maintenant installé sur votre serveur ! 
{.is-success}

# Installation Agent

Tous les agent sont disponible en téléchargement ici : https://www.zabbix.com/download_agents
# Tabs {.tabset}
## Windows

Je télécharge l'exécutable de l'agent pour Windows, et je l'installe sur mon serveur Windows

Ici je laisse tout par défaut, j'indique juste l'ip de mon serveur Zabbix

![zabbix-agent-windows-1.jpg](/monitoring/zabbix-agent-windows-1.jpg)

Et je continue, en laisser tous les paramètres par défaut

Une fois que mon agent est installé, je peux configurer mon serveur sur l'interface web de mon serveur zabbix.

## Debian 

Connecter vous sur la machine client

On va ajoutez les dépôts de zabbix : 

```bash
wget https://repo.zabbix.com/zabbix/5.4/debian/pool/main/z/zabbix-release/zabbix-release_5.4-1+debian11_all.deb
dpkg -i zabbix-release_5.4-1+debian11_all.deb
apt update
```

Puis on installe l'agent :

```bash
apt install zabbix-agent
```

Une fois fait, éditez le fichier `/etc/zabbix/zabbix_agentd.conf`

à la ligne 121, indiquez l'ip de votre serveur zabbix, pour moi : `Server=192.168.10.20`

# Ajoutez un client
# Tabs {.tabset}
## Via agent
Pour ajoutez un client je vais dans l'onglet configuration puis groupes d'hôtes

Je créer un nouveau groupe d'hôtes, pour ma part nommé Windows.

![zabbix-ajoutez-agent-1.jpg](/monitoring/zabbix-ajoutez-agent-1.jpg)

Ensuite je vais dans Configuration -> Hôtes et je créer un hôte.

J'indique le nom d'hôte et je sélectionne le groupe Windows. J'ajoute une interface "Agent" et j'indique son IP, on peut également le faire via enregistrement DNS.

![zabbix-ajoutez-agent-2.jpg](/monitoring/zabbix-ajoutez-agent-2.jpg)

Maintenant que le client est ajouté, je peux lui appliquer une template.

Allez dans l'onglet "Modèles" puis sélectionnez la template "Windows by Zabbix agent".

![zabbix-ajoutez-agent-3.jpg](/monitoring/zabbix-ajoutez-agent-3.jpg)

Maintenant si je vais dans l'onglet Surveillance puis Dernières  données et que je sélectionne mon hôte SRV-R310 on peut voir les données récolté par l'agent.

![zabbix-ajoutez-agent-4.jpg](/monitoring/zabbix-ajoutez-agent-4.jpg)

> Félicitations, vous avez configuré votre client !
{.is-success}

## Via snmp

Bientôt disponible ...
