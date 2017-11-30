---
title: Status Request
taxonomy:
    category: docs
---

 
| API path: | Request type:  |
|------|------|
| /status | GET|

 
##### Description: 
Determines the status of NIS.

 
##### No Parameter: 
##### Example: 
http://127.0.0.1:7890/status

 
##### Example of returned JSON object: 
```json
{
        "code": 6,
        "type": 4,
        **"message": "status"**
        }
``` 
The code can be interpreted as follows:

 

1. Unknown status.
1. NIS is stopped.
1. NIS is starting.
1. NIS is running.
1. NIS is booting the local node (implies NIS is running).
1. The local node is booted (implies NIS is running).
1. The local node is synchronized (implies NIS is running and the local node is booted).
1. NIS local node does not see any remote NIS node (implies running and booted).
1. NIS is currently loading the block chain from the database. In this state NIS cannot serve any requests.

 
##### Possible Errors: 
If there is no response to this request, NIS is either not running or is in a state where it can't serve requests.

 
