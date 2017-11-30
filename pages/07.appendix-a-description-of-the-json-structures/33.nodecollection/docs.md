---
title: NodeCollection
taxonomy:
    category: docs
---

 
##### Description: 
A NodeCollection object holds arrays of nodes with different statuses. The following statuses are supported:

 
##### Description of the fields: 

| Parameter | Description |
|------|------|
| inactive | A connection to the node cannot be established. |
| active | A connection can be established and the remote node responds in a timely manner. |
| busy | A connection can be established but the node cannot provide information within the timeout limits.  |
| failure | A fatal error occurs when trying to establish a connection or the node couldn't authenticate itself correctly.  |
| data | Generic status indicating the node collection just lists nodes without saying anything about the status of the node.  |

 
##### JSON structure by example: 
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
        ],
        }
``` 
##### Description of the fields: 

| Parameter | Description |
|------|------|
| inactive | Denotes the beginning of the array of inactive nodes. |
| active | Denotes the beginning of the array of active nodes. |
| busy | Denotes the beginning of the array of busy nodes. |
| failure | Denotes the beginning of the array of failing nodes. |
| &lt;Node&gt; | The Node object as described in Node. |

 
