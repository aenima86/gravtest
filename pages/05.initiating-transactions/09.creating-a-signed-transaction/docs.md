---
title: Creating a signed transaction
taxonomy:
    category: docs
---

 
This chapter explains which data from the transactions you need to sign and what JSON object you to send to NIS.

 
### Gathering data for the signature 
To create a transaction signature you need to sign an array of bytes extracted from the transaction. Since there is more than one type of transaction the byte array will have a different structure for different types of transactions. Nevertheless the first part of the byte array has the same structure for every transaction. Note that:

 


 
 For transfer transactions and multisig aggregate modification transactions the version must be 

 
**Note:** the following part is optional and only available for version 2 transfer transactions that have an attachment.

 
The following part is repeated for every mosaic in the attachment.

 
The following part is repeated for every cosignatory modification

 
The following part describes the minimum cosignatories modification. The part is optional. Version 1 aggregate modification transactions should omit this part. Version 2 aggregate modification transactions with no minimum cosignatories modification should only write the length field with value 0x00, 0x00, 0x00, 0x00.

 
What follows here is the inner transaction object. The structure is one of the structures described above transactions (excluding signature transactions).

 
The following 5 fields are repeated for every property. **Note:** The property values are always strings

 
**Note:** The following levy object is optional. Set length field to 0 if the mosaic definition has no levy and omit all subsequent fields up to the comment "The levy structure ends here.".

 
The levy structure ends here.

 
To build the final byte array that needs to be signed, simply concatenate the common part for a transaction and the type specific part. For example if you want to build the byte array for a transfer transaction you have as common something that looks like

 
0x01, 0x01, 0x00, 0x00, 0x01, 0x00, 0x00, 0x00, 0x6f, 0x00, 0x00, 0x00, 0x20, 0x00, 0x00, 0x00, 0x68, 0x32, 0x03, 0xb4, 0x55, 0x09, 0x0e, 0x2f, 0xfe, 0xd6, 0x48, 0x53, 0x6c, 0x99, 0x01, 0x4d, 0x1c, 0xa9, 0x2c, 0x10, 0x47, 0xaf, 0xbc, 0xae, 0x58, 0x05, 0x7b, 0xb6, 0xa6, 0x98, 0xc8, 0x0b, 0x80, 0x84, 0x1e, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00

 
and a transfer transaction specific part

 
0x28, 0x00, 0x00, 0x00, 0x54, 0x41, 0x49, 0x34, 0x35, 0x32, 0x53, 0x37, 0x44, 0x4c, 0x36, 0x57, 0x48, 0x57, 0x54, 0x5a, 0x5a, 0x32, 0x57, 0x33, 0x44, 0x49, 0x4d, 0x34, 0x32, 0x36, 0x58, 0x57, 0x49, 0x4a, 0x4b, 0x4c, 0x55, 0x4e, 0x58, 0x4e, 0x4b, 0x54, 0x37, 0x4c, 0x40, 0x2f, 0x07, 0x2f, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00

 
which gives you the final array

 
0x01, 0x01, 0x00, 0x00, 0x01, 0x00, 0x00, 0x00, 0x6f, 0x00, 0x00, 0x00, 0x20, 0x00, 0x00, 0x00, 0x68, 0x32, 0x03, 0xb4, 0x55, 0x09, 0x0e, 0x2f, 0xfe, 0xd6, 0x48, 0x53, 0x6c, 0x99, 0x01, 0x4d, 0x1c, 0xa9, 0x2c, 0x10, 0x47, 0xaf, 0xbc, 0xae, 0x58, 0x05, 0x7b, 0xb6, 0xa6, 0x98, 0xc8, 0x0b, 0x80, 0x84, 0x1e, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00 0x28, 0x00, 0x00, 0x00, 0x54, 0x41, 0x49, 0x34, 0x35, 0x32, 0x53, 0x37, 0x44, 0x4c, 0x36, 0x57, 0x48, 0x57, 0x54, 0x5a, 0x5a, 0x32, 0x57, 0x33, 0x44, 0x49, 0x4d, 0x34, 0x32, 0x36, 0x58, 0x57, 0x49, 0x4a, 0x4b, 0x4c, 0x55, 0x4e, 0x58, 0x4e, 0x4b, 0x54, 0x37, 0x4c, 0x40, 0x2f, 0x07, 0x2f, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00

 
Signing this array will give you the 64 byte long signature.

 
NIS uses the SHA3-256 hash function. To create a hash of a transaction you need to hash the byte array of the transaction. See the section above to learn how to build the byte array from a transaction.

 
### Sending the data to NIS 
After preparing the data as described in the last section you can send the array and the corresponding signature via a RequestAnnounce request

 
| API path: | Request type:  |
|------|------|
| /transaction/announce | POST|

 
##### Description: 
Creates and broadcasts a transaction. The private key is not involved.

 
##### Parameter: 

| Parameter | Description |
|------|------|
|  requestAnnounce   |  A RequestAnnounce JSON object as described in Appendix A: RequestAnnounce .    |

 
##### Example: 
Request cannot be performed in a browser.

 
##### Example of returned JSON NemAnnounceResult object: 
```json
{
        "type":1,
        "code":1,
        "message":"SUCCESS",
        "transactionHash": {
        "data":"c1786437336da077cd572a27710c40c378610e8d33880bcb7bdb0a42e3d35586"
        },
        "innerTransactionHash": {
        "data":"cc317a7674d56352b4c711096a7594bd11908bf518293a191fc2faa12eac0fbb"
        }
        }
``` 
##### Possible Errors: 
The possible erros are described in chapter 6.1.

 
