---
title: Zabbix
description: 
published: 1
date: 2021-12-10T12:15:17.533Z
tags: 
editor: markdown
dateCreated: 2021-12-10T11:32:30.444Z
---

# Présentation

# Installation
Pour ce tutoriel j'utilise une j'installe zabbix 5.4 sur une Debian 11, j'utilise un serveur web apache2 ainsi que mariadb pour le serveur de base de données.
> Ce tutoriel présente des failles de sécuriter, merci de l'utiliser uniquement pour effectuer des tests ou pour un réseau local.
{.is-danger}


---

Bien, pour commencer on met à jour notre système d'exploitation puis on installe quelques dépendances : apache2, mariadb, php etc..

```bash
apt update && apt upgrade
apt install apache2 php php-mysql php-mysqlnd php-ldap php-bcmath php-mbstring php-gd php-pdo php-xml libapache2-mod-php mariadb-server mariadb-client
```

Ensuite je télécharger le dépo officiel de zabbix.

```bash
cd /tmp
wget https://repo.zabbix.com/zabbix/5.4/debian/pool/main/z/zabbix-release/zabbix-release_5.4-1+debian11_all.deb
```

Une fois télécharger on installe les dépots zabbix et on met à jour la liste des dépots.

```bash
dpkg -i zabbix-release_5.4-1+debian11_all.deb
apt update
```

> Si vous avez une erreur à cette étape, éxécuter ces 3 commandes, puis recommancer l'étape précédente.
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

On va maintenant créer une base de données ainsi que sont utilisateur : 

```bash
mysql -uroot
```

```SQL
create database zabbix character set utf8 collate utf8_bin;
create user zabbix@localhost identified by 'mon-mdp';
grant all privileges on zabbix.* to zabbix@localhost;
exit
```

Nous pouvons importez le schéma et les données initial de la base de données. Il faudra entrer le  mot de passe récemment créé.

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

Il nous reste qu'à redémarrer quelques services et les activer au démarrage de la machine

```bash
systemctl restart zabbix-server zabbix-agent apache2
systemctl enable zabbix-server zabbix-agent apache2
```

