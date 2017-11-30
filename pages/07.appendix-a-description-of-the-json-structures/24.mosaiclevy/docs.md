---
title: MosaicLevy
taxonomy:
    category: docs
---

 
##### Description: 
A mosaic definition can optionally specify a levy for transferring those mosaics. This might be needed by legal entities needing to collect some taxes for transfers.

 
##### JSON structure by example: 
```json
{
        "type": 1,
        "recipient": "TD3RXTHBLK6J3UD2BH2PXSOFLPWZOTR34WCG4HXH",
        "mosaicId": {
        "namespaceId": "nem",
        "name": "xem"
        },
        "fee": 1000
        }
``` 
##### Description of the fields: 

| Parameter | Description |
|------|------|
| type | The levy type. The following types are supported: 1: The levy is an absolute fee. The field 'fee' states how many sub-units of the specified mosaic will be transferred to the recipient. 2: The levy is calculated from the transferred amount. The field 'fee' states how many percentiles of the transferred quantity will transferred to the recipient.   |
| recipient | The recipient of the levy. |
| mosaicId | The mosaic in which the levy is paid. |
| recipient | The fee. The interpretation is dependent on the type of the levy |

 
