---
title: NamespaceMetaDataPair
taxonomy:
    category: docs
---

 
##### Description: 
A namespace consists of a namespace object and a database id. the id is needed for requests that support paging.

 
##### JSON structure by example: 
```json
{
        "meta":{
        "id":26264,
        },
        "namespace":{
        "fqn": "makoto.metal.coins",
        "owner": TD3RXTHBLK6J3UD2BH2PXSOFLPWZOTR34WCG4HXH",
        "height": 13465
        }
        }
``` 
##### Description of the fields: 

| Parameter | Description |
|------|------|
| meta | The label for the meta data object. |
| id | The database id for the namespace object. |
| namespace | The label for the namespace object. |
| fqn | The fully qualified name of the namespace, also named namespace id. |
| owner | The owner of the namespace. |
| height | The height at which the ownership begins. |

 
