---
title: NisNodeInfo
taxonomy:
    category: docs
---

 
##### Description: 
The NisNodeInfo object provides detailed information about a node.

 
##### JSON structure by example: 
```json
{
        "node": {
        &lt;Node&gt;
        },
        "nisInfo": {
        &lt;ApplicationMetaData&gt;
        }
        }
``` 
##### Description of the fields: 

| Parameter | Description |
|------|------|
| node | Denotes the beginning of the node substructure. |
| &lt;Node&gt; | The Node object as described in Node. |
| nisInfo | Denotes the beginning of the application meta data substructure. |
| &lt;ApplicationMetaData&gt; | The ApplicationMetaData object as described in ApplicationMetaData. |

 
