---
title: Kubernetes
description: 
published: true
date: 2022-02-14T11:31:27.185Z
tags: 
editor: markdown
dateCreated: 2022-02-14T10:33:28.625Z
---

# Présentation
Kubernetes est un orchestrateur de conteneur docker.

# Notions
- noeuds (serveurs) : physiques ou virtuels
  - master ou simple noeud d'exécution 
  
- pods : pierre centrale de K8S
	- ensemble cohérent de conteneurs
  - un ou plusieurs conteneurs
  - une instace de K8S
  
- service : abstraction des pods
	- permet d'éviter la communication par ip
  - service > ip/port > pods
  - service = ip et port fixe
  
- volumes : persistens ou non
	- leiux d"achanges entre pods
  - intérieur de pods = non persistent
  - extérieur = persistant
  
- deployments: objets de gestion des déploiments
	- création/supprission
  - scaling: gestion de paramètres pour la montée en charge (ou réduction)
  
- namespaces: cluster virtuel (ensemble de services)
	- sous ensemble pour cloisonner dans K8S
  
# Installation
Désactiver le swap :
```bash
swapoff -a
```

Mis en place des dépots : 
```bash
apt-get update && apt-get install -y apt-transport-https curl sudo gnupg software-properties-common
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -
sudo add-apt-repository "deb http://apt.kubernetes.io/ kubernetes-xenial main"
```

Installation :
```bash
sudo apt-get install -y kubelet kubeadm kubectl kubernetes-cni
systemctl enable kubelet
```
- kubeadm : installation du cluster
- kubelet : service qui tourne sur les machines (lancement pods...)
- kubectl : permet la communication avec le cluster