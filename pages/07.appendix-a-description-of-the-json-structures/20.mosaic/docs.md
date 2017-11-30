---
title: Mosaic
taxonomy:
    category: docs
---

 
##### Description: 
A mosaic describes an instance of a mosaic definition. Mosaics can be transferred by means of a transfer transaction.

 
##### JSON structure by example: 
```json
{
        "mosaicId": {
        "namespaceId": "alice.drinks",
        "name": "orange juice"
        },
        "quantity": 123000
        }
``` 
##### Description of the fields: 

| Parameter | Description |
|------|------|
| mosaicId | The mosaic id. See MosaicId |
| quantity | The mosaic quantity. The quantity is always given in smallest units for the mosaic, i.e. if it has a divisibility of 3 the quantity is given in millis.  |

 
