---
title: AccountHistoricalDataViewModel
taxonomy:
    category: docs
---

 
##### Description: 
Nodes can support a feature for retrieving historical data of accounts. If a node supports this feature, it will return an array of AccountHistoricalDataViewModel objects.

 
##### JSON structure by example: 
```json
{
        "height": 8976,
        "address": "NALICELGU3IVY4DPJKHYLSSVYFFWYS5QPLYEZDJJ",
        "balance": 80670000000,
        "vestedBalance": 13949175142,
        "unvestedBalance": 66720824858,
        "importance": 0.00008166760846617221,
        "pageRank": 0.0006944567083595363
        }
``` 
##### Description of the fields: 

| Parameter | Description |
|------|------|
| height | The height for which the data is valid. |
| address | The address of the account. |
| balance | The balance of the account. |
| vestedBalance | The vested part of the balance. |
| unvestedBalance | The unvested part of the balance. |
| importance | The importance of the account. |
| pageRank | The page rank part of the importance. |

 
