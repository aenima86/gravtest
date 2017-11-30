---
title: Transaction objects
taxonomy:
    category: docs
---

 
### ImportanceTransferTransaction 
##### Description: 
NIS has the ability to transfer the importance of one account to another account for harvesting. The account receiving the importance is called the remote account. Importance transfer transactions are part of the secure harvesting feature of NEM. Once an importance transaction has been included in a block it needs 6 hours to become active.

 
##### JSON structure by example (main network): 
```json
{
        "timeStamp": 9111526,
        "signature": "651a19ccd09c1e0f8b25f6a0aac5825b0a20f158ca4e0d78f2abd904a3966b6e3599a47b9ff199a3a6e1152231116fa4639fec684a56909c22cbf6db66613901",
        "fee": 3000000,
        "mode": 1,
        "remoteAccount": "cc6c9485d15b992501e57fe3799487e99de272f79c5442de94eeb998b45e0144",
        "type": 2049,
        "deadline": 9154726,
        "version": 1744830465,
        "signer": "a1aaca6c17a24252e674d155713cdf55996ad00175be4af02a20c67b59f9fe8a"
        }
``` 
##### Description of the fields: 

| Parameter | Description |
|------|------|
| timeStamp | The number of seconds elapsed since the creation of the nemesis block.  |
| signature | The transaction signature (missing if part of a multisig transaction).  |
| fee | The fee for the transaction. The higher the fee, the higher the priority of the transaction. Transactions with high priority get included in a block before transactions with lower priority.  |
| mode |  The mode. Possible values are: 1:  Activate remote harvesting.2:  Deactivate remote harvesting.  |
| remoteAccount | The public key of the receiving account as hexadecimal string.  |
| type | The transaction type. |
| deadline | The deadline of the transaction. The deadline is given as the number of seconds elapsed since the creation of the nemesis block. If a transaction does not get included in a block before the deadline is reached, it is deleted.  |
| version | The version of the structure. |
| signer | The public key of the account that created the transaction. |

 
### MosaicDefinitionCreationTransaction 
##### Description: 
Before a mosaic can be created or transferred, a corresponding definition of the mosaic has to be created and published to the network. This is done via a mosaic definition creation transaction.

 
##### JSON structure by example (test network): 
```json
{
        "timeStamp": 9111526,
        "signature": "651a19ccd09c1e0f8b25f6a0aac5825b0a20f158ca4e0d78f2abd904a3966b6e3599a47b9ff199a3a6e1152231116fa4639fec684a56909c22cbf6db66613901",
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
        "value": "3"
        },{
        "name": "initialSupply",
        "value": "1000"
        },{
        "name": "supplyMutable",
        "value": "false"
        },{
        "name": "transferable",
        "value": "true"
        }
        ],
        "levy": {
        "type": 1,
        "recipient": "TD3RXTHBLK6J3UD2BH2PXSOFLPWZOTR34WCG4HXH",
        "mosaicId": {
        "namespaceId": "nem",
        "name": "xem"
        },
        "fee": 1000
        }
        }
        }
``` 
##### Description of the fields: 

| Parameter | Description |
|------|------|
| timeStamp | The number of seconds elapsed since the creation of the nemesis block. |
| signature | The transaction signature (missing if part of a multisig transaction). |
| fee | The fee for the transaction. The higher the fee, the higher the priority of the transaction. Transactions with high priority get included in a block before transactions with lower priority.  |
| type | The transaction type. |
| deadline | The deadline of the transaction. The deadline is given as the number of seconds elapsed since the creation of the nemesis block. If a transaction does not get included in a block before the deadline is reached, it is deleted.  |
| version | The version of the structure. |
| signer | The public key of the account that created the transaction. |
| creationFee | The fee for the creation of the mosaic. |
| creationFeeSink | The public key of the account to which the creation fee is tranferred. |
| mosaicDefinition | The actual mosaic definition. See MosaicDefinition for details. |

 
### MosaicSupplyChangeTransaction 
##### Description: 
In case a mosaic definition has the property 'supplyMutable' set to true, the creator of the mosaic definition can change the supply, i.e. increase or decrease the supply.

 
##### JSON structure by example (test network): 
```json
{
        "timeStamp": 9111526,
        "signature": "651a19ccd09c1e0f8b25f6a0aac5825b0a20f158ca4e0d78f2abd904a3966b6e3599a47b9ff199a3a6e1152231116fa4639fec684a56909c22cbf6db66613901",
        "fee": 108000000,
        "type": 16386,
        "deadline": 9154726,
        "version": -1744830463,
        "signer": "d99e88c90da71a4b0d848454e59e296c9ef7a8f018f3eaa3a198dc460b6621a4",
        "supplyType": 1,
        "delta": 123,
        "mosaicId": {
        "namespaceId": "alice.vouchers",
        "name": "gift vouchers"
        }
        }
``` 
##### Description of the fields: 

