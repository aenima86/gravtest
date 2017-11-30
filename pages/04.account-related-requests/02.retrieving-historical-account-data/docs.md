---
title: Retrieving historical account data
taxonomy:
    category: docs
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

 
