---
title: ExplorerBlockViewModel
taxonomy:
    category: docs
---

 
##### Description: 
The following structure is used by the NEM block chain explorer for convenience reason. The data is similar but not identical to that of a Block.

 
##### JSON structure by example: 
```json
{
        "data":[
        {
        "txes":[
        &lt;ExplorerTransferViewModel&gt;,
        &amp;vellip;
        &lt;ExplorerTransferViewModel&gt;
        ],
        "block": &lt;Block&gt; ,
        "hash":"a6f62c62eedf4fafe6991e5cf31eae440963577c919f4eae86b4db8f8e572dce",
        "difficulty": 23456345897
        },
        …
        ]
        }
``` 
##### Description of the fields: 

| Parameter | Description |
|------|------|
| txes | Array containing the transactions of the block. |
| &lt;ExplorerTransferViewModel&gt; | The ExplorerBlockViewModel object as described in ExplorerTransferViewModel  |
| block | Entry containing a JSON block object. |
| &lt;Block&gt; | The Block object as described in Appendix A: Block  |
| hash | The hash of the block as hexadecimal string. |
| difficulty | The block difficulty. |

 
