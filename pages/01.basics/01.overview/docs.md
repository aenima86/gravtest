
# **4. Account related requests**

TEST

This chapter will guide you through the process of retrieving account information from a NEM Infrastructure Server. The information that can be retrieved is the durable account data, its meta data and information about transactions and harvested blocks.

 
NIS supports two different kind of accounts: normal accounts and multsig (short for: multi signature) accounts:

 
##### Normal accounts: 
Normal accounts are created and controlled by a private key. Any action for the account like sending NEM to another account via a transfer transaction is signed with this private key. If an attacker gains knowledge of the private key, he/she can rob the account. The private key must therefore be kept secret by all means.

 
##### Multisig accounts: 
Multisig accounts can be created by converting a normal account to a multisig account via a **aggregate modification transaction**. This adds cosignatories to the account. After that modification, only the cosignatories can initiate an action for the account. Any action must be signed by all cosignatories. This makes a multisig account significantly more secure than a normal account. When a single cosignatory private key is gained by an attacker, the attacker still can't initiate any action on the account since **all** cosignatories must sign. It is strongly recommended to convert any account holding a significantly high amount of NEM into a multisig account with at least 3 cosignatories. Once converted to a multisig account, the original private key for the account plays no role any more.

 
Durable data is either stored in the database or can be calculated from other database data. The corresponding JSON object is described in Appendix A: AccountInfo . It has the fields: 

 

| Parameter | Description |
|------|------|
|  address   |  Each account has a unique address. First letter of an address indicate the network the account belongs to. Currently two networks are defined: the test network whose account addresses start with a capital **T** and the main network whose account addresses always start with a capital **N**. Addresses have always a length of 40 characters and are base-32 encoded.   |
|  balance   |  Each account has a balance which is an integer greater or equal to zero and denotes the number of **micro** NEMs which the account owns. Thus a balance of 123456789 means the account owns 123.456789 NEM. A balance is split into its vested and unvested part. Only the vested part is relevant for the importance calculation. For transfers from one account to another only the balance itself is relevant.   |
|  importance   |  Each account is assigned an importance. The importance is a decimal number between 0 and 1. It denotes the probability of an account to harvest the next block in case the account has harvesting turned on and all other accounts are harvesting too. The exact formula for calculating the importance is not public yet. Accounts need at least 10k **vested** NEM to be included in the importance calculation.   |
|  publicKey   |  The public key of an account can be used to verify signatures of the account. Only accounts that have already published a transaction have a public key assigned to the account. Otherwise the field is null.   |
|  label   |  This field is not used yet and is always null.   |
|  harvestedBlocks   |  Harvesting is the process of generating new blocks. The field denotes the number of blocks that the account harvested so far. For a new account the number is 0.   |

 
The meta data for an account describes the harvesting status of an account, and in case that the account is a cosignatory of at least one multisig account, the list of those multisig accounts. An account can either harvest with its current importance or delegate the harvesting to a so called remote account. In the latter case the remote account uses the importance of the original account to harvest. The corresponding JSON object and the possible values for the status/remoteStatus are described in Appendix A: AccountMetaDataPair . The meta data consists of the following fields: 

 

| Parameter | Description |
|------|------|
|  status   |  This field describes the harvesting status of an account.   |
|  remoteStatus   |  The field describes the status of remote harvesting.   |
|  cosignatoryOf   |  Array of AccountInfo structures that describe the multisig accounts that this account is cosignatory of.   |

 
Known accounts have at least one incoming transaction. The corresponding JSON objects are described in Appendix A: Transaction , TransactionMetaData and TransactionMetaDataPair . 

 
A transaction has always the following fields:

 

