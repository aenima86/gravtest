---
title: Monitoring incoming and outgoing calls
taxonomy:
    category: docs
---

 
| API path: | Request type:  |
|------|------|
| /debug/connections/incoming | GET|

 
##### Description: 
Gets an audit collection of incoming calls as described in Appendix A: AuditCollection . You can monitor the outstanding and recent incoming requests with this information. 

 
##### No parameter: 
##### Example: 
http://127.0.0.1:7890/debug/connections/incoming

 
##### Example of returned JSON AuditCollection object: 
```json
{
        "outstanding": [
        {
        "path": "/debug/connections/incoming",
        "start-time": 9317306,
        "host": "127.0.0.1",
        "elapsed-time": 0,
        "id": 4070
        }],
        "most-recent": [
        {
        "path": "/debug/connections/incoming",
        "start-time": 9317306,
        "host": "127.0.0.1",
        "elapsed-time": 0,
        "id": 4070
        },
        {
        "path": "/chain/score",
        "start-time": 9317303,
        "host": "95.16.203.168",
        "elapsed-time": 3,
        "id": 4069
        }]
        }
``` 
##### Possible Errors: 
None.

 
| API path: | Request type:  |
|------|------|
| /debug/connections/outgoing | GET|

 
##### Description: 
Gets an audit collection of outgoing calls as described in Appendix A: AuditCollection . You can monitor the outstanding and recent outgoing requests with this information. 

 
##### No parameter: 
##### Example: 
http://127.0.0.1:7890/debug/connections/outgoing

 
##### Example of returned JSON AuditCollection object: 
```json
{
        "outstanding": [
        {
        "path": "/chain/blocks-after",
        "start-time": 9317511,
        "host": "88.12.55.125",
        "elapsed-time": 6,
        "id": 6452
        }],
        "most-recent": [
        {
        "path": "/chain/blocks-after",
        "start-time": 9317511,
        "host": "88.12.55.125",
        "elapsed-time": 6,
        "id": 6452
        },
        {
        "path": "/chain/hashes-from",
        "start-time": 9317511,
        "host": "88.12.55.125",
        "elapsed-time": 6,
        "id": 6451
        }]
        }
``` 
##### Possible Errors: 
None.

 
