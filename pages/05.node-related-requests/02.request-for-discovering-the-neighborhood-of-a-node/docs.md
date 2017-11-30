---
title: Request for discovering the neighborhood of a node
taxonomy:
    category: docs
---

 
### Complete neighborhood 
| API path: | Request type:  |
|------|------|
| /node/peer-list/all | GET|

 
##### Description: 
Gets an array of all known nodes in the neighborhood.

 
##### No parameter: 
##### Example: 
http://127.0.0.1:7890/node/peer-list/all

 
##### Example of returned JSON NodeCollection object (&lt;Node&gt;
        denotes a Node object): 
```json
{
        "inactive": [
        &lt;Node&gt;,
        &lt;Node&gt;
        ],
        "active": [
        &lt;Node&gt;,
        &lt;Node&gt;
        ],
        "busy": [
        &lt;Node&gt;,
        &lt;Node&gt;
        ],
        "failure": [
        &lt;Node&gt;,
        &lt;Node&gt;
        ]
        }
``` 
##### Possible Errors: 
In case the node has not been booted yet, NIS will return a JSON error object. See Appendix A: Error object ** **for more information of the error object and Appendix B: NIS Errors for the error message. 

 
### Reachable neighborhood 
| API path: | Request type:  |
|------|------|
| /node/peer-list/reachable | GET|

 
##### Description: 
Gets an array of all nodes with status 'active' in the neighborhood.

 
##### No parameter: 
##### Example: 
http://127.0.0.1:7890/node/peer-list/reachable

 
##### Example of returned JSON NodeCollection object (&lt;Node&gt;
        denotes a Node object): 
```json
{
        "data": [
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
        ]
        }
``` 
##### Possible Errors: 
In case the node has not been booted yet, NIS will return a JSON error object. See Appendix A: Error object ** **for more information of the error object and Appendix B: NIS Errors for the error message. 

 
### Active neighborhood 
| API path: | Request type:  |
|------|------|
| /node/peer-list/active | GET|

 
##### Description: 
Gets an array of active nodes in the neighborhood that are selected for broadcasts.

 
##### No parameter: 
##### Example: 
http://127.0.0.1:7890/node/peer-list/active

 
##### Example of returned JSON NodeCollection object (&lt;Node&gt;
        denotes a Node object): 
```json
{
        "data": [
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
        ]
        }
``` 
##### Possible Errors: 
In case the node has not been booted yet, NIS will return a JSON error object. See Appendix A: Error object ** **for more information of the error object and Appendix B: NIS Errors for the error message. 

 
### Maximum chain height in the active neighborhood 
| API path: | Request type:  |
|------|------|
| /node/active-peers/max-chain-height | GET|

 
##### Description: 
Requests the chain height from every node in the active node list (described in Active neighborhood) and returns the maximum height seen.

 
##### No parameter: 
##### Example: 
http://127.0.0.1:7890/node/active-peers/max-chain-height

 
##### Example of returned JSON BlockHeight object: 
```json
{
        "height": 43920
        }
``` 
##### Possible Errors: 
In case the node has not been booted yet, NIS will return a JSON error object. See Appendix A: Error object ** **for more information of the error object and Appendix B: NIS Errors for the error message. 

 
