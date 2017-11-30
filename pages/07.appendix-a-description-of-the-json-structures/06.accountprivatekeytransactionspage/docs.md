---
title: AccountPrivateKeyTransactionsPage
taxonomy:
    category: docs
---

 
##### Description: 
The account private key transactions page contains data that NIS needs to retrieve a set of transactions from the database. The data includes the private key of the account for which transactions are retrieved. Use requests that use this structure only when NIS is running locally.

 
The fields "hash" and "id" are optional.

 
##### JSON structure by example: 
```json
{
        "value": "68e4f79f886927de698df4f857de2aada41ccca6617e56bb0d61623b35b08cc0",
        "hash": "44e4968e5aa35fe182d4def5958e23cf941c4bf809364afb4431ebbf6a18c039",
        "id": "12345"
        }
``` 
##### Description of the fields: 

| Parameter | Description |
|------|------|
| value | The private key as hexadecimal string. |
| hash | The optional hash value. |
| id | The optional transaction id. |

 