| Parameter | Description |
|------|------|
|  timeStamp   |  The number of seconds elapsed since the creation of the nemesis block. Future timestamps are not allowed. Transaction validation detects future timestamps and returns an error in that case. Network time synchronization ensures that any NEM software component will use valid timestamps when creating transactions.   |
|  signature   |  The transaction signature. The transaction signature is validated using the supplied public key in the field signer. If the signature is not valid, an error is returned from validation.   |
|  fee   |  The fee for the transaction. The higher the fee, the higher is the priority of the transaction. Transactions with high priority get included in a block before transactions with lower priority. If the sender does not have enough funds the validation will result in an error   |
|  type   |  The transaction type. Currently the following types of transactions are supported: 0x101:  Transfer of NEM from sender to recipient.0x801:  Transfer of importance from sender to remote account.0x1001:  An aggregate modification transaction, which converts a normal account into a multisig account.0x1002:  A multisig signature transaction which is used to sign a multisig transaction.0x1003:  A multisig transaction, which is used for multisig accounts.   |
|  deadline   |  The deadline of the transaction. The deadline is given as the number of seconds elapsed since the creation of the nemesis block. If a transaction does not get included in a block before the deadline is reached, it is deleted.   |
|  version   |  The version of the structure. The following version are currently support. 0x68 &lt;&lt; 24 + 1 (1744830465 as 4 byte integer): the main network version 0x98 &lt;&lt; 24 + 1 (-1744830463 as 4 byte integer): the test network version   |
|  signer   |  The public key of the account that created the transaction. The public key is encoded as hexadecimal string.   |

 
Depending on the type of the transaction, there are additional fields which are specific to given type. For instance a transfer transaction will have the additional fields.

 

| Parameter | Description |
|------|------|
|  recipient   |  The address of the recipient. If the address is not valid an error is returned from validation.   |
|  message   |  Optionally a transfer transaction can contain a message.   |
|  payload   |  Optional field in case the transaction contains a message. The payload is the actual (possibly encrypted) message data. The payload is allowed to have a maximal size of 512 bytes. Transaction validation detects if the limit is exceeded and returns an error in this case.   |
|  type   |  Optional field in case the transaction contains a message. The field holds the message type information. Possible message types are: 1:  The message is not encrypted.2:  The message is encrypted.   |

 
Please refer to Appendix A for detailed information on the various transactions types and their additional fields.

 
Transaction meta data contains only following field:

 

| Parameter | Description |
|------|------|
|  height   |  The height of the block in which the transaction was included.   |
|  id   |  The id of the transaction.   |
|  hash   |  The hash of the transaction.   |

 


 
Accounts can harvest (i.e. generate new) blocks if they are lucky. The account which harvests a block collects the fees which are included in the transactions in the block. The information which blocks were harvested by an account can be requested. The request returns an array of HarvestInfo JSON objects. For an example see Appendix A: HarvestInfo 

 
A harvest info object has the following fields:

 

| Parameter | Description |
|------|------|
|  timeStamp   |  The number of seconds elapsed since the creation of the nemesis block.   |
|  id   |  The database id for the block.   |
|  difficulty   |  The block difficulty.   |
|  totalFee   |  The total fee collected by harvesting the block.   |
|  height   |  The height of the harvested block.   |

 


 
It is possible to request an array with the importance information for all accounts. The request returns an array of AccountImportanceViewModel JSON objects. For an example see Appendix A: AccountImportanceViewModel . 

 
An account importance view model has the following fields:

 

| Parameter | Description |
|------|------|
|  address   |  The address of the account.   |
|  importance   |  Substructure that describes the importance of the account.   |
|  isSet   |  Indicates if the fields "score", "ev" and "height" are available. isSet can have the values 0 or 1. In case isSet is 0 the following fields are not available.   |
|  score   |  The importance of the account. The importance ranges between 0 and 1.   |
|  ev   |  The page rank portion of the importance. The page rank ranges between 0 and 1.   |
|  height   |  The height at which the importance calculation was performed.   |

 
## **4.3. Retrieving account data**
--- 
### 4.3.1 Generating new account data 
| API path: | Request type:  |
|------|------|
| /account/generate | GET|

 
##### Description: 
Generates a KeyPairViewModel.

 
##### No Parameter: 
##### Example: 
http://127.0.0.1:7890/account/generate

 
##### Example of returned JSON object: 