| Parameter | Description |
|------|------|
| timeStamp | The number of seconds elapsed since the creation of the nemesis block. |
| signature | The transaction signature (missing if part of a multisig transaction). |
| fee | The fee for the transaction. The higher the fee, the higher the priority of the transaction. Transactions with high priority get included in a block before transactions with lower priority.  |
| type | The transaction type. |
| deadline | The deadline of the transaction. The deadline is given as the number of seconds elapsed since the creation of the nemesis block. If a transaction does not get included in a block before the deadline is reached, it is deleted.  |
| version | The version of the structure. |
| signer | The public key of the account that created the transaction. |
| supplyType | The supply type. Supported supply types are: 1: Increase in supply. 2: Decrease in supply.  |
| delta | The supply change in units for the mosaic. |
| mosaicId | The mosaic id. See MosaicId for details. |

 
### MultisigAggregateModificationTransaction 
##### Description: 
Multisig aggregate modification transactions are part of the NEM's multisig account system. A multisig aggregate modification transaction holds an array of multisig cosignatory modifications and a single multisig minimum cosignatories modification inside the transaction. A multisig aggregate modification transaction can be wrapped by a multisig transaction. Aggregate modification transactions that use the minCosignatories field need to have version 0x68000002 (decimal 1744830466) for mainnet and 0x98000002 (decimal -1744830462) for testnet. 

 
##### JSON structure by example (main network): 
```json
{
        "timeStamp": 9111526,
        "signature": "651a19ccd09c1e0f8b25f6a0aac5825b0a20f158ca4e0d78f2abd904a3966b6e3599a47b9ff199a3a6e1152231116fa4639fec684a56909c22cbf6db66613901",
        "fee": 3000000,
        "type": 257,
        "deadline": 9154726,
        "version": 1744830466,
        "signer": "a1aaca6c17a24252e674d155713cdf55996ad00175be4af02a20c67b59f9fe8a",
        "modifications": [
        &lt;MultisigCosignatoryModification&gt;,
        &lt;MultisigCosignatoryModification&gt;
        ],
        "minCosignatories" : {
        "relativeChange" : 2
        }
        }
``` 
##### Description of the fields: 

| Parameter | Description |
|------|------|
| timeStamp | The number of seconds elapsed since the creation of the nemesis block. |
| signature | The transaction signature (missing if part of a multisig transaction). |
| fee | The fee for the transaction. The higher the fee, the higher the priority of the transaction. Transactions with high priority get included in a block before transactions with lower priority.  |
| type | The transaction type. |
| deadline | The deadline of the transaction. The deadline is given as the number of seconds elapsed since the creation of the nemesis block. If a transaction does not get included in a block before the deadline is reached, it is deleted.  |
| version | The version of the structure. |
| signer | The public key of the account that created the transaction. |
| modifications | The JSON array of multisig modifications. |
| minCosignatories | JSON object that holds the minimum cosignatories modification. |
| relativeChange | Value indicating the relative change of the minimum cosignatories. |

 
### MultisigCosignatoryModification 
##### Description: 
Multisig cosignatory modifications are part of the NEM's multisig account system. With a multisig cosignatory modification a cosignatory is added to or deleted from a multisig account. Multisig cosignatory modifications are part of a multisig aggregate modification transactions, see details there.

 
##### JSON structure by example: 
```json
{
        "modificationType": 1,
        "cosignatoryAccount": "213150649f51d6e9113316cbec5bf752ef7968c1e823a28f19821e91daf848be"
        }
``` 
##### Description of the fields: 

