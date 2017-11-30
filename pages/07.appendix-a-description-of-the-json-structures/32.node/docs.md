---
title: Node
taxonomy:
    category: docs
---

 
##### Description: 
Nodes are the entities that perform communication in the network like sending and receiving data. A node has an identity which is tied to an account through which the node can identify itself to the network. The communication is done through the endpoint of the node. Additionally a node provides meta data information.

 
##### JSON structure by example: 
```json
{
        "metaData":
        {
        "features": 1,
        "networkId": 104,
        "application": "NIS",
        "version": "0.4.30-BETA",
        "platform": "Oracle Corporation (1.8.0_05) on Windows 8.1"
        },
        "endpoint":
        {
        "protocol": "http",
        "port": 7890,
        "host": "85.25.36.97"
        },
        "identity":
        {
        "name": "Hi, I am Alice2",
        "public-key": "3302e7703ee9f364c25bbfebb9c12ac91fa9dcd69e09a5d4f3830d71505a2350"
        }
        }
``` 
##### Description of the fields: 

| Parameter | Description |
|------|------|
| metaData | Denotes the beginning of the meta data substructure. |
| features | The number of features the nodes has. |
| networkId | The network id. The following network ids are supported: 104 (hex 0x68): The main network id. 152 (hex 0x98): The test network id.  |
| application | The name of the application that is running the node. |
| version | The version of the application. |
| platform | The underlying platform (OS, java version). |
| endpoint | Denotes the beginning of the endpoint substructure. |
| protocol | The protocol used for the communication (HTTP or HTTPS). |
| port | The port used for the communication. |
| host | The IP address of the endpoint. |
| identity | Denotes the beginning of the identity substructure. |
| name | The name of the node. |
| public-key | The public key used to identify the node. |

 
