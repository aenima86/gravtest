---
title: How to use a multisig account
taxonomy:
    category: docs
---

 
The purpose of multisig accounts is to make accounts safer. But this relies on the user not making mistakes when using multisig accounts. If for instance all private keys of the cosignatories of a multisig account reside on a single computer then the multisig account is essentially as good as a normal account because if that computer gets compromised all private keys are disclosed to the attacks at once.

 
It is therefore essential to have the private key of the cosignatories on different computer preferably in different locations.

 
If you have read "Initiating a multisig transaction" you know that the cosignatories of a multisig transaction must know the hash of the inner transaction in order to be able to sign the multisig transaction. There are two ways of gaining knowledge of that hash:

 
In first case the implementer of the client side software is responsible for transferring the hash to the cosignatories while in second case the NEM network will do it for you.

 
The standard client NCC uses the second method. It lets you handle multisig accounts in a convenient way.

 
 Currently, we recommend to use at least three cosignatories in different locations when using the multisig account feature. If one of the cosignatory's private key gets compromised you should immediately remove that account from the list of cosignatories and afterwards add a new cosignatory (see chapter Adding and removing cosignatories on how to do this).

 
**If a private key is stored on a computer that computer should not be used for surfing the internet or doing other unsafe things.**

 
