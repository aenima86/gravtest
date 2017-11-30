---
title: AccountMetaData
taxonomy:
    category: docs
---

 
##### Description: 
The account meta data describes additional information for the account. See Account related requests for details.

 
##### JSON structure by example: 
```json
{
        "status": "LOCKED",
        "remoteStatus": "ACTIVE",
        "cosignatoryOf" : [
        &lt;AccountInfo&gt;,
        &lt;AccountInfo&gt;
        ],
        "cosignatories" : [
        &lt;AccountInfo&gt;,
        &lt;AccountInfo&gt;
        ]
        }
``` 
##### Description of the fields: 

| Parameter | Description |
|------|------|
|  status   |  The harvesting status of a queried account. The harvesting status can be one of the following values: "UNKNOWN":  The harvesting status of the account is not known."LOCKED":  The account is not harvesting."UNLOCKED":  The account is harvesting.   |
|  remoteStatus   |  The status of remote harvesting of a queried account. The remote harvesting status can be one of the following values: "REMOTE":  The account is a remote account and therefore remoteStatus is not applicable for it."ACTIVATING":  The account has activated remote harvesting but it is not yet active."ACTIVE":  The account has activated remote harvesting and remote harvesting is active."DEACTIVATING":  The account has deactivated remote harvesting but remote harvesting is still active."INACTIVE":  The account has inactive remote harvesting, or it has deactivated remote harvesting and deactivation is operational.   |
| cosignatoryOf  |  JSON array of AccountInfo structures. The account is cosignatory for each of the accounts in the array.   |
| cosignatories  |  JSON array of AccountInfo structures. The array holds all accounts that are a cosignatory for this account.   |

 
