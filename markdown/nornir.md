# Framework Nornir

### Folder called inventory, he is going to stock :
- defaults.yaml
- groups.yaml
- hosts.yaml <br/>

In the file **hosts** : we have to list hosts and their data.<br/>
In the file **groups** : we have to define the different groups and their informations.<br/>
In the file **defaults** : We have to define the default username and the password if ther are.<br/>
Now, we have to create a file config.yaml to regroup all files :<br/>

```yaml
---
core :
    num_workers : 100
inventory :
    plugin : nornir.plugins.inventory.simple.SimpleInventory
    SimpleInventory
    options :
        host_file: "inventory/hosts.yaml"
        group_file: "inventory/groups.yaml"
        defaults_file: "inventory/defaults.yaml"


```
**To see the structuraction we have to :**
```py
from nornir.core.inventory import Host
import json
print(json.dumps(Host.schema(), indent=4))

#To affiche :
from nornir import InitNornir<br/>
nr = InitNornir(config_file="config.yaml")
print(nr.inventory.host) #We can also affiche  groups.

#To filter :

##We use the InitNornir's method called filter.
# For example: to filter host they have only the host who have a site called :
 from nornir import InitNornir
  nr = InitNornir(config_file="config.yaml")
  print( nr.filter( site = "bma" ).inventory.hosts.keys() )
```

