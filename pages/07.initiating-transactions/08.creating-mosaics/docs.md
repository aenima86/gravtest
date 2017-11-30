---
title: Creating mosaics
taxonomy:
    category: docs
---

 
### Creating a mosaic definition 
The basics of the NEM mosaic concept can be found in the chapter Mosaics. To define and create a mosaic type you need to issue a MosaicDefinitionCreationTransaction. As usual this is done by sending a RequestPrepareAnnounce JSON object to NIS which in this case would look like this: 

 
```json

            {
            "transaction":
            {
            "timeStamp": 9111526,
            "fee": 108000000,
            "type": 16385,
            "deadline": 9154726,
            "version": -1744830463,
            "signer": "cbda3edb771d42801a5c6ce0725f9374efade19a8933d6ac22ccfa50c777d0f9",
            "creationFee": 50000000000,
            "creationFeeSink": "53e140b5947f104cabc2d6fe8baedbc30ef9a0609c717d9613de593ec2a266d3",
            "mosaicDefinition": {
            "creator": "cbda3edb771d42801a5c6ce0725f9374efade19a8933d6ac22ccfa50c777d0f9",
            "description": "precious vouchers",
            "id": {
            "namespaceId": "alice.vouchers",
            "name": "Alice's gift vouchers"
            },
            "properties": [{
            "name": "divisibility",
            "value": "0"
            },{
            "name": "initialSupply",
            "value": "1000"
            },{
            "name": "supplyMutable",
            "value": "true"
            },{
            "name": "transferable",
            "value": "false"
            }
            ],
            "levy": {
            "type": 1,
            "recipient": "TD3RXTHBLK6J3UD2BH2PXSOFLPWZOTR34WCG4HXH",
            "mosaicId": {
            "namespaceId": "nem",
            "name": "xem"
            },
            "fee": 10
            }
            }
            },
            "privateKey": "00983bb01d05edecfaef55df9486c111abb6299c754a002069b1d0ef4537441bda"
            }
        
``` 
With the above transaction a mosaic with id 'alice.vouchers * Alice's gift vouchers' is created within the namespace 'alice.vouchers'. The account must own that namespace in order to be able to create a mosaic in it. There is a high creation fee for creating mosaic definition in order to discourage squatting. As stated in the previous chapter, the fee is not transferred to the block harvester but to a special account whose public key is provided in the field 'creationFeeSink'.

 
The mosaic has the following properties:
* It is not divisible, i.e. the vouchers that the mosaic represents can only be transferred as a whole, not partially.
* There will be initially 1000 vouchers (mosaics of that type).
* The supply (the number of mosaics of that type) can be changed at a later point.
* The vouchers are not transferable among accounts. Only the creator of the mosaic can transfer vouchers to other accounts and once an account owns a voucher it can only be transferred back to the creator. The definition also implies a levy with each transfer. The levy section states that there is an additional fee of 10 XEM for each transfer. That fee is send to the recipient with address TD3RXTHBLK6J3UD2BH2PXSOFLPWZOTR34WCG4HXH. This levy part of the transaction is optional. If that part is ommited no additional fee arises from transferring the mosaics. 

 
Reasons for NIS now accepting the transactions are most likely:
* The transaction signer does not own the namespace that is specified in the mosaic definition or the namespace has expired.
* A mosaic definition with the specified mosaic id already exists (see discussion below about altering mosaic definitions).
* The public key of the creation fee sink is invalid or the creation fee is too low.
* The mosaic id in the levy part of the transaction is unknown to NIS. 

 
When the transaction gets included into a block and the block is executed, The creator will be credited the amount of mosaics stated in the 'initialSupply' field (in the example 1000).

 
### Altering a mosaic definition 
There might be the need to alter a mosaic definition, either because you want to change the description or because you supplied faulty properties or faulty levy data. This is done simply by issuing another mosaic definition creation transaction as described above with the same mosaic id but different description/properties/levy. However there are some restriction when doing so:
* The description can be changed at any point even if the creator does not own the entire supply.
* Properties and the levy data can **only** be changed if the creator owns every single mosaic of that type. This is necessary to prevent the creator from secretly introducing a levy or inflating the mosaic by increasing the supply. Keep in mind that renewing the mosaic definition costs you 50000 XEM again, so it is worthwhile to double check the data before issuing the transaction. 

 
### Changing the mosaic supply 
In case you created a mosaic definition with 'supplyMutable' set to true, you are able to change the mosaic supply. To do so, you must issue a MosaicSupplyChangeTransaction. This is done by sending a RequestPrepareAnnounce JSON object to NIS which in this case would look like this: 

 
```json

            {
            "transaction":
            {
            "timeStamp": 9111526,
            "fee": 108000000,
            "type": 16386,
            "deadline": 9154726,
            "version": -1744830463,
            "signer": "d99e88c90da71a4b0d848454e59e296c9ef7a8f018f3eaa3a198dc460b6621a4",
            "supplyType": 1,
            "delta": 100,
            "mosaicId": {
            "namespaceId": "alice.vouchers",
            "name": "Alice's gift vouchers"
            }
            },
            "privateKey": "00983bb01d05edecfaef55df9486c111abb6299c754a002069b1d0ef4537441bda"
            }
        
``` 
In the above example the supply for an existing mosaic with id 'alice.vouchers * Alice's gift vouchers' is changed. Specifically
* the supplyType 1 means the supply is increased (a supply type of 2 means a supply decrease).
* the delta of 100 means that another 100 units are credited to the creators account. 

 
Reasons for NIS now accepting the transactions are most likely:
* The transaction signer is not the creator os the mosaic.
* The mosaic definition states that the supply is immutable.
* When attempting to increase the supply, the total supply must not exceed 9,000,000,000 mosaics.
* When attempting to decrease the supply, the creator must own the number of mosaics that he wants to delete. 

 
After the transaction gets included into the block chain, the supply change is realized.

 
