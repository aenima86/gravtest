---
title: RequestPrepareAnnounce
taxonomy:
    category: docs
---

 
##### Description: 
A RequestPrepareAnnounce object is used to transfer transaction data and a private key to NIS in order to initiate and broadcast a transaction.

 
##### JSON structure by example (test network): 
```json
{
        "transaction":
        {
        "timeStamp": 9111526,
        "amount": 1000000000,
        "fee": 3000000,
        "recipient": "TDGIMREMR5NSRFUOMPI5OOHLDATCABNPC5ID2SVA",
        "type": 257,
        "deadline": 9154726,
        "message":
        {
        "payload": "74657374207472616e73616374696f6e",
        "type": 1
        },
        "version": -1744830463,
        "signer": "a1aaca6c17a24252e674d155713cdf55996ad00175be4af02a20c67b59f9fe8a"
        },
        "privateKey": "68e4f79f886927de698df4f857de2aada41ccca6617e56bb0d61623b35b08cc0"
        }
``` 
##### Description of the fields: 

| Parameter | Description |
|------|------|
| transaction | Denotes the beginning of the transaction data part. The transaction data is described in Appendix A: Transaction . The field 'signature is missing since the transaction is not signed at this point.  |
| privateKey | The private key which NIS will use to sign the transaction. |

 
