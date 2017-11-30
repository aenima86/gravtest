---
title: AccountImportanceViewModel
taxonomy:
    category: docs
---

 
##### Description: 
Each account is assigned an importance in the NEM network. The ability of an account to generate new blocks is proportional to its importance. The importance is a number between 0 and 1.

 
##### JSON structure by example: 
```json
{
        "address": "TALICELCD3XPH4FFI5STGGNSNSWPOTG5E4DS2TOS"
        "importance":
        {
        "isSet": 1,
        "score": 0.0011561555164258449,
        "ev": 0.004367936531009263,
        "height": 38413
        }
        }
``` 
##### Description of the fields: 

| Parameter | Description |
|------|------|
| address | The address of the account. |
| importance | Substructure that describes the importance of the account. |
| isSet | Indicates if the fields "score", "ev" and "height" are available.isSet can have the values 0 or 1. In case isSet is 0 the fields are not available.  |
| score | The importance of the account. The importance ranges between 0 and 1. |
| ev | The page rank portion of the importance. The page rank ranges between 0 and 1. |
| height | The height at which the importance calculation was performed. |

 
