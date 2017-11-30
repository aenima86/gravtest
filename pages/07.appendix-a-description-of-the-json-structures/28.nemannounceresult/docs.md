---
title: NemAnnounceResult
taxonomy:
    category: docs
---

 
##### Description: 
The NemAnnounceResult extends the NemRequestResult by supplying the additional fields 'transactionHash' and in case of a multisig transaction 'innerTransactionHash'.

 
##### JSON structure by example: 
```json
{
        "type": 4,
        "code": 6,
        "message": "status",
        "transactionHash": {
        "data":"c1786437336da077cd572a27710c40c378610e8d33880bcb7bdb0a42e3d35586"
        },
        "innerTransactionHash": {
        "data": "44e4968e5aa35fe182d4def5958e23cf941c4bf809364afb4431ebbf6a18c039"
        }
        }
``` 
##### Description of the fields: 

| Parameter | Description |
|------|------|
| type |  See description of NemRequestResult. |
| code |  See description of NemRequestResult. |
| message |  See description of NemRequestResult. |
| transactionHash |  The JSON hash object of the transaction. |
| innerTransactionHash |  The JSON hash object of the inner transaction or null if the transaction is not a multisig transaction. |

 
