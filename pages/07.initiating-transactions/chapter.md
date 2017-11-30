---
title: Initiating transactions
taxonomy:
    category: docs
child_type: docs
---

 
### Chapter

# Initiating transactions 
Transactions are the way of transferring NEM and/or messages from one account to another. Once a transaction is initiated, it is still unconfirmed and thus not yet accepted by the network. At this point it is not yet clear if it will get included in a block. Never rely on a transaction which has the state 'unconfirmed'. Once it is included in a block, the transaction gets processed and, in case of a transfer transaction, the amount stated in the transaction gets transferred from the sender's account to the recipient's account. Additionally the transaction fee is deducted from the sender's account. The transaction is said to have 0 confirmations at this point. When another block is added to the block chain the transaction has 1 confirmation. The next block added to the chain will give it 2 confirmations and so on.

 
Crypto currencies have the ability to roll back part the block chain. This is essential for being able to resolve forks of the block chain. There is however a maximum number of blocks that can be rolled back, this is called the rewrite limit. Hence forks can only be resolved up to a certain depth too. NEM has a rewrite limit of 360 blocks. Once a transaction has more than 360 confirmations, it cannot be reversed. In real life, forks that are deeper than 20 blocks do not happen, unless there was some severe problem with the block chain due to a bug in the code or an attack of some kind.

 
A client can initiate a transaction in two ways:

 
 
 
Since most client with depend on a local NIS to create the transaction signature Chapters 6.1 through 6.6 will explain transaction related actions using the first way. Chapter 6.7 explains the steps you have to take to gather the data that needs to be signed and how to initiate a transaction the second way. Note however that we will not explain how to create the signature itself since this involves some cryptographical concepts which are out of the scope of this document. 

 
