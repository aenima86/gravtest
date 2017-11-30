---
title: TimeSynchronizationResult
taxonomy:
    category: docs
---

 
##### Description: 
A time synchronization result is the outcome of the network time synchronization of a node with other remote nodes. To agree upon a common time nodes need to synchronize time every hour.

 
##### JSON structure by example: 
```json
{
        "dateTime": "2014-11-16 20:47:06",
        "currentTimeOffset": 2786,
        "change": 36
        }
``` 
##### Description of the fields: 

| Parameter | Description |
|------|------|
| dateTime | The date and time when the synchronization was performed. |
| currentTimeOffset | The current offset to the local computer clock in milliseconds. |
| change | The change in milliseconds compared to the last synchronization. |

 
