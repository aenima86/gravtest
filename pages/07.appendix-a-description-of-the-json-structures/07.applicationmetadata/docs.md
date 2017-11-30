---
title: ApplicationMetaData
taxonomy:
    category: docs
---

 
##### Description: 
The application meta data object supplies additional information about the application running on a node.

 
##### JSON structure by example: 
```json
{
        "currentTime": 9189086,
        "application": "NEM Infrastructure Server",
        "startTime": 9060202,
        "version": "0.4.30-BETA",
        "signer": "CN=NEM Community,OU=Development Team,O=NEM,L=Internet,ST=web,C=WD"
        }
``` 
##### Description of the fields: 

| Parameter | Description |
|------|------|
| currentTime | The current network time, i.e. the number of seconds that have elapsed since the creation of the nemesis block. |
| application | The name of the application running on the node. |
| startTime | The network time when the application was started. |
| version | The application version. |
| signer | The signer of the certificate used by the application. |

 
