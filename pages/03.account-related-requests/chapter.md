---
title: Account related requests
taxonomy:
    category: docs
---

 
### Chapter

# Account related requests 
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

 