```json
{
        "privateKey": "0962c6505d02123c40e858ff8ef21e2b7b5466be12c4770e3bf557aae828390f",
        "address": "NCKMNCU3STBWBR7E3XD2LR7WSIXF5IVJIDBHBZQT",
        "publicKey": "c2e19751291d01140e62ece9ee3923120766c6302e1099b04014fe1009bc89d3"
        }
``` 
##### Possible Errors: 
None.

 
### 4.3.2 Requesting the account data 
| API path: | Request type:  |
|------|------|
| /account/get | GET|

 
##### Description: 
Gets an AccountMetaDataPair for an account.

 
##### Parameter: 

| Parameter | Description |
|------|------|
|  address   |  The address of the account.   |

 
##### Example: 
http://127.0.0.1:7890/account/get?address=TALICELCD3XPH4FFI5STGGNSNSWPOTG5E4DS2TOS 

 
##### Example of returned JSON object: 
```json
{
        "account":
        {
        "address": "TALICELCD3XPH4FFI5STGGNSNSWPOTG5E4DS2TOS",
        "balance": 124446551689680,
        "vestedBalance": 104443451691625,
        "importance": 0.010263666447108395,
        "publicKey": "a11a1a6c17a24252e674d151713cdf51991ad101751e4af02a20c61b59f1fe1a",
        "label": null,
        "harvestedBlocks": 645
        },
        "meta":
        {
        "cosignatoryOf": [ ],
        "cosignatories": [ ],
        "status": "LOCKED",
        "remoteStatus": "ACTIVE"
        }
        }
``` 
##### Possible Errors: 
If the address parameter is not valid, NIS returns an error. See Appendix B: NIS Errors for details about errors. 

 


 
Alternatively you can retrieve the account data by providing the public key for the account:

 
| API path: | Request type:  |
|------|------|
| /account/get/from-public-key | GET|

 
##### Parameter: 

| Parameter | Description |
|------|------|
|  publicKey   |  The public key of the account as hex string.   |

 
##### Example: 
http://127.0.0.1:7890/account/get/from-public-key?publicKey=f9bd190dd0c364261f5c8a74870cc7f7374e631352293c62ecc437657e5de2cd 

 
The returned JSON object has the same structure as in the first example.

 
##### Possible Errors: 
If the public key parameter is not valid, NIS returns an error. See Appendix B: NIS Errors for details about errors. 

 
### 4.3.3 Requesting the original account data for a delegate account 
| API path: | Request type:  |
|------|------|
| /account/get/forwarded | GET|

 
##### Description: 
Given a delegate (formerly known as remote) account's address, gets the AccountMetaDataPair for the account for which the given account is the delegate account. If the given account address is not a delegate account for any account, the request returns the AccountMetaDataPair for the given address.

 
##### Parameter: 

| Parameter | Description |
|------|------|
|  address   |  The address of the delegate account.   |

 
##### Example: 
http://127.0.0.1:7890/account/get/forwarded?address=NC2ZQKEFQIL3JZEOB2OZPWXWPOR6LKYHIROCR7PK 

 
##### Example of returned JSON object: 
```json
{
        "account":
        {
        "address": "NALICE2A73DLYTP4365GNFCURAUP3XVBFO7YNYOW",
        "balance": 11793338398661,
        "vestedBalance": 10890953464862,
        "importance": 0.001264596432148395,
        "publicKey": "bdd8dd702acb3d88daf188be8d6d9c54b3a29a32561a068b25d2261b2b2b7f02",
        "label": null,
        "harvestedBlocks": 742
        },
        "meta":
        {
        "cosignatoryOf": [ ],
        "cosignatories": [ ],
        "status": "LOCKED",
        "remoteStatus": "ACTIVE"
        }
        }
``` 
##### Possible Errors: 
If the address parameter is not valid, NIS returns an error. See Appendix B: NIS Errors for details about errors. 

 


 
Alternatively you can retrieve the original account data by providing the public key of the delegate account:

 
| API path: | Request type:  |
|------|------|
| /account/get/forwarded/from-public-key | GET|

 
##### Parameter: 

