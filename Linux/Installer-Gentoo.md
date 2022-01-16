---
title: Installer Gentoo
description: 
published: false
date: 2022-01-16T13:16:14.942Z
tags: 
editor: markdown
dateCreated: 2022-01-16T13:16:14.942Z
---

# Introduction

# Prérequis
- Connaissance solides des systèmes linux (pour comprendre)
- Récupérer le media d'installation CD : https://www.gentoo.org/downloads

# Installation
Faite booter le media d'installation sur votre machine

attender que `livecd ~ #` apparaisse

mettez votre clavier en français :

```bash
loadkeys fr
```

vérifier que vous posséder bien une ip :

```bash
ip a
```

tester la communication avec internet :

```bash
ping -c2 google.fr
```

mettez un mot de passe à root :

```bash
passwd
```

démarrer sshd :
```bash
/etc/init.d/sshd start
```

connecter vous en ssh sur votre machine :
```bash
ssh root@192.168.10.140
```

### Partitionnement
```bash
cfdisk
```

j'écrit 1 partion de 4Go en changer le type "swap" pour le swap. Je créer une deruxième partition pour le reste.

Je fait un fdisk -l pour vérifier que mes partitions sont créer.
```bash
ping -c2 linuxtricks.fr
```

Je formate mes partitions :
```bash
mkswap /dev/sda1
mkfs.ext4 /dev/sda2
```

Je monte ma partition racine et j'active le swap
```bash
mount /dev/sda2 /mnt/gentoo
swapon /dev/sda1
```

vérifier la date :
```bash
date
```

Pour modifier la date :
```bash
date MMJJhhmmAAAA
```

On télécharge le stage 3 de gentoo 
```bash
cd /mnt/gentoo
wget https://bouncer.gentoo.org/fetch/root/all/releases/amd64/autobuilds/20220109T170538Z/stage3-amd64-openrc-20220109T170538Z.tar.xz
tar xJvpf stage3*
```

configurer le fichier make.conf 
```bash
nano -w /mnt/gentoo/etc/portage/make.conf
```

vérfier les variables :
```bash
COMMON_FLAGS="-march=native -O2 -pipe"
CFLAGS="${COMMON_FLAGS}"
CXXFLAGS="${COMMON_FLAGS}"
```

à la fin du fichier ajoutez :
```bash
USE=""
MAKEOPTS="-j12" # 12 car 12CPU
LINGUAS="fr" #Langue (anciennement)
L10N="fr" #Langue
VIDEO_CARDS="fbdev vesa intel i915 nvidia nouveau radeon amdgpu radeonsi virtualbox vmware" #Cartes graphiques, choisir les cartes adéquats. Garder fbdev (framebuffer) et vesa (générique)
INPUT_DEVICES="libinput synaptics keyboard mouse evdev jokstick wacom" # Périphériques d'entrées utilisés (clavier souris + si affinités)
EMERGE_DEFAULT_OPTS="${EMERGE_DEFAULT_OPTS} --quiet-build=y" # Pour ne pas avoir la compilation verbeuse
```

on selectionne dans mirrors
```bash
mirrorselect -i -o >> /mnt/gentoo/etc/portage/make.conf
```

```bash
mkdir -p /mnt/gentoo/etc/portage/repos.conf
cp /mnt/gentoo/usr/share/portage/config/repos.conf /mnt/gentoo/etc/portage/repos.conf/gentoo.conf
```

copier les informations dns
```bash
cp -L /etc/resolv.conf /mnt/gentoo/etc/
```

on monte les dossiers :
```bash
mount -t proc /proc /mnt/gentoo/proc
mount --rbind /dev /mnt/gentoo/dev
mount --rbind /sys /mnt/gentoo/sys
```

on entre dans le chroot (on change de racine) :
```bash
chroot /mnt/gentoo /bin/bash
```

met à jour les variables d'env et en change notre prompt
```bash
env-update && source /etc/profile
export PS1="[chroot] $PS1"
source /etc/profile
```

télécharge les paquet de gentoo
```bash
emerge-webrsync
```

on séléctionne notre profile
```bash
eselect profile list
eselect profile set 5
```

on modifie le locale
```bash
nano -w /etc/locale.gen
```

on ajoute :
```bash
fr_FR.UTF-8 UTF-8
```

on regénére les locales :
```bash
locale-gen
```

on séléctionne notre locale :
```bash
eselect locale list
eselect locale set 4
```

on le fait aussi pour le TTY (mettre en fr):
```bash
nano -w /etc/conf.d/keymaps
```

one recharge à nouveau les variable sd'environnement :
```bash
env-update && source /etc/profile && export PS1="[chroot] $PS1"
```

on change la timezone :
```bash
echo "Europe/Paris" > /etc/timezone
emerge --config sys-libs/timezone-data
```

on modifie fstab :
```bash
nano -w /etc/fstab
```

on ajoute :
```bash
/dev/sda1               none            swap            defaults,noatime         0 0
/dev/sda2               /               ext4            defaults,noatime         0 1
```

on installer :
```bash
emerge -a linux-firmware
emerge -a gentoo-sources
emerge -a pciutils usbutils
```

on sélectionne notre noyau
```bash
eselect kernel list
eselect kernel set 1
```


on compile le noyau :
```bash
cd /usr/src/linux
make mrproper
make menuconfig
```

compiler le noyau :
```bash
make -j5
```

installer les modules :
```bash
make modules_install
```

installer le noyau :
```bash
make install
```

configurer le nom d'hôte :
```bash
nano -w /etc/conf.d/hostname
```

ajoutez :
```bash
hostname="gentoo"
```

ajoutez le aussi dans :
```bash
nano -w /etc/hosts
```

in installer :
```bash
emerge -a --noreplace net-misc/netifrc
```

installer client dhcp :
```bash
emerge -a dhcpcd
```

reperer le nom de votre interface réseau :
```bash
ip a
```

créer le fihicer de conf pour le réseua :
```bash
nano -w /etc/conf.d/net
```

créer un lien symboliques :
```bash
ln -sv net.lo net.enp2s1
rc-update add net.enp2s1 default
```


ajouter :
```bash
config_enp2s1="dhcp"
```

définir un mdp à root :
```bash
passwd
```

activer le service sshd au boot :
```bash
 rc-update add sshd default
```

on créer un user :
```bash
useradd -m -G users,audio,cdrom,portage,video,wheel -s /bin/bash zatoufly
passwd zatoufly
```

## installer grub
installer grub :
```bash
emerge -a grub
grub-install /dev/sda
grub-mkconfig -o /boot/grub/grub.cfg
```

```bash
cd /
rm stage3*
exit
cd /
umount -R /mnt/gentoo
reboot
```


à test :
emerge --ask --verbose sys-boot/grub:2
grub-install /dev/sda

echo 'GRUB_PLATFORMS="efi-64"' >> /etc/portage/make.conf
emerge --ask sys-boot/grub:2
emerge --ask --update --newuse --verbose sys-boot/grub:2