| Parameter | Description |
|------|------|
| modificationType | The type of modification. Possible values are: 1:  Add a new cosignatory.2:  Delete an existing cosignatory.  |
| cosignatoryAccount | The public key of the cosignatory account as hexadecimal string |

 
### MultisigSignatureTransaction 
##### Description: 
Multisig signature transactions are part of the NEM's multisig account system. Multisig signature transactions are included in the corresponding multisig transaction and are the way a cosignatory of a multisig account can sign a multisig transaction for that account.

 
##### JSON structure by example (test network): 
```json
{
        "timeStamp": 9111526,
        "signature": "651a19ccd09c1e0f8b25f6a0aac5825b0a20f158ca4e0d78f2abd904a3966b6e3599a47b9ff199a3a6e1152231116fa4639fec684a56909c22cbf6db66613901",
        "fee": 3000000,
        "type": 257,
        "deadline": 9154726,
        "version": -1744830463,
        "signer": "a1aaca6c17a24252e674d155713cdf55996ad00175be4af02a20c67b59f9fe8a",
        "otherHash": {
        "data": "44e4968e5aa35fe182d4def5958e23cf941c4bf809364afb4431ebbf6a18c039"
        },
        "otherAccount": "TDGIMREMR5NSRFUOMPI5OOHLDATCABNPC5ID2SVA"
        }
``` 
##### Description of the fields: 

| Parameter | Description |
|------|------|
| timeStamp | The number of seconds elapsed since the creation of the nemesis block. |
| signature | The transaction signature. |
| fee | The fee for the transaction. |
| type | The transaction type. |
| deadline | The deadline of the transaction. The deadline is given as the number of seconds elapsed since the creation of the nemesis block. If a transaction does not get included in a block before the deadline is reached, it is deleted.  |
| version | The version of the structure. |
| signer | The public key of the account that created the transaction. |
| otherHash | The hash of the inner transaction of the corresponding multisig transaction. |
| otherAccount | The address of the corresponding multisig account. |

 
### MultisigTransaction 
##### Description: 
Multisig transaction are the only way to make transaction from a multisig account to another account. A multisig transaction carries another transaction inside (often referred to as "inner" transaction). The inner transaction can be a transfer, an importance transfer or an aggregate modification transaction. A multisig transaction also has multisig signature transactions from the cosignatories of the multisig account inside.

 
##### JSON structure by example (test network): 
```json
{
        "timeStamp": 9111526,
        "signature": "651a19ccd09c1e0f8b25f6a0aac5825b0a20f158ca4e0d78f2abd904a3966b6e3599a47b9ff199a3a6e1152231116fa4639fec684a56909c22cbf6db66613901",
        "fee": 3000000,
        "type": 257,
        "deadline": 9154726,
        "version": -1744830463,
        "signer": "a1aaca6c17a24252e674d155713cdf55996ad00175be4af02a20c67b59f9fe8a",
        "otherTrans": &lt;inner transaction&gt;,
        "signatures":[
        &lt;MultisigSignatureTransaction&gt;,
        &lt;MultisigSignatureTransaction&gt;
        ]
        }
``` 
##### Description of the fields: 

| Parameter | Description |
|------|------|
| timeStamp |  The number of seconds elapsed since the creation of the nemesis block. |
| signature |  The transaction signature. |
| fee |  The fee for the transaction. |
| type |  The transaction type. |
| deadline |  The deadline of the transaction. The deadline is given as the number of seconds elapsed since the creation of the nemesis block. If a transaction does not get included in a block before the deadline is reached, it is deleted.  |
| version |  The version of the structure. |
| signer |  The public key of the account that created the transaction. |
| otherTrans |  The inner transaction. The inner transaction can be a transfer transaction, an importance transfer transaction or a multisig aggregate modification transaction. The inner transaction does not have a valid signature.  |
| signatures |  The JSON array of MulsigSignatureTransaction objects. |

 
### ProvisionNamespaceTransaction 
##### Description: 
Accounts can rent a namespace for one year and after a year renew the contract. This is done via a ProvisionNamespaceTransaction.

 
##### JSON structure by example (test network): 
```json
{
        "timeStamp": 9111526,
        "signature": "651a19ccd09c1e0f8b25f6a0aac5825b0a20f158ca4e0d78f2abd904a3966b6e3599a47b9ff199a3a6e1152231116fa4639fec684a56909c22cbf6db66613901",
        "fee": 108000000,
        "type": 8193,
        "deadline": 9154726,
        "version": -1744830463,
        "signer": "d99e88c90da71a4b0d848454e59e296c9ef7a8f018f3eaa3a198dc460b6621a4",
        "rentalFeeSink": "3e82e1c1e4a75adaa3cba8c101c3cd31d9817a2eb966eb3b511fb2ed45b8e262",
        "rentalFee": 5000000000,
        "newPart": "voucher",
        "parent": "alice"
        }
``` 
##### Description of the fields: 

