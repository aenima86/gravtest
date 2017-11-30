---
title: Requesting parts of the block chain
taxonomy:
    category: docs
---

 
NIS can supply either individual blocks identified by block height or block hash or can supply up to 10 blocks beginning at a certain height.

 
### 5.4.1 Getting a block with a given hash 
| API path: | Request type:  |
|------|------|
| /block/get | GET|

 
##### Description: 
Gets a block from the chain that has a given hash.

 
##### Parameter: 

| Parameter | Description |
|------|------|
|  blockHash    |  The 256 bit sha3 hash of the block. The hash must be supplied as hexadecimal string.   |

 
##### Example: 
http://127.0.0.1:7890/block/get?blockHash=58efa578aea719b644e8d7c731852bb26d8505257e03a897c8102e8c894a99d6 

 
##### Example of returned JSON object (main network): 
```json
{
        "timeStamp": 9232942,
        "signature": "005f91b8908fc173a428ff8e8c4a0ee0d69e4004aed0d08f27690b6b6672ef74ccc6b89695bed5f29b0f4a812cb84bfa459f52a4e14a11e574793969f0e1a30f",
        "prevBlockHash": {
        "data": "f721e563b4431594c5af6f6be0a913f47f0aca6c3b8ee6a703bfe175ee54babf"
        },
        "type": 1,
        "transactions": [
        ],
        "version": 1744830465,
        "signer": "78e121cc1cf63424651ec64251e78efda81386c9f5e9eb4cb08b2a2192c9dce5",
        "height": 42803
        }
``` 
##### Possible Errors: 
If the block hash is not found in the database, NIS will return a JSON error object. See Appendix A: Error object or more information of the error object and Appendix B: NIS Errors for the error message. 

 
### 5.4.2 Getting a block with a given height 
| API path: | Request type:  |
|------|------|
| /block/at/public | POST|

 
##### Description: 
Gets a block from the chain that has the given height.

 
##### Parameter: 

| Parameter | Description |
|------|------|
|  blockHeight    |  A BlockHeight JSON object as described in Appendix A: BlockHeight .    |

 
##### Example: 
Request cannot be performed in a browser.

 
##### Example of returned JSON object (test network): 
```json
{
        "timeStamp": 9232942,
        "signature": "005f91b8908fc173a428ff8e8c4a0ee0d69e4004aed0d08f27690b6b6672ef74ccc6b89695bed5f29b0f4a812cb84bfa459f52a4e14a11e574793969f0e1a30f",
        "prevBlockHash": {
        "data": "f721e563b4431594c5af6f6be0a913f47f0aca6c3b8ee6a703bfe175ee54babf"
        },
        "type": 1,
        "transactions": [
        ],
        "version": -1744830463,
        "signer": "78e121cc1cf63424651ec64251e78efda81386c9f5e9eb4cb08b2a2192c9dce5",
        "height": 42803
        }
``` 
##### Possible Errors: 
If the block with the specified height cannot be found in the database, NIS will return a JSON error object. See Appendix A: Error object or more information of the error object and Appendix B: NIS Errors the error message. 

 
### 5.4.3 Getting part of a chain 
| API path: | Request type:  |
|------|------|
| /local/chain/blocks-after | POST|

 
##### Description: 
Gets up to 10 blocks after given block height from the chain. If the database contains less than 10 block after the given height, then less blocks are returned. The returned data is an array of ExplorerBlockViewModel JSON objects.

 
##### Parameter: 

| Parameter | Description |
|------|------|
|  blockHeight    |  A BlockHeight JSON object as described in Appendix A: BlockHeight .    |

 
##### Example: 
Request cannot be performed in a browser.

 
##### Example of returned JSON object: 
```json
{
        "data":[{
        "txes":[{
        "tx": &lt;ExplorerViewModelTransaction&gt;
        "tx": &lt;ExplorerViewModelTransaction&gt;
        }],
        "block": &lt;Block&gt;
        "hash":"8ca8a3e01ac0eb482e668fda74141984ba118b027fc5f1f67d2d36a38bf48c49"
        }]
        }
``` 
##### Possible Errors: 
If the block height supplied is not positive, NIS will return a JSON error object. See Appendix A: Error object ** **for more information of the error object and Appendix B: NIS Errors for the error message. 

 
