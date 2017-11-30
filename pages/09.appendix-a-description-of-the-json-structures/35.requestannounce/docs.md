---
title: RequestAnnounce
taxonomy:
    category: docs
---

 
##### Description: 
A RequestAnnounce object is used to transfer the transaction data and the signature to NIS in order to initiate and broadcast a transaction.

 
##### JSON structure by example: 
```json
{
        "data": "010100000100000000000000200000002b76078fa709bbe675
        2222b215abc7ec0152ffe831fb4f9aed3e7749a425900a0009
        3d0000000000000000002800000054444e46555946584f5353
        334e4e4c4f35465a5348535a49354c33374b4e514945485055
        4d584c54c0d45407000000000b00000001000000030000000c
        3215",
        "signature": "db2473513c7f0ce9f8de6345f0fbe773
        dc687eb571123d08eab4d98f96849eae
        b63fa8756fb6c59d9b9d0e551537c1cd
        ad4a564747ff9291db4a88b65c97c10d"
        }
``` 
##### Description of the fields: 

| Parameter | Description |
|------|------|
| data | The transaction data as string. The string is created by first creating the corresponding byte array (see chapter 6.7) and then converting the byte array to a hexadecimal string.  |
| signature | The signature for the transaction as hexadecimal string. |

 