| Parameter | Description |
|------|------|
| timeStamp | The number of seconds elapsed since the creation of the nemesis block. |
| signature | The transaction signature (missing if part of a multisig transaction). |
| fee | The fee for the transaction. The higher the fee, the higher the priority of the transaction. Transactions with high priority get included in a block before transactions with lower priority.  |
| type | The transaction type. |
| deadline | The deadline of the transaction. The deadline is given as the number of seconds elapsed since the creation of the nemesis block. If a transaction does not get included in a block before the deadline is reached, it is deleted.  |
| version | The version of the structure. |
| signer | The public key of the account that created the transaction. |
| rentalFeeSink | The public key of the account to which the rental fee is transferred. |
| rentalFee | The fee for renting the namespace. |
| newPart | The new part which is concatenated to the parent with a '.' as separator. |
| parent | The parent namespace. This can be null if the transaction rents a root namespace. |

 
### TransferTransaction 
##### Description: 
Transfer transactions contain data about transfers of XEM or mosaics to another account. There are two version of transfer transactions, version 1 and version 2. Version 1 transfer transaction are only capable of transferring XEM and a message while version 2 transfer transactions additionally can transfer a set of mosaics. 

 
##### JSON structure by example (v1 transfer transaction, test network): 
```json
{
        "timeStamp": 9111526,
        "amount": 1000000000,
        "signature": "651a19ccd09c1e0f8b25f6a0aac5825b0a20f158ca4e0d78f2abd904a3966b6e3599a47b9ff199a3a6e1152231116fa4639fec684a56909c22cbf6db66613901",
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
        }
``` 
##### JSON structure by example (v2 transfer transaction, test network): 
```json
{
        "timeStamp": 9111526,
        "amount": 123000000,
        "signature": "fad7ea2b5df5f7846f45fd9983a75ad8d333af3660f4f0d355864420f4482605d675e89d97177385338b226097342b4222add52c5397423f9eaf6b01fe3ef70c",
        "fee": 3000000,
        "recipient": "TBEH27FNRS43FNH3PXE4XN3H7HXA37H77APSZW46",
        "type": 257,
        "deadline": 9154726,
        "message":
        {
        "payload": "74657374207472616e73616374696f6e",
        "type": 1
        },
        "version": -1744830462,
        "signer": "cb4ef3709d25ccd0c022b2d53e4ce31478ebc4bf177b1b54482afb8e55692521",
        "mosaics":[{
        "mosaicId":{
        "namespaceId": "id0",
        "name": "name0"
        },
        "quantity": 10
        },{
        "mosaicId":{
        "namespaceId": "id1",
        "name": "name1"
        },
        "quantity": 11
        }]
        }
``` 
##### Description of the fields: 

| Parameter | Description |
|------|------|
| timeStamp | The number of seconds elapsed since the creation of the nemesis block. |
| amount | The amount of micro NEM that is transferred from sender to recipient. |
| signature | The transaction signature. |
| fee | The fee for the transaction. The higher the fee, the higher the priority of the transaction. Transactions with high priority get included in a block before transactions with lower priority.  |
| recipient | The address of the recipient. |
| type | The transaction type. |
| deadline | The deadline of the transaction. The deadline is given as the number of seconds elapsed since the creation of the nemesis block. If a transaction does not get included in a block before the deadline is reached, it is deleted.  |
| message | Optionally a transaction can contain a message. In this case the transaction contains a message substructure. If not the field is null.  |
| payload |  Optional field in case the transaction contains a message. The payload is the actual (possibly encrypted) message data.  |
| type |  Optional field in case the transaction contains a message. The field holds the message type information. Possible message types are: 1:  The message is not encrypted.2:  The message is encrypted.  |
| version | The version of the structure. |
| signer | The public key of the account that created the transaction. |
| mosaics | The array of Mosaic objects. |

 