| Parameter | Description |
|------|------|
|  publicKey   |  The public key of the account as hex string.   |

 
##### Example: 
http://127.0.0.1:7890/account/get/forwarded/from-public-key?publicKey=bdd8dd702acb3d88daf188be8d6d9c54b3a29a32561a068b25d2261b2b2b7f02 

 
The returned JSON object has the same structure as in the first example.

 
##### Possible Errors: 
If the public key parameter is not valid, NIS returns an error. See Appendix B: NIS Errors for details about errors. 

 
### 4.3.4 Requesting the account status 
| API path: | Request type:  |
|------|------|
| /account/status | GET|

 
##### Description: 
Gets the AccountMetaData from an account.

 
##### Parameter: 

| Parameter | Description |
|------|------|
|  Address   |  The address of the account.   |

 
##### Example: 
http://127.0.0.1:7890/account/status?address=TALICELCD3XPH4FFI5STGGNSNSWPOTG5E4DS2TOS 

 
##### Example of returned JSON object: 
```json
{
        "cosignatoryOf": [ ],
        "status": "LOCKED",
        "remoteStatus": "ACTIVE"
        }
``` 
##### Possible Errors: 
If the address parameter is not valid, NIS returns an error. See Appendix B: NIS Errors for details about errors. 

 
### 4.3.5 Requesting transaction data for an account 
A transaction is said to be incoming with respect to an account if the account is the recipient of the transaction. In the same way outgoing transaction are the transactions where the account is the sender of the transaction. Unconfirmed transactions are those transactions that have not yet been included in a block. Unconfirmed transactions are **not** guaranteed to be included in any block.

 
##### Incoming transactions 
| API path: | Request type:  |
|------|------|
| /account/transfers/incoming | GET|

 
##### Description: 
Gets an array of TransactionMetaDataPair objects where the recipient has the address given as parameter to the request. A maximum of 25 transaction meta data pairs is returned. The returned transaction meta data pairs are sorted in descending order in which they were written to the database.

 
 The second parameter is optional. When it's not present, the request will return newest transactions according to the above criteria. When hash is supplied as second parameter, the request will return up to 25 transactions that appeared directly before the transaction that has the supplied hash sorted according to the above criteria.

 
The third parameter is optional. When an id is supplied as third parameter, the request will return up to 25 transactions that appeared directly before the transaction that has the supplied id sorted according to the above criteria.

 
If less than 25 transactions fulfill the requirements, only those transactions are returned.

 


 
##### Parameters: 

| Parameter | Description |
|------|------|
|  address  |  The address of the account.   |
|  hash   |  The 256 bit sha3 hash of the transaction up to which transactions are returned.   |
|  id    |  The transaction id up to which transactions are returned.   |

 
#####  
##### Example: 
 http://127.0.0.1:7890/account/transfers/incoming?address=TALICELCD3XPH4FFI5STGGNSNSWPOTG5E4DS2TOS&amp;hash=949583a20ebdfdcb58277eb42fef3e66e9e6bbfc47304d8741a82c68f7c53a2 

 
