---
title: Initiating a transaction
taxonomy:
    category: docs
---

 
| API path: | Request type:  |
|------|------|
| /transaction/prepare-announce | POST|

 
##### Description: 
Creates and broadcasts a transaction. Since this request involves the private key of an account, it should only be sent to a **local** NIS.

 
##### Parameter: 

| Parameter | Description |
|------|------|
|  requestPrepareAnnounce   |  A RequestPrepareAnnounce JSON object as described in Appendix A: RequestPrepareAnnounce .    |

 
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
There are various errors that can occur due to failure of transaction validation See Appendix A: Error object ** **for more information of the error object and Appendix B: NIS Errors for the error message. 

 
The most common errors are:

 
