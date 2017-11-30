---
title: Initiating a multisig transaction
taxonomy:
    category: docs
---

 
As stated above, only one of the cosignatories (Bob, Jusan and Go) can create a transaction for the account Alice.

Lets assume Bob wants to start a transfer transaction which transfers 1000 NEM from account Alice to account Jusan. Since the account Alice is a multisig account the transfer transaction (in the JSON object the "otherTrans" structure) must be wrapped in a multisig transaction (see Appendix A: MultisigTransaction ). The corresponding RequestPrepareAnnounce object would look similar to this (test network): 

 
```json
 {
        "transaction":
        {
        "timeStamp": 9111526,
        "fee": 3000000,
        "type": 4100,
        "deadline": 9154726,
        "version": -1744830463,
        "signer": "6083df7119d43e815ed2967c795f806f6b73f8f92a56a7611e3848816ec50958",
        "otherTrans": {
        "timeStamp": 9111526,
        "amount": 1000000000,
        "fee": 4000000,
        "recipient": "TBJUSANZ63AKNJ57XMK6Y2IBH55UNNRXJFZRDTRW",
        "type": 257,
        "deadline": 9154726,
        "message":
        {
        "payload": "",
        "type": 1
        },
        "version": -1744830463,
        "signer": "a1aaca6c17a24252e674d155713cdf55996ad00175be4af02a20c67b59f9fe8a"
        },
        "signatures":[
        ]
        },
        "privateKey": "00a6e2526b5cc84f9174c4ff050ca352623061115951c649b36b08409c4ccb7b2e"
        }
``` 
NIS will sign the transaction and publish it. The returned NemAnnounceResult object this time contains the hash of the inner transaction (otherTrans in the above structure):

 
```json
    {
        "type": 1,
        "code": 1,
        "message": "SUCCESS"
        "transactionHash": {
            "data":"c1786437336da077cd572a27710c40c378610e8d33880bcb7bdb0a42e3d35586"
        },
        "innerTransactionHash": {
            **"data": "44e4968e5aa35fe182d4def5958e23cf941c4bf809364afb4431ebbf6a18c039"**
        }
    }
``` 
The hash is needed by the nodes that will create multisig signature transactions for the above transaction.

 
At this point the transaction cannot (and will not) be included in a block because none of the other cosignatories - Jusan and Go - has signed the transaction yet …

 
### Cosigning multisig transaction 
… to do so, Jusan or Go must initiate a multisig signature transaction (see Appendix A: MultisigSignatureTransaction ). Jusan has to create a RequestPrepareAnnounce JSON object that looks similar to this (test network): 

 
```json
 {
        "transaction":
        {
        "timeStamp": 9111526,
        "fee": 6000000,
        "type": 4098,
        "deadline": 9157365,
        "version": -1744830463,
        "signer": "0662ed29cbfa7038530fb7f52df865eed6708d51bc7a24bcd05db35185b53c70",
        "otherHash": {
        **"data": "44e4968e5aa35fe182d4def5958e23cf941c4bf809364afb4431ebbf6a18c039"**
        },
        **"otherAccount": "TALICELCD3XPH4FFI5STGGNSNSWPOTG5E4DS2TOS"**
        },
        "privateKey": "00be34fdb20a9f6fed51376f0bab9f25ea7a48d610324588a6b203d0a1a6db4bc1"
        }
``` 
Note that Jusan used the hash ('otherHash') returned by NIS from Bob's request.

 
After NIS has signed the transaction and sent it to the network, the signature transaction will be attached to the multisig transaction. With Jusan having signed the multisig transaction that Bob initiated, two of the three cosignatories have signed the inner transfer transaction (Bob indirectly signed by initiating the multisig transaction) and thus the multisig transaction can be included in a block. 

 