##### Example of returned JSON object (test network): 
```json
{
        "data": [
        {
        "meta":
        {
        "id": 71245,
        "height": 40706,
        "hash": {
        "data":"15c373ad4c3fe6af47d1941379ff262f785bdcfa07c02ac3608bc10da27d5e82"
        }
        },
        "transaction":
        {
        "timeStamp": 9106400,
        "amount": 1000000000,
        "signature": "449cd76ea8bda2220b3d6ad6f8db5f81d4e68ad3d4b0c3db9a3c267355657639eabed3dbcef8e0cc22953ae2b36a22ee7dc6327484c9649cccd686a511eca105",
        "fee": 3000000,
        "recipient": "TALICELCD3XPH4FFI5STGGNSNSWPOTG5E4DS2TOS",
        "type": 257,
        "deadline": 9149600,
        "message":
        {
        "payload": "280000005444334b32493543524850595634425a5a5a4c335850454e4",
        "type": 2
        },
        "version": -1744830463,
        "signer": "c20a1dffe699c7a68328986273265e33fceebe074f274240ef890dd80ad55ed6"
        }
        },
        {
        "meta":
        {
        "id": 71356,
        "height": 40629,
        "hash": {
        "data":"37c34ead4c3fe6af42d994135798262f785ba2d807c02ac3608bc10da12e5f87"
        }
        },
        "transaction":
        {
        "timeStamp": 9101541,
        "amount": 49997995000000,
        "signature": "57c3c48d2ae8b24240b57d72493f498cfeb61e2ab87237dc0e08c51007d5c7f15847d0e08c0286e68a72028925db5fa809ca9d57e2cb6eebe11822176a834c0b",
        "fee": 2005000000,
        "recipient": "TALICELCD3XPH4FFI5STGGNSNSWPOTG5E4DS2TOS",
        "type": 257,
        "deadline": 9144741,
        "message":
        {
        "payload": "526f6262657279212121",
        "type": 1
        },
        "version": -1744830463,
        "signer": "546e4fb9c81db84e04d8e9e67380db0fe1f540df09a527fb995b589b5695ae24"
        }
        }]
        }
``` 
##### Possible Errors: 
If the address parameter is not valid or the id cannot be found in the database, NIS returns an error. See Appendix B: NIS Errors for details about errors. 

 
##### Outgoing transactions 
| API path: | Request type:  |
|------|------|
| /account/transfers/outgoing | GET|

 
##### Description: 
Gets an array of transaction meta data pairs where the recipient has the address given as parameter to the request. A maximum of 25 transaction meta data pairs is returned. For details about sorting and discussion of the second parameter see Incoming transactions.

 
##### Parameters: 

| Parameter | Description |
|------|------|
|  address   |  The address of the account.   |
|  hash   |  The 256 bit sha3 hash of the transaction up to which transactions are returned.   |
|  id    |  The transaction id up to which transactions are returned.   |

 
#####  
##### Example: 
http://127.0.0.1:7890/account/transfers/outgoing?address=TALICELCD3XPH4FFI5STGGNSNSWPOTG5E4DS2TOS&amp;hash=949583a20ebdfdcb58277eb42fef3e66e9e6bbfc47304d8741a82c68f7c53a22 

 
##### Example of returned JSON object (test network): 
```json
{
        "data": [
        {
        "meta":
        {
        "id": 70498,
        "height": 40803,
        "hash": {
        "data":"37c34ead4c3fe6af42d994135798262f785ba2d807c02ac3608bc10da12e5f87"
        }
        },
        "transaction":
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
        }]
        }
``` 
##### Possible Errors: 
If the address parameter is not valid or the id cannot be found in the database, NIS returns an error. See Appendix B: NIS Errors for details about errors. 

 
##### All transactions 
| API path: | Request type:  |
|------|------|
| /account/transfers/all | GET|

 
##### Description: 
Gets an array of transaction meta data pairs for which an account is the sender or receiver. A maximum of 25 transaction meta data pairs is returned. For details about sorting and discussion of the second parameter see Incoming transactions.

 
##### Parameters: 

| Parameter | Description |
|------|------|
|  address   |  The address of the account.   |
|  hash   |  The 256 bit sha3 hash of the transaction up to which transactions are returned.   |
|  id    |  The transaction id up to which transactions are returned.   |

 
#####  
##### Example: 
 http://127.0.0.1:7890/account/transfers/all?address=TALICELCD3XPH4FFI5STGGNSNSWPOTG5E4DS2TOS&amp;hash=949583a20ebdfdcb58277eb42fef3e66e9e6bbfc47304d8741a82c68f7c53a22 

 
##### Example of returned JSON object: 
See example for Incoming transactions or Outgoing transactions.

 
##### Possible Errors: 
If the address parameter is not valid or the id cannot be found in the database, NIS returns an error. See Appendix B: NIS Errors for details about errors. 

 
##### Unconfirmed transactions 
| API path: | Request type:  |
|------|------|
| /account/unconfirmedTransactions | GET|

 
##### Description: 
Gets the array of transactions for which an account is the sender or receiver and which have not yet been included in a block. The returned structure is UnconfirmedTransactionMetaDataPair see Appendix A: UnconfirmedTransactionMetaDataPair 

 
##### Parameters: 

