---
title: MosaicDefinitionMetaDataPair
taxonomy:
    category: docs
---

 
##### Description: 
A mosaic definition consists of a database id and a mosaic definition object. The id is needed for requests that support paging.

 
##### JSON structure by example: 
```json
{
        "meta" {
        "id": 3541
        }
        "mosaic": {
        "creator": "10cfe522fe23c015b8ab24ef6a0c32c5de78eb55b2152ed07b6a092121187100",
        "id": {
        "namespaceId": "alice.drinks",
        "name": "orange juice"
        },
        "description": "A healthy drink with lots of vitamins",
        "properties": [
        ]
        }
        }
``` 
##### Description of the fields: 

| Parameter | Description |
|------|------|
| meta | The label for the meta data object. |
| id | The id for the mosaic definition object. |
| mosaic | The label for the mosaic definition object. See MosaicDefinition for a detailed description of the object.  |
| creator | The public key of the mosaic definition creator. |
| id | The mosaic id. See MosaicId. |
| description | The mosaic description. The description may have a length of up to 512 characters and cannot be empty. |
| properties | The mosaic properties. |

 
