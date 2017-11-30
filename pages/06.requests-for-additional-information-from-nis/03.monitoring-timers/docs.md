---
title: Monitoring timers
taxonomy:
    category: docs
---

 
| API path: | Request type:  |
|------|------|
| /debug/connections/timers | GET|

 
##### Description: 
Gets an array of task monitor structures as described in Appendix A: NemAsyncTimerVisitor . You can monitor the statistics for periodic tasks with this information. 

 
##### No parameter: 
##### Example: 
http://127.0.0.1:7890/debug/timers

 
##### Example of returned array of JSON NemAsyncTimerVisitor objects: 
```json
{
        "data": [
        {
        "last-delay-time": 3000,
        "executions": 1024,
        "failures": 0,
        "successes": 1024,
        "last-operation-start-time": 9317695,
        "is-executing": 0,
        "name": "FORAGING",
        "average-operation-time": 0,
        "last-operation-time": 0
        },
        {
        "last-delay-time": 74181,
        "executions": 71,
        "failures": 0,
        "successes": 71,
        "last-operation-start-time": 9317654,
        "is-executing": 0,
        "name": "REFRESH",
        "average-operation-time": 6,
        "last-operation-time": 7
        }]
        }
``` 
##### Possible Errors: 
None.

 
