---
title: Monitoring the network time
taxonomy:
    category: docs
---

 
| API path: | Request type:  |
|------|------|
| /debug/time-synchronization | GET|

 
##### Description: 
Gets an array of time synchronization results as described in Appendix A: TimeSynchronizationResult . You can monitor the change in network time with this information. 

 
##### No parameter: 
##### Example: 
http://127.0.0.1:7890/debug/time-synchronization

 
##### Example of returned array of JSON TimeSynchronizationResult objects: 
```json
{
        "data": [
        {
        "dateTime": "2014-11-19 19:23:04",
        "currentTimeOffset": 1747,
        "change": 57
        },
        {
        "dateTime": "2014-11-19 19:24:17",
        "currentTimeOffset": 1776,
        "change": 29
        },
        {
        "dateTime": "2014-11-19 19:25:18",
        "currentTimeOffset": 1729,
        "change": -47
        }]
        }
``` 
##### Possible Errors: 
None.

 
