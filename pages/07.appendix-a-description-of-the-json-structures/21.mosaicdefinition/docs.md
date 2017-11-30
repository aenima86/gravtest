---
title: MosaicDefinition
taxonomy:
    category: docs
---

 
##### Description: 
A mosaic definition describes an asset class. Some fields are mandatory while others are optional. The properties of a mosaic definition always have a default value and only need to be supplied if they differ from the default value.

 
##### JSON structure by example: 
```json
{
        "creator": "10cfe522fe23c015b8ab24ef6a0c32c5de78eb55b2152ed07b6a092121187100",
        "id": {
        "namespaceId": "alice.drinks",
        "name": "orange juice"
        },
        "description": "A healthy drink with lots of vitamins",
        "properties": [{
        "name": "divisibility",
        "value": "3"
        },{
        "name": "initialSupply",
        "value": "1000"
        },{
        "name": "supplyMutable",
        "value": "false"
        },{
        "name": "transferable",
        "value": "true"
        }],
        "levy": {
        "type": 1,
        "recipient": "TD3RXTHBLK6J3UD2BH2PXSOFLPWZOTR34WCG4HXH",
        "mosaicId": {
        "namespaceId": "alice.drinks",
        "name": "orange juice"
        },
        "fee": 1000
        }
        }
``` 
##### Description of the fields: 

| Parameter | Description |
|------|------|
| creator | The public key of the mosaic definition creator. |
| id | The mosaic id. See MosaicId. |
| description | The mosaic description. The description may have a length of up to 512 characters and cannot be empty. |
| properties | The mosaic properties. The properties may be an empty array in which case default values for all properties are applied. See MosaicProperties for further details.  |
| levy | The optional levy for the mosaic. A creator can demand that each mosaic transfer induces an additional fee. See MosaicLevy for further details.  |

 
