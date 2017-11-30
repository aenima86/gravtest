---
title: Adding and removing cosignatories
taxonomy:
    category: docs
---

 
It is possible to modify the list of cosignatories for a multisig account. This is done via a aggregate modification transaction wrapped in a multisig transaction.

 
Suppose you want to add the cosignatory Hachi to the multisig account Alice and increase the minimum of cosignatories required to complete a transaction from 2 to 3.

 
To do that, one of the existing cosignatories (assuming here it is Jusan) must initiate the corresponding multisig transaction (test network):

 
```json
{
        "transaction":
        {
        "timeStamp": 9111526,
        "fee": 6000000,
        "type": 4100,
        "deadline": 9154726,
        "version": -1744830462,
        "signer": "6083df7119d43e815ed2967c795f806f6b73f8f92a56a7611e3848816ec50958",
        "otherTrans": {
        "timeStamp": 9111526,
        "fee": 16000000,
        "type": 4097,
        "deadline": 9154726,
        "version": -1744830462,
        "signer": "a1aaca6c17a24252e674d155713cdf55996ad00175be4af02a20c67b59f9fe8a",
        "modifications": [
        {
        "modificationType": 1,
        **"cosignatoryAccount": "6c66ea288522990db7a0a63c9c20f532cdcb68dc3c9544fb20f7322c92ceadbb"**
        }
        ],
        "minCosignatories" : {
        "relativeChange": 1
        }
        },
        "signatures":[
        ]
        },
        "privateKey": "00be34fdb20a9f6fed51376f0bab9f25ea7a48d610324588a6b203d0a1a6db4bc1"
        } 
``` 
After NIS has signed and broadcasted the transaction to the network, one of the other two cosignatories needs to sign the transaction as well as explained in Initiating a multisig transaction. After the transaction was successfully included in a block, the account Alice is a 3 of 4 multisig account.

 
If at some later time Bob, Jusan and Go want to remove the cosignatory Hachi to make it a 2 of 3 multisig account again one of cosignatories could initiate a similar transaction as above but this time with "modificationType" set to **2** (which means remove) and using a minimum cosignatories relative change value of **-1**. For removing a cosignatory all cosignatories except the one being removed need to sign the transaction. Once approved by the network Hachi is no longer cosignatory of the multisig account Alice.

 
 Removal of accounts is NOT final and might be subject of change 

 
