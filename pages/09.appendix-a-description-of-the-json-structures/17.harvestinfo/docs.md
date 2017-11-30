---
title: HarvestInfo
taxonomy:
    category: docs
---

 
##### Description: 
A HarvestInfo object contains information about a block that an account harvested.

 
##### JSON structure by example: 
```json
{
        "timeStamp": 8963798,
        "id": 254378,
        "difficulty": 46534789865332,
        "totalFee": 2041299054,
        "height": 38453
        }
``` 
##### Description of the fields: 

| Parameter | Description |
|------|------|
| timeStamp | The number of seconds elapsed since the creation of the nemesis block. |
| id | The database id for the harvested block. |
| difficulty | The block difficulty. The initial difficulty was set to 100000000000000. The block difficulty is always between one tenth and ten times the initial difficulty.  |
| totalFee | The total fee collected by harvesting the block. |
| height | The height of the harvested block. |

 
