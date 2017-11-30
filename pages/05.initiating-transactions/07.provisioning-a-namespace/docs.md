---
title: Provisioning a namespace
taxonomy:
    category: docs
---

 
This chapter explains what actions you have to take in order to provision (i.e. rent) a namespace. You can find a detailed description of namespaces in the chapter Namespaces. Suppose you want to claim the root namespace 'alice' and the sub-namespace 'alice.vouchers'. The first action would be to issue an ProvisionNamespaceTransaction. As usual this is done by sending a RequestPrepareAnnounce JSON object to NIS which in this case would look like this: 

 
```json

            {
            "transaction":
            {
            "timeStamp": 9111526,
            "fee": 108000000,
            "type": 8193,
            "deadline": 9154726,
            "version": -1744830463,
            "signer": "d99e88c90da71a4b0d848454e59e296c9ef7a8f018f3eaa3a198dc460b6621a4",
            "rentalFeeSink": "3e82e1c1e4a75adaa3cba8c101c3cd31d9817a2eb966eb3b511fb2ed45b8e262",
            "rentalFee": 50000000000,
            "newPart": "alice",
            "parent": null
            },
            "privateKey": "00983bb01d05edecfaef55df9486c111abb6299c754a002069b1d0ef4537441bda"
            }
        
``` 
The field 'parent' is set to null indicating that you want to rent a root namespace. You also have to be sure that no one else has already rented that root namespace or NIS will return an error. The high rental fee is there to prevent users from squatting all kinds of root namespaces. This fee is not given to the harvesters because this would encourage harvesters to wait until they are allowed to harvest a block, include their provision namespace transaction in that block and thus essentially getting the namespace for free. Instead all rental fees are collected in a special multisig account. The most common error responses from NIS will be:
* The namespace is already owned by another account.
* The namespace contains illegal character or a reserved namespace part.
* The public key of the rental fee sink is invalid.
* The rental fee is invalid (i.e. too low). If NIS responses with a success message, the transaction is broadcasted to the network and will get included in a future block. After the transaction is included in a block you can check that you are the owner of that namespace by issuing an /account/namespaces request, see chapter xyz. 

 
To rent the sub-namespace 'alice.vouchers' you need again send a RequestPrepareAnnounce JSON object to NIS which this time looks like this:

 
```json

             {
             "transaction":
             {
             "timeStamp": 9111526,
             "fee": 108000000,
             "type": 8193,
             "deadline": 9154726,
             "version": -1744830463,
             "signer": "d99e88c90da71a4b0d848454e59e296c9ef7a8f018f3eaa3a198dc460b6621a4",
             "rentalFeeSink": "3e82e1c1e4a75adaa3cba8c101c3cd31d9817a2eb966eb3b511fb2ed45b8e262",
             "rentalFee": 5000000000,
             "newPart": "vouchers",
             "parent": "alice"
             },
             "privateKey": "00983bb01d05edecfaef55df9486c111abb6299c754a002069b1d0ef4537441bda"
             }
         
``` 
This time the parent is set to the parent namespace, in this case the root namespace 'alice'. The rental fee for a sub-namespace is 10% of the fee for a root namespace, i.e. 5000 XEM. Be sure to wait until you own the root namespace or NIS will respond with an error message. Once the transaction is included in a block, you own the sub-namespace 'alice.vouchers' as long as the root namespace 'alice' does not expire.

 
If you want to rent the sub-namespace 'alice.vouchers.special' you have to issue a RequestPrepareAnnounce object again, this time with parent set to 'alice.vouchers'. and the newPart being 'special'.

 
After a year the root namespace expires. In order not to let this happen you need to send a provision namespace transaction for the root namespace within one month before it expires. The RequestPrepareAnnounce object is the same as if you were renting the namespace for the first time. The renewal of the root namespace also automatically renews any sub-namespace of that root namespace that the account already owns. 

 
