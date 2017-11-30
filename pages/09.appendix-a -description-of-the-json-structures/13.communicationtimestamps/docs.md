---
title: CommunicationTimeStamps
taxonomy:
    category: docs
---

 
##### Description: 
Communication timestamps contain information about the network time of a remote NIS. NEM uses a time synchronization mechanism to synchronize time across the network. Each node maintains a network time which is the time of the computer clock plus an offset which compensates for the deviation from the computer clocks of other nodes.

 
##### JSON structure by example: 
```json
{
        "sendTimeStamp": 9145477789,
        "receiveTimeStamp": 9145477789
        }
``` 
##### Description of the fields: 

| Parameter | Description |
|------|------|
| sendTimeStamp | The network time at the moment the reply was sent. |
| receiveTimeStamp | The network time at the moment the request was received. |

 
