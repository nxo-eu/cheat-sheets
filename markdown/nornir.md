```yaml
title: Nornir
category: Python
layout: 2022/sheet
```
**Table of Contents**

<!-- vscode-markdown-toc -->
* 1. [nornir](#Nornir)
    * 1.1. [Installation](#Installation)
	* 1.2. [Initialization](#Initialization)
* 2. [Inventory](#Inventory)
    * 2.1. [Defaults](#Defaults)
    * 2.2. [Hosts](#Hosts)
    * 2.3. [Groups](#Groups)
* 3. [Visualisation] (#Visualisation)
	* 3.1. [Accessors](#Accessors)
    * 3.2. [Filters](#Filters)
* 4. [Tasks](#Tasks)

###  1.1. <a name='Installation'></a>Installation

To install, we only need the help of the pip tool.

```shell
pip install nornir
```

To check that nornir has been installed
```shell
python
>>> from nornir import InitNornir
>>>
```


###  1.2. <a name='Initialization'></a>Initialization
To create a nornir object, you need to :
```py
from nornir import InitNornir
nr = InitNornir(config_file="config.yaml")
```
By creating a config.yaml file that stores information about hosts, groups, default values (logins, passwords,...). Here is an example: 
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
#### Or you can use without the config file :

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
These two methods can also be combined.

###  2. <a name='Inventory'></a>Inventory
Using the *SimpleInventory* plugin, we will store our hosts, groups and defaults in an inventory folder as specified during Initialization. Here is the structure of our data:

```powershell
C:.
│   config.yaml
│   main.py
│
└───inventory
        defaults.yaml
        groups.yaml
        hosts.yaml
```

### 2.1. <a name='Defaults'></a>Defaults
We store the default values, in our case, we will store a default username and password:
```yaml
#inventory/defaults.yaml
---
username: 'admin'
password: 'password'

```

### 2.2. <a name='Hôtes'></a>Hôtes
To register a host :
```yml
---
veos1: # => Name
    hostname: 172.16.2.1 # =>IP Adress
    groups: #  => Group defined in the groups.yaml file
        - veos
    connection_options: # => Option specific to each host
        napalm:
            extras:
                optional_args:
                    enable_password: 'password'
                    # => We retrieve the password defined in the defaults.yaml file
```


### 2.3. <a name='Groups'></a>Groups
Here we will describe the common information :
```yaml
---
veos: # => Name of the group
    platform: 'eos'  # => Server
    data: => # => Information that could have been stored in the hosts.yaml file, but storing it here optimises the code.
        vlans:  # => Connecting to a virtual network
            - {id: 10, name: test10, ip: 10.1.10.254}
            - {id: 20, name: test20, ip: 10.1.20.254}
        accesses: 
            - {interface: 3, vlan_id: 10}
            - {interface: 4, vlan_id: 20}
        trunks:
            - {interface: 1, id: 1}
            - {interface: 2, id: 1}

```

### 3. <a name='Visualisation'></a>Visualisation
We will see how to display this data through a Python script
###  3.1. <a name='Accessors'></a>Accessors
To display the hosts, you only need to add this line:
```py
print(nr.inventory.hosts)
```
The same applies to groups:
```py
print(nr.inventory.groups)
```
###  3.2. <a name='Filters'></a>Filters
We can filter with a single condition.
```py
print(nr.inventory.hosts)
```
But also with multiple conditions (prioritising if possible):
```py
nr.filter(site="cmh", role="spine").inventory.hosts.keys()

```
This works for both hosts and groups.

### 4. <a name='Tasks'></a>Tasks
Here, we will make a communication between the hosts :
```py
def say(task: Task, text: str) -> Result:
    return Result(
        host=task.host,
        result=f"{task.host.name} says {text}" #=> We transmit from one host to the other the text message which is in parameter
    )
```