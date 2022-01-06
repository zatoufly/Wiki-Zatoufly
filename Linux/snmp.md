---
title: snmp
description: 
published: 1
date: 2022-01-06T10:06:56.423Z
tags: 
editor: markdown
dateCreated: 2022-01-06T10:06:56.423Z
---

# Installation
 
### Mettez à jour votre système
```bash
apt update && apt full-upgrade -y
```
 
### Installer snmp
```bash
apt install snmpd -y
```
 
### renseignez l'ip de votre serveur de supervision
```bash
vim /etc/snmp/snmpd.conf
```
Sur la ligne "agentAddress"
 
### relancez le service snmp
```bash
systemctl reload snmp
systemctl enable snmp
```