| Parameter | Description |
|------|------|
|  address   |  The address of the account.   |

 
##### Example: 
http://127.0.0.1:7890/account/unconfirmedTransactions?address=TALICELCD3XPH4FFI5STGGNSNSWPOTG5E4DS2TOS 

 
##### Example of returned JSON object (test network): 
```json
{
        "meta": {
        "data": "d7c9e33421e43bf4a5d6e21304c8096c599142755d581bd6e9037f41545a5873"
        },
        "data": [
        {
        "timeStamp": 9131839,
        "amount": 1000000000,
        "signature": "0acface77696a54340a7da8592750ea0410f62717d07e4df30e09718092521262465df5c4d98d32cd9d6e8699d66e016ec8db716d20090ad99cc16f7a6d13904",
        "fee": 2000000,
        "recipient": "TDGIMREMR5NSRFUOMPI5OOHLDATCABNPC5ID2SVA",
        "type": 257,
        "deadline": 9175039,
        "message": {
        "payload": "",
        "type": 1
        },
        "version": -1744830463,
        "signer": "a1aaca6c17a24252e674d155713cdf55996ad00175be4af02a20c67b59f9fe8a"
        }]
        }
``` 
##### Possible Errors: 
If the address parameter is not valid, NIS returns an error. See Appendix B: NIS Errors Errors for details about errors. 

 
### 4.3.6 Transaction data with decoded messages 
All the requests for retrieving transaction data for an account which were described in previous part do not decode any message contained in a transaction. The following requests are similar to the ones above but are able to return transaction data with decoded messages. Decoding requires the private key of an account for which transactions are requested. Therefore the following requests **should only be done when NIS is running locally**.

 
##### Incoming/outgoing/all transactions with decoded messages 
| API path: | Request type:  |
|------|------|
| /local/account/transfers/incoming | POST|

 
| API path: | Request type:  |
|------|------|
| /local/account/transfers/outgoing | POST|

 
| API path: | Request type:  |
|------|------|
| /local/account/transfers/all | POST|

 
##### Description: 
The request returns incoming/outgoing/all transactions as described in the previous chapter. The only difference is that if a transaction contains an encoded message, this message will be decoded before it is sent to the requester.

 
##### Parameters: 

| Parameter | Description |
|------|------|
|  page   |  An AccountPrivateKeyTransactionsPage JSON object as described in Appendix A: AccountPrivateKeyTransactionsPage    |

 
##### Example: 
Request cannot be performed in a browser.

 
##### Example of returned JSON object: 
See section: Requesting transaction data for an account

 
##### Possible Errors: 
If the private key is not supplied, NIS returns an error. See Appendix B: NIS Errors for details about errors. 

 
### 4.3.7 Requesting harvest info data for an account 
| API path: | Request type:  |
|------|------|
| /account/harvests | GET|

 
##### Description: 
Gets an array of harvest info objects for an account.

 
##### Parameter: 

| Parameter | Description |
|------|------|
|  address   |  The address of the account.   |
|  hash    |  The 256 bit sha3 hash of the block up to which harvested blocks are returned.   |

 
##### Example: 
 http://127.0.0.1:7890/account/harvests?address=TALICELCD3XPH4FFI5STGGNSNSWPOTG5E4DS2TOS&amp;hash=81d52a7df4abba8bb1613bcc42b6b93cf3114524939035d88ae8e864cd2c34c8 

 
