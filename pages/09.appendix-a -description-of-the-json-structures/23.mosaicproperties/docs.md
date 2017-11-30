---
title: MosaicProperties
taxonomy:
    category: docs
---

 
##### Description: 
Each mosaic definition comes with a set of properties. Each property has a default value which will be applied in case it was not specified. Future release may add additional properties to the set of available properties. The available properties and their default values are: * **divisibility:** defines the smallest sub-unit that a mosaic can be divided into. A divisibility of 0 means that only entire units can be transferred while a divisibility of 3 means the mosaic can be transferred in milli-units. * **initialSupply:** defines how many units of the mosaic are initially created. These mosaics are credited to the creator of the mosaic. The initial supply has an upper limit of 9,000,000,000 units. * **supplyMutable:** determines whether or not the supply can be changed by the creator at a later point using a MosaicSupplyChangeTransaction. Possible values are "true" and "false", the former meaning the supply can be changed and the latter that the supply is fixed for all times. * **transferable:** determines whether or not the a mosaic can be transferred to a user other than the creator. In certain scenarios it is not wanted that user are able to trade the mosaic (for example when the mosaic represents bonus points which the company does not want to be tranferable to other users). Possible values are "true" and "false", the former meaning the mosaic can be arbitrarily transferred among users and the latter meaning the mosaic can only be transferred to and from the creator. 

 
##### JSON structure by example: 
```json
[{
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
        }]
``` 
##### Description of the fields: 

| Parameter | Description |
|------|------|
| name | The name of the mosaic property. |
| value | The name of the mosaic property. |

 
