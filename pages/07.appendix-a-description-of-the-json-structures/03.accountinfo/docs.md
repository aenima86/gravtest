---
title: AccountInfo
taxonomy:
    category: docs
---

 
##### Description: 
The account structure describes basic information for an account.

 
##### JSON structure by example: 
```json
{
        "address": "TALICELCD3XPH4FFI5STGGNSNSWPOTG5E4DS2TOS",
        "balance": 124446551689680,
        "vestedBalance": 1041345514976241,
        "importance": 0.010263666447108395,
        "publicKey": "a11a1a6c17a24252e674d151713cdf51991ad101751e4af02a20c61b59f1fe1a",
        "label": null,
        "harvestedBlocks": 645
        }
``` 
##### Description of the fields: 
##### Description of the fields: 

| Parameter | Description |
|------|------|
| address | The address of the account. |
| balance | The balance of the account in micro NEM. |
| vestedBalance | The vested part of the balance of the account in micro NEM. |
| importance | The importance of the account. |
| publicKey | The public key of the account. |
| label | The label of the account (not used, always null). |
| harvestedBlocks | The number blocks that the account already harvested. |

 
