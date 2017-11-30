---
title: Namespaces
taxonomy:
    category: docs
---

 
NEM supports the concept of namespaces which is the NEM analog of internet domain names. A namespace is an identification string that consists of one or more parts that are concatenated by dots, for example 'makoto.metals.silver'. All namespaces are unique and thus can only have one owner at a time. A namespace that has only one part is called a root namespace, otherwise sub-namespace. Root namespaces can be rented by accounts for the duration of one year. One month before the root namespace expires the rental contract can be renewed for another year. If a root namespace rental contract is renewed, all sub-namespaces are valid for another year as well. If the root namespace is not renewed, it exires together with all sub-namespaces. One month after a root namespace expires, another account is able to rent that root namespace. The new owner does not inherit the sub-namespaces from the previous owner however. An account can only rent a sub-namespace if it owns the corresponding root namespace. 

 
 Namespaces have certain restrictions with respected to the characters being allowed in the parts as well as the length of a part. A root namespace may have a length of 16 characters while sub-namespaces may have a length of 64 characters. Valid characters are: a, b, c, ..., z, A, B, C, ..., Z, 0, 1, 2, ..., 9, _ , - However a part is only allowed to begin with a letter from the alphabet, thus 'alice' is an allowed part for a root namespace while '1alice' is not. Certain strings are reserved and thus not allowed as namespace parts. Among the disallowed namespace parts are nem, user, account, org, com, biz, net, edu, mil, gov and info. This list is not final and can be extended in the future. Thus 'user.alice' or 'alice.user' are not allowed in the NEM namespace system. The namespace may have up to 3 parts, thus 'makoto.metals.silver' is valid while 'makoto.metals.silver.coin' is not. 

 
 A namespace rental contract is done via a Appendix A: ProvisionNamespaceTransaction . In addition to the usual transaction fee there is a rental fee. This fee is paid to the so called rental fee sink which is a special account with address NAMESPACEWH4MKFMBCVFERDPOOP4FK7MTBXDPZZA in the main net and TAMESPACEWH4MKFMBCVFERDPOOP4FK7MTDJEYP35 in the test net. The fee for renting a namespace for one year is 50000 XEM for a root namespace and 5000 XEM for a sub-namespace. 

 
 The ownership of a namespace is needed in order to create mosaics. 

 
### 7.3.1 Retrieving root namespaces 
| API path: | Request type:  |
|------|------|
| /namespace/root/page | GET|

 
##### Description: 
Gets the root namespaces. The requests supports paging, i.e. retrieving the root namespaces in batches of a specified size. The request returns an array of NamespaceMetaDataPair objects.

 
##### Parameter: 

| Parameter | Description |
|------|------|
|  id   |  The topmost namespace database id up to which root namespaces are returned. The parameter is optional. If not supplied the most recent rented root namespaces are returned.   |
|  pagesize   |  The number of namespace objects to be returned for each request. The parameter is optional. The default value is 25, the minimum value is 5 and hte maximum value is 100.   |

 
##### Example: 
http://127.0.0.1:7890/namespace/roots?id=26754&amp;pageSize;=35

 
##### Example of returned JSON object: 
```json
{
        "data": [{
        "meta":{
            "id":26264,
        },
        "namespace":{
            "fqn": "makoto.metal.coins",
            "owner": TD3RXTHBLK6J3UD2BH2PXSOFLPWZOTR34WCG4HXH",
            "height": 13465
        }
        },{
            "meta":{
            "id":25421,
        },
        "namespace":{
            "fqn": "gimre.vouchers",
            "owner": TDGIMREMR5NSRFUOMPI5OOHLDATCABNPC5ID2SVA",
            "height": 12392
        }
        }]
        }
``` 
##### Possible Errors: 
None.

 
### 7.3.2 Retrieving a specific namespace 
| API path: | Request type:  |
|------|------|
| /namespace | GET|

 
##### Description: 
Gets the namespace with given id.

 
##### Parameter: 

| Parameter | Description |
|------|------|
|  namespace   |  The namespace id.   |

 
##### Example: 
http://127.0.0.1:7890/namespace?namespace=makoto.metal.coins

 
##### Example of returned JSON object: 
```json
{
        "fqn": "makoto.metal.coins",
        "owner": TD3RXTHBLK6J3UD2BH2PXSOFLPWZOTR34WCG4HXH",
        "height": 13465
        }
``` 
##### Possible Errors: 
NIS returns an error if the namespace parameter is missing or invalid. See Appendix B: NIS Errors for details about errors. 

 
