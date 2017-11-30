---
title: Converting an account to a multisig account
taxonomy:
    category: docs
---

 
NIS natively supports m of n multisig accounts. This means an account can be converted into a multisig account having n cosignatories and m of those cosignatories need to sign a transaction from the multisig account in order to complete the transaction. To convert a normal account to a multisig account an aggregate modification transaction (see Appendix A: MultisigAggregateModificationTransaction ) must be sent to the network. Assuming you want to convert Alice with public key: 

 
into a 2 of 3 multisig account meaning the account has 3 cosignatories and at least 2 cosignatories have to sign to complete a multisig transaction:

 
you would have to create a JSON object that looks similar to this (test network):

 
```json
 {
        "transaction":
        {
        "timeStamp": 9111526,
        "fee": 28000000,
        "type": 4097,
        "deadline": 9154726,
        "version": -1744830462,
        "signer": "a1aaca6c17a24252e674d155713cdf55996ad00175be4af02a20c67b59f9fe8a",
        "modifications": [
        {
        "modificationType": 1,
        "cosignatoryAccount": "6083df7119d43e815ed2967c795f806f6b73f8f92a56a7611e3848816ec50958"
        },{
        "modificationType": 1,
        "cosignatoryAccount": "0662ed29cbfa7038530fb7f52df865eed6708d51bc7a24bcd05db35185b53c70"
        },{
        "modificationType": 1,
        "cosignatoryAccount": "cc61676a4275abcffd10a9ea1081091ff054a1a8a720429256aebf8034aab099"
        }
        ],
        "minCosignatories" : {
        "relativeChange": 2
        }
        },
        "privateKey": "00983bb01d05edecfaef55df9486c111abb6299c754a002069b1d0ef4537441bda"
        }
``` 
Note again that there is no signature since the transaction will be signed by NIS.

 
After the transaction is signed by NIS and is accepted by the network by including it into a block, the account Alice is now a 2 of 3 multisig account. From this point on, only the cosignatories can initiate a transaction for the account Alice. Also, any transaction from account Alice must be a multisig transaction.

 
