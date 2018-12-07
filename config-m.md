---
Configuration des machines 

H4404
---

- [Configuration réseaux Machine 1](#configuration-r%C3%A9seaux-machine-1)
    - [1. Script pour lancer les machines](#1-script-pour-lancer-les-machines)
    - [2. Adresses IPs:](#2-adresses-ips)
        - [PC-Site2-1 (Win 7)](#pc-site2-1-win-7)
        - [PC-Site2-2 (Win 7)](#pc-site2-2-win-7)
            - [Configuration IP](#configuration-ip)
            - [Configuration pare feu](#configuration-pare-feu)
        - [DAB-Site1-1](#dab-site1-1)
        - [DAB-Site2-2](#dab-site2-2)
- [Configuration réseaux Machine 2](#configuration-r%C3%A9seaux-machine-2)
    - [1. Script pour lancer les machines](#1-script-pour-lancer-les-machines-1)
    - [2. Adresses IPs:](#2-adresses-ips-1)
        - [Configuration des VLAN à partir de l'hôte](#configuration-des-vlan-%C3%A0-partir-de-lh%C3%B4te)
        - [PC-Site2-1 (Win 7)](#pc-site2-1-win-7-1)
            - [Configuration IP](#configuration-ip-1)
            - [Configuration pare feu](#configuration-pare-feu-1)
        - [PC-Site2-2 (Win 7)](#pc-site2-2-win-7-1)
            - [Configuration IP](#configuration-ip-2)
            - [Configuration pare feu](#configuration-pare-feu-2)

# Configuration réseaux Machine 1

## 1. Script pour lancer les machines
```bash
/VMS/DAB-Site1-1/launch.sh
/VMS/DAB-Site1-2/launch.sh
/VMS/PC-Site-1-1/launch.sh
/VMS/PC-Site-1-2/launch.sh
/VMS/PLD-MARS-Debian.web-1/launch.sh
/VMS/Vyos-Agence-Principale1/launch.sh
```

## 2. Adresses IPs:

### PC-Site2-1 (Win 7)

* IP: ```10.2.2.2```
* Masque de sous-réseau: ```255.255.255.0```
* Pqsserelle par défaut: ```10.2.2.1``` (VLAN 6)

### PC-Site2-2 (Win 7)

#### Configuration IP

* IP: ```10.2.2.3```
* Masque de sous-réseau: ```255.255.255.0```
* Passerelle par défaut: ```10.2.2.1``` (VLAN 6)

#### Configuration pare feu

* Désactiver le pare feu
* Chemin ```Panneau de configuration/Pare-feu Windows/ Activer ou désactiver ```

### DAB-Site1-1


### DAB-Site2-2

# Configuration réseaux Machine 2

__*Remarques générales*__
> * Configurer les VLANs avant de configurer les machines

## 1. Script pour lancer les machines
```bash

```

## 2. Adresses IPs:

### Configuration des VLAN à partir de l'hôte

Configurer les VLAN de la machine physique 2.
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

### PC-Site2-1 (Win 7)
#### Configuration IP
#### Configuration pare feu
### PC-Site2-2 (Win 7)
#### Configuration IP
#### Configuration pare feu


* ```ipconfig -a``` pour identifier toutes les interfaces des machines