##### Example of returned JSON object: 
```json
{
        "data": [{
        "timeStamp": 8879051,
        "blockHash": {
        "data": "be3bb308ce33625f0dab64fd31b9ebe1c50dd4b94b43b03c228f481ab82458c3"
        },
        "totalFee": 102585065,
        "height": 37015
        }]
        }
``` 
##### Possible Errors: 
If the address parameter is not valid or the hash cannot be found in the database, NIS returns an error. See Appendix B: NIS Errors Errors for details about errors. 

 
### 4.3.8 Retrieving account importances for accounts 
| API path: | Request type:  |
|------|------|
| /account/importances | GET|

 
##### Description: 
Gets an array of account importance view model objects.

 
##### No parameter: 
##### Example: 
http://127.0.0.1:7890/account/importances

 
##### Example of returned JSON object: 
```json
{
        "data": [{
        "address": "TCYGT6GHZPNASMAXV7YCFCU5R5XTJKNNT66R4A4T",
        "importance": {
        "isSet": 0
        }
        },
        {
        "address": "TD2JJJVPKDZFXWK3N3ZJLN7A5TGNOTM3J5EVSTIG",
        "importance": {
        "score": 0.001222376902598832,
        "ev": 0.004252356221747241,
        "isSet": 1,
        "height": 40926
        }
        }]
        }
``` 
##### Possible Errors: 
None.

 
### 4.3.9 Retrieving namespaces that an account owns 
| API path: | Request type:  |
|------|------|
| /account/namespace/page | GET|

 
##### Description: 
Gets an array of namespace objects for a given account address. The parent parameter is optional. If supplied, only sub-namespaces of the parent namespace are returned.

 
##### Parameter: 

| Parameter | Description |
|------|------|
|  address   |  The address of the account.   |
|  parent   |  The optional parent namespace id.   |
|  id   |  The optional namespace database id up to which namespaces are returned.   |
|  pageSize   |  The (optional) number of namespaces to be returned.   |

 
##### Example: 
http://127.0.0.1:7890/account/namespace/page?address=TD3RXTHBLK6J3UD2BH2PXSOFLPWZOTR34WCG4HXH&amp;parent=makoto.metal 

 
##### Example of returned JSON object: 
```json
{
        "data": [{
        "fqn": "makoto.metal.coins",
        "owner": TD3RXTHBLK6J3UD2BH2PXSOFLPWZOTR34WCG4HXH",
        "height": 13465
        }]
        }
``` 
##### Possible Errors: 
NIS returns an error if the address or the parent (if supplied) is invalid. See Appendix B: NIS Errors for details about errors. 

 
### 4.3.10 Retrieving mosaic definitions that an account has created 
| API path: | Request type:  |
|------|------|
| /account/mosaic/definition/page | GET|

 
##### Description: 
Gets an array of mosaic definition objects for a given account address. The parent parameter is optional. If supplied, only mosaic definitions for the given parent namespace are returned. The id parameter is optional and allows retrieving mosaic definitions in batches of 25 mosaic definitions. For more information how to use the id see Incoming transactions. 

 
##### Parameter: 

| Parameter | Description |
|------|------|
|  address   |  The address of the account.   |
|  parent   |  The optional parent namespace id.   |
|  id   |  The optional mosaic definition database id up to which mosaic definitions are returned.   |

 
##### Example: 
http://127.0.0.1:7890/account/mosaic/definition/page?address=TD3RXTHBLK6J3UD2BH2PXSOFLPWZOTR34WCG4HXH&amp;parent=makoto.metal.coins 

 
##### Example of returned JSON object: 
```json
{
        "data": [{
        "creator": "10cfe522fe23c015b8ab24ef6a0c32c5de78eb55b2152ed07b6a092121187100",
        "id": {
        "namespaceId": "makoto.metal.coins",
        "name": "silver coin"
        },
        "description": "Real silver coins, pure silver",
        "properties": [{
        "name": "divisibility",
        "value": "0"
        },{
        "name": "initialSupply",
        "value": "1000"
        },{
        "name": "supplyMutable",
        "value": "false"
        },{
        "name": "transferable",
        "value": "true"
        }]
        }]
        }
``` 
##### Possible Errors: 
NIS returns an error if the address, the parent (if supplied) or the id (if supplied) is invalid. See Appendix B: NIS Errors for details about errors. 

 
### 4.3.11 Retrieving mosaics that an account owns 
| API path: | Request type:  |
|------|------|
| /account/mosaic/owned | GET|

 
##### Description: 
Gets an array of mosaic objects for a given account address.

 
##### Parameter: 

