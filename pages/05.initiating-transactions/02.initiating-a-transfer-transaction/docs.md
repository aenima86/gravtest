---
title: Initiating a transfer transaction
taxonomy:
    category: docs
---

 
NIS supports transfer transactions having version 1 or 2. Transfer transactions with version 1 can only transfer a message and XEM coins while version 2 transfer transactions can transfer a set of mosaics too.

 
### Version 1 transfer transactions 
Suppose you want to send 1000 NEM from sender account (referred hereafter as **'Alice'**):

 
TALICELCD3XPH4FFI5STGGNSNSWPOTG5E4DS2TOS

 
to recipient account: 

 
TBOBBSXX7BESJXDWGLP5Z7FM5HSTKUH5WIMPW562

 
The RequestPrepareAnnounce JSON object you have to send to NIS via a POST request would look similar to this (test network):

 
```json

        {
        "transaction":
        {
        "timeStamp": 9111526,
        "amount": 1000000000,
        "fee": 3000000,
        "recipient": "TBOBBSXX7BESJXDWGLP5Z7FM5HSTKUH5WIMPW562",
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
        "privateKey": "00983bb01d05edecfaef55df9486c111abb6299c754a002069b1d0ef4537441bda"
        }
    
``` 
Note that there is no signature in the transaction part of the object since NIS will create the signature for you. Note also that the field 'version' contains both the network version and the transaction version as can be see when converting the value to the hexadecimal system: -1744830463 = 0x98000001 (network version 0x98 and transaction version 0x01). If the sender account has enough funds for the transaction NIS would respond with the JSON object

 
```json
{
        "type": 1,
        "code": 1,
        "message": "SUCCESS",
        "transactionHash": {
        "data":"c1786437336da077cd572a27710c40c378610e8d33880bcb7bdb0a42e3d35586"
        },
        "innerTransactionHash": {}
        }
``` 
### Version 2 transfer transactions 
With transfer transactions version 2 you can just transfer messages and XEM as described in the previous chapter, the only difference being the field version which should have the value -1744830462 = 0x98000002 for testnet or 1744830466 = 0x68000002 for mainnet. 

 
However, version 2 transfer transaction are more powerful as they let you transfer mosaics too. Suppose you already have created a mosaic with id 'makoto.metals.silver * coin' with a divisibility of 0 and you want bundle the transfer of those silver coin mosaics with a transfer of 100 XEM for each silver coin. For transferring 3 silver coin mosaics and 300 XEM with a single transfer transaction you would issue a RequestPrepareAnnounce JSON object to NIS which looks like this:

 
```json

        {
        "transaction":
        {
        "timeStamp": 9111526,
        "amount": 3000000,
        "fee": 30000000,
        "recipient": "TBOBBSXX7BESJXDWGLP5Z7FM5HSTKUH5WIMPW562",
        "type": 257,
        "deadline": 9154726,
        "message":
        {
        "payload": "",
        "type": 1
        },
        "version": -1744830462,
        "signer": "a1aaca6c17a24252e674d155713cdf55996ad00175be4af02a20c67b59f9fe8a"
        "mosaics":[{
        "mosaicId":{
        "namespaceId": "makoto.metals.silver",
        "name": "coin"
        },
        "quantity": 1
        },{
        "mosaicId":{
        "namespaceId": "nem",
        "name": "xem"
        },
        "quantity": 100000000
        }]
        },
        "privateKey": "00983bb01d05edecfaef55df9486c111abb6299c754a002069b1d0ef4537441bda"
        }
    
``` 
There are 2 mosaics attached to the transfer transaction:
* A mosaic with id 'makoto.metals.silver * coin' and quantity 1 which represents 1 smallest unit available for the mosaic. Since the divisibility of that mosaic is 0 (as assumed above) the quantity represents 1 whole unit, i.e. 1 coin.
* A mosaic with id 'nem * xem' (which is the special XEM mosaic representing regular XEM coins) which has a divisibility of 6 and thus the quantity of 100000000 represents 100 XEM. You can view the attachment as being a bag of mosaics holding in this example 1 silver coin mosaic and 100 XEM. 

 
The amount field of the transaction is interpreted differently for the transaction due to the attachment. The number to multiply the quantities given in the attachment is given by dividing the amount by 1,000,000 (as of this version NIS does not support fractional transfers). So in this example 3,000,000 / 1,000,000 = 3 and thus 3 times the attachment is transferred resulting in 3 silver coin mosaics and 300 XEM being transferred to the recipient.

 
Common reason for the transaction to be rejected could be:
* At least one mosaic specified in the attachment is unknown to NIS.
* The sender does not own enough mosaics of at least type specified in the attachment.
* At least one mosaic specified in the attachment is defined as not transferable and both sender and recipient are not the creator of that mosaic. 

 
If the mosaic definition for the mosaic 'makoto.metals.silver * coin' has a levy section stating that for each transfer involving the silver coin mosaic 10 XEM has to be paid to the recipient with address TDGOGOGOWZJ3HU4F6CUM5IKE7GHG4FFTF5BZ7JPW then the transfer transaction would automatically induce a transfer of 10 XEM from the transaction sender to TDGOGOGOWZJ3HU4F6CUM5IKE7GHG4FFTF5BZ7JPW.

 
