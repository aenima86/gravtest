---
title: Requesting information about a node
taxonomy:
    category: docs
---

 
### Basic node information 
| API path: | Request type:  |
|------|------|
| /node/info | GET|

 
##### Description: 
Gets basic information about a node. Using IP 127.0.0.1 gets information about the local node.

 
##### No parameter: 
##### Example: 
http://127.0.0.1:7890/node/info

 
##### Example of returned JSON Node 
```json
{
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
        }
        }
``` 
##### Possible Errors: 
In case the node has not been booted yet, NIS will return a JSON error object. See Appendix A: Error object ** **for more information of the error object and Appendix B: NIS Errors for the error message. 

 
### Extended node information 
| API path: | Request type:  |
|------|------|
| /node/extended-info | GET|

 
##### Description: 
Gets extended information about a node. Using IP 127.0.0.1 gets extended information about the local node.

 
##### No parameter: 
##### Example: 
http://127.0.0.1:7890/node/extended-info

 
##### Example of returned JSON NisNodeInfo object: 
```json
{
        "node": {
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
        }
        },
        "nisInfo":
        {
        "currentTime": 9288341,
        "application": "NEM Infrastructure Server",
        "startTime": 9238484,
        "version": "0.4.33-BETA",
        "signer": "CN=VeriSign Class 3 Code Signing 2010 CA,OU=Terms of use at https://www.verisign.com/rpa (c)10,OU=VeriSign Trust Network,O=VeriSign\\,
        Inc.,C=US"
        }
        }
``` 
##### Possible Errors: 
In case the node has not been booted yet, NIS will return a JSON error object. See Appendix A: Error object ** **for more information of the error object and Appendix B: NIS Errors for the error message. 

 
