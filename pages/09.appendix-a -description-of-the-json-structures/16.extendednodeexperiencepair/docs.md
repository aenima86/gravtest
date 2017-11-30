---
title: ExtendedNodeExperiencePair
taxonomy:
    category: docs
---

 
##### Description: 
When exchanging data with other nodes the result of the communication is divided into three different outcomes: success, neutral and failure. In the cases of success and failure the result is saved to be able to judge the quality of a node. This has influence on the probability that a certain node is selected as partner.

 
##### JSON structure by example: 
```json
{
        "node":
        {
        &lt;Node&gt;
        },
        "syncs": 822,
        "experience":
        {
        "s": 357,
        "f": 0
        }
        }
``` 
##### Description of the fields: 

| Parameter | Description |
|------|------|
| node | Denotes the beginning of the of the Node substructure. |
| &lt;Node&gt; | The remote Node object as described in Node. |
| syncs | The number of synchronization attempts the node had with the remote node. |
| experience | Denotes the beginning of the of the NodeExperience substructure. |
| s | The number of successful communications with the remote node. |
| f | The number of failed communications with the remote node. |

 
