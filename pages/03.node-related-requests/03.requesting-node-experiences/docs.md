---
title: Requesting node experiences
taxonomy:
    category: docs
---

 
| API path: | Request type:  |
|------|------|
| /node/experiences | GET|

 
##### Description: 
Gets an array of node experiences from another node. Each node saves its experiences with other nodes in an internal map. Sharing experiences helps nodes to select honest nodes for communication.

 
##### No parameter: 
##### Example: 
http://127.0.0.1:7890/node/experiences

 
##### Example of returned array of JSON ExtendedNodeExperiencePair objects: 
```json
{
        "data": [
        {
        "node":
        "metaData":
        {
        "application": "NIS",
        "version": "0.4.33-BETA",
        "platform": "Oracle Corporation (1.8.0_25) on Windows 8"
        },
        "endpoint":
        {
        "protocol": "http",
        "port": 7890,
        "host": "81.224.224.156"
        },
        "identity":
        {
        "name": "Alice",
        "public-key": "a1aaca6c17a24252e674d155713cdf55996ad00175be4af02a20c67b59f9fe8a"
        },
        "syncs": 3,
        "experience":
        {
        "s": 1,
        "f": 0
        }
        }]
        }
``` 
##### Possible Errors: 
In case the node has not been booted yet, NIS will return a JSON error object. See Appendix A: Error object ** **for more information of the error object and Appendix B: NIS Errors for the error message. 

 
