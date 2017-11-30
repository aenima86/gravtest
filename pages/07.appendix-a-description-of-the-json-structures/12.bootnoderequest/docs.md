---
title: BootNodeRequest
taxonomy:
    category: docs
---

 
##### Description: 
The BootNodeRequest JSNON object is used to transfer the relevant data for booting a local node to NIS. With the boot data NIS can create the local node object and connect to the network.

 
##### JSON structure by example: 
```json
{
        "metaData":
        {
        "application":"NIS"
        },
        "endpoint":
        {
        "protocol":"http",
        "port":7890,
        "host":"localhost"
        },
        "identity":
        {
        "private-key":"a6cbd01d04edecfaef51df9486c111abb6299c764a00206eb1d01f4587491b3f",
        "name":"Alice"
        }
        }
``` 
##### Description of the fields: 
##### Description of the fields: 

| Parameter | Description |
|------|------|
| metaData | Denotes the beginning of the metaData substructure. |
| application | The application name. |
| endpoint | Denotes the beginning of the endpoint substructure. |
| protocol | The protocol to use (only HTTP supported as for now). |
| port | The port to use. |
| host | The IP address to use. |
| identity | Denotes the fof the identity substructure. |
| private-key | The private key used for creating the identity. |
| name | The name of the node (can be anything). |

 
