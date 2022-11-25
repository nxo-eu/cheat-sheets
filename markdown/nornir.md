```yaml
title: Nornir
category: Python
layout: 2022/sheet
```
**Table of Contents**

<!-- vscode-markdown-toc -->
* 1. [nornir](#Norni)
    * 1.1. [Installation](#Controlstructures)
	* 1.2. [Initialisation](#Initialisation)
	* 1.3. [Inventaire](#Inventaire)
	* 1.4. [Tâches](#Tâches)

###  1.1. <a name='Installation'></a>Installation

Pour installer, nous avons seulement besoin de l'aide de l'outil pip.

```shell
pip install nornir
```

Pour vérifier qu'on a bien installer nornir :
```shell
python
>>> from nornir import InitNornir
>>>
```


###  1.2. <a name='Initialisation'></a>Initialisation
Pour créer un objet nornir il faut :
```py
from nornir import InitNornir
nr = InitNornir(config_file="config.yaml")
```
En créant un fichier config.yaml qui stock les informations concenant les hotes, les groupes,des valeurs par défaut (les identifiants, mots de passe,... ). En voici un exemple : 
```yaml
inventory:
       plugin: SimpleInventory
       options:
            host_file: 'inventory/hosts.yaml'
            group_file: 'inventory/groups.yaml'
            defaults_file: 'inventory/defaults.yaml'
runner:
       plugin: threaded
       options:
            num_workers: 2
```
#### Ou on peut utiliser sans fichier config :

```py
from nornir import InitNornir
nr = InitNornir(
    runner={
        "plugin": "threaded",
        "options": {
            "num_workers": 2,
        },
    },
    inventory={
        "plugin": "SimpleInventory",
        "options": {
            "host_file": "inventory/hosts.yaml",
            "group_file": "inventory/groups.yaml"
        },
    },
)
```
On peut également combiner ces deux méthodes.

###  1.2. <a name='Inventaire'></a>Inventaire
A l'aide du plugin *SimpleInventory*, nous allons stocker nos hôtes, groupes et valeurs par défaut dans un dossier inventory. Voici un exemple :
```yaml
#inventory/host.yaml
---
veos1:
    hostname: 172.16.2.1
    groups:
        - veos
    connection_options:
        napalm:
            extras:
                optional_args:
                    enable_password: 'password'

veos2:
    hostname: 172.16.2.2
    groups:
        - veos
    connection_options:
        napalm:
            extras:
                optional_args:
                    enable_password: 'password'
```

```yaml
#inventory/groups.yaml
---
veos:
    platform: 'eos'
    data:
        vlans:
            - {id: 10, name: test10, ip: 10.1.10.254}
            - {id: 20, name: test20, ip: 10.1.20.254}
        accesses:
            - {interface: 3, vlan_id: 10}
            - {interface: 4, vlan_id: 20}
        trunks:
            - {interface: 1, id: 1}
            - {interface: 2, id: 1}
```
Ici, on voir qu'on a meme stocciée les adresses ip dans les vlans.
```yaml
---
username: 'admin'
password: 'password'
```