| Parameter | Description |
|------|------|
|  address   |  The address of the account.   |

 
##### Example: 
http://127.0.0.1:7890/account/mosaic/owned?address=TD3RXTHBLK6J3UD2BH2PXSOFLPWZOTR34WCG4HXH 

 
##### Example of returned JSON object: 
```json
{
        "data": [{
        "mosaicId": {
        "namespaceId": "alice.drinks",
        "name": "orange juice"
        },
        "quantity": 123
        },{
        "mosaicId": {
        "namespaceId": "makoto.metal.coins",
        "name": "silver coin"
        },
        "quantity": 8
        }]
        }
``` 
##### Possible Errors: 
NIS returns an error if the address is invalid. See Appendix B: NIS Errors for details about errors. 

 
### 4.3.12 Locking and unlocking accounts 
Accounts that have at least 10000 vested NEM balance are allowed to harvest blocks. To do that the account must be unlocked. After start-up of NIS all accounts are locked by default.

 
##### Unlocking the account (enables harvesting) 
| API path: | Request type:  |
|------|------|
| /account/unlock | POST|

 
##### Description: 
Unlocks an account (starts harvesting).

 
##### Parameter: 

| Parameter | Description |
|------|------|
|  **privateKey**   |  A PrivateKey JSON object as described in Appendix A: PrivateKey    |

 
##### Example: 
Request cannot be performed in a browser.

 
##### No return value 
##### Locking the account (stops harvesting) 
| API path: | Request type:  |
|------|------|
| /account/lock | POST|

 
##### Description: 
Locks an account (stops harvesting).

 
##### Parameter: 

| Parameter | Description |
|------|------|
|  **privateKey**   |  A PrivateKey JSON object as described in Appendix A: PrivateKey    |

 
##### Example: 
Request cannot be performed in a browser.

 
##### No return value 
##### Possible Errors: 
Both requests return an error if the private key does not correspond to a known account or the account is not allowed to harvest. See Appendix B: NIS Errors for details about errors. 

 
### 4.3.13 Retrieving the unlock info 
Each node can allow users to harvest with their delegated key on that node. The NIS configuration has entries for configuring the maximum number of allowed harvesters and optionally allow harvesting only for certain account addresses. The unlock info gives information about the maximum number of allowed harvesters and how many harvesters are already using the node. 

 
| API path: | Request type:  |
|------|------|
| /account/unlocked/info | POST|

 
##### No parameter: 
##### Example: 
Request cannot be performed in a browser.

 
##### Example of returned JSON object: 
```json
{
        "num-unlocked" : 2,
        "max-unlocked" : 3
        }
``` 
##### Possible Errors: 
None

 
## **4.4. Retrieving historical account data**
--- 
The configuration for NIS offers the possibility for a node to expose additional features that other nodes don't want to offer. One of those features is the supply of historical account data like balance and importance information. To turn on this feature for your NIS, you need to add HISTORICAL_ACCOUNT_DATA to the list of optional features in the file config.properties.

 
| API path: | Request type:  |
|------|------|
| /account/historical/get | GET|

 
##### Description: 
Gets historical information for an account.

 
##### Parameter: 

| Parameter | Description |
|------|------|
|  address   |  The address of the account.   |
|  startHeight   |  The block height from which on the data should be supplied.   |
|  endHeight   |  The block height up to which the data should be supplied. The end height must be greater than or equal to the start height.   |
|  increment   |  The value by which the height is incremented between each data point. The value must be greater than 0. NIS can supply up to 1000 data points with one request. Requesting more than 1000 data points results in an error.   |

 
##### Example: 
 http://bigalice3.nem.ninja:7890/account/historical/get?address=NALICELGU3IVY4DPJKHYLSSVYFFWYS5QPLYEZDJJ&amp;startHeight=17592&amp;endHeight=17592&amp;increment=1 

 
##### Example of returned JSON object: 
```json
{
        [
        {
        "height": 17592,
        "address": "NALICELGU3IVY4DPJKHYLSSVYFFWYS5QPLYEZDJJ",
        "balance": 509676000000,
        "vestedBalance": 100999147150,
        "unvestedBalance": 408676852850,
        "importance": 0.00008857563463531297,
        "pageRank": 0.0007605047835049349
        }
        ]
        }
``` 
##### Possible Errors: 
If the address is invalid, the start height is larger than the endheight, the increment is not a positive or the request results in more than 1000 data points an error is returned.

 

