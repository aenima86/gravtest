---
title: AuditCollection
taxonomy:
    category: docs
---

 
##### Description: 
An audit collection consists of two arrays, containing information about incoming requests from other nodes. The first array contains information about outstanding (i.e. not yet processed requests) and the second array contains information about the most recent requests. The audit collection is for debug purposes.

 
##### JSON structure by example: 
```json
{
        "outstanding": [{
        "path": "/chain/score",
        "start-time": 9020618,
        "host": "86.124.91.183",
        "elapsed-time": 5,
        "id": 797725
        }],
        "most-recent": [{
        "path": "/push/transaction",
        "start-time": 9020621,
        "host": "hachi.nem.ninja",
        "elapsed-time": 2,
        id": 797750
        }]
        }
``` 
##### Description of the fields: 

| Parameter | Description |
|------|------|
| path | The relative URL path. |
| start-time | The number of seconds elapsed since the creation of the nemesis block. |
| host | The host which initiated the request. |
| elapsed-time | The time in seconds that has elapsed since the request was received. |
| id | The unique id of the request. |

 
