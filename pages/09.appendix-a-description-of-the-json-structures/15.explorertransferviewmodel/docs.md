---
title: ExplorerTransferViewModel
taxonomy:
    category: docs
---

 
##### Description: 
The following structure is used by the NEM block chain explorer for convenience reason. The data is similar but not identical to that of a Transaction structure.

 
##### JSON structure by example: 
```json
{
        "tx": &lt;Transaction&gt;,
        "hash": "5cba4614e52af19417fb53c4bdf442a57b9f558aee17ece530a5220da55cf47d",
        "innerHash": "ae3b107f1216e1ccf12b6f3c3c555bc1d95311747338ce66f539ea2c18c0aa57"
        }
``` 
##### Description of the fields: 

| Parameter | Description |
|------|------|
| tx | Entry containing the JSON Transaction object. |
| &lt;Transaction&gt; | The Transaction object. Depending on the type of the transaction the structure will look different. See Appendix A: Transaction objects for the different transaction types.  |
| hash | The hash of the transaction. |
| innerHash | The hash of the inner transaction. This entry is only available for multisig transactions |

 
