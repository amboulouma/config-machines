---
Configuration des machines 

H4404
---

- [Configuration réseaux Machine 1](#configuration-r%C3%A9seaux-machine-1)
    - [1. Script pour lancer les machines](#1-script-pour-lancer-les-machines)
    - [2. Configuration des VLAN à partir de l'hôte](#2-configuration-des-vlan-%C3%A0-partir-de-lh%C3%B4te)
    - [3. Configuration des adresses IPs:](#3-configuration-des-adresses-ips)
- [Configuration réseaux Machine 2](#configuration-r%C3%A9seaux-machine-2)
    - [1. Script pour lancer les machines](#1-script-pour-lancer-les-machines-1)
    - [2. Configuration des VLAN à partir de l'hôte](#2-configuration-des-vlan-%C3%A0-partir-de-lh%C3%B4te-1)
    - [3. Configuration des adresses IPs:](#3-configuration-des-adresses-ips-1)
        - [1. Commandes à lancer dans la machine hôte](#1-commandes-%C3%A0-lancer-dans-la-machine-h%C3%B4te)
        - [2. Commandes sur chaque machine](#2-commandes-sur-chaque-machine)
            - [DAB-Site-2-1](#dab-site-2-1)
            - [DAB-Site-2-2](#dab-site-2-2)
            - [PC-Site-1-1](#pc-site-1-1)
            - [PC-Site-1-2](#pc-site-1-2)

# Configuration réseaux Machine 1

__*Remarques générales*__
> * Configurer les VLANs avant de configurer les machines
> * On configure les machines Linux depuis la machine hôte
> * On ne branche la machine sur le switch que quand tout est configuré.

## 1. Script pour lancer les machines
```bash
/VMS/DAB-Site1-1/launch.sh
/VMS/DAB-Site1-2/launch.sh
/VMS/PC-Site-2-1/launch.sh
/VMS/PC-Site-2-2/launch.sh
/VMS/PLD-MARS-Debian.web-1/launch.sh
/VMS/Vyos-Agence-Principale1/launch.sh
```

## 2. Configuration des VLAN à partir de l'hôte

Configurer les VLAN des machine virtuelles sur la machine physique 1.

```bash

```
__Output__
>```bash
>
>```
__*Remarques*__

> * 
> * 

## 3. Configuration des adresses IPs:

Configuration des adresses IPs des machines virtuelles sur la machine physique 1.

```bash

```
__Output__
>```bash
>
>```
__*Remarques*__

> * 
> * 

# Configuration réseaux Machine 2

## 1. Script pour lancer les machines

Script pour lancer les machines.

```bash
/VMS/DAB-Site2-1/launch.sh
/VMS/DAB-Site2-2/launch.sh
/VMS/PC-Site-1-1/launch.sh
/VMS/PC-Site-1-2/launch.sh
/VMS/Vyos-Agence-Principale2/launch.sh
```

## 2. Configuration des VLAN à partir de l'hôte

Configurer les VLAN des machine virtuelles sur la machine physique 2.

```bash
sudo vconfig add p255p1 5
sudo vconfig add p255p1 3
sudo vconfig add p255p1 6
sudo vconfig add p255p1 7

sudo ifconfig p255p1 up
sudo ifconfig p255p1.5 up
sudo ifconfig p255p1.3 up
sudo ifconfig p255p1.6 up
sudo ifconfig p255p1.7 up
```
__Output__
>```bash
>Added VLAN with VID == 5 to IF -:p255p1:-
>Added VLAN with VID == 3 to IF -:p255p1:-
>Added VLAN with VID == 6 to IF -:p255p1:-
>Added VLAN with VID == 7 to IF -:p255p1:-
>```
__*Remarques*__

> * p255p1 est eth1 de la machine hôte
> * Activer la carte réseau en premier avant d'activer les VLANs.
> * VM pour chaque VM configurer dans réseaux :
>   * Mode d'accès par pont
>   * Nom: Nom du VLAN

## 3. Configuration des adresses IPs:

Configuration des adresses IPs des machines virtuelles sur la machine physique 2.

### 1. Commandes à lancer dans la machine hôte

On configure les IPs des machines virtuelles sur la machine hôte.

```bash
sudo ifconfig p255p1.5 10.2.1.2 netmask 255.255.255.0
sudo ifconfig p255p1.5 10.2.1.3 netmask 255.255.255.0
sudo ifconfig p255p1.5 10.2.2.2 netmask 255.255.255.0
sudo ifconfig p255p1.5 10.2.2.3 netmask 255.255.255.0
```
### 2. Commandes sur chaque machine

#### DAB-Site-2-1

```bash
ifconfig eth0 10.2.1.2
sudo route add default gw 10.2.1.1
```

#### DAB-Site-2-2

```bash
ifconfig eth0 10.2.1.3
sudo route add default gw 10.2.1.1
```

#### PC-Site-1-1

```bash
ifconfig eth0 10.2.2.2
sudo route add default gw 10.2.2.1
```

#### PC-Site-1-2

```bash
ifconfig eth0 10.2.2.3
sudo route add default gw 10.2.2.1
```

__*Remarques*__

> * Configurer les machines sur chaque sous réseau.
