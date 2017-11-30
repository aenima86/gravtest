---
title: Booting the local node
taxonomy:
    category: docs
---

 
| API path: | Request type:  |
|------|------|
| /node/boot | POST|

 
##### Description: 
Boots the local node and thus assign an account (the identity) to the local node.

 
##### Parameter: 

| Parameter | Description |
|------|------|
|  bootNodeRequest    |  A BootNodeRequest JSON object as described in Appendix A: BootNodeRequest .    |

 
##### Example: 
Request cannot be performed in a browser.

 
##### No return value 
##### Possible Errors: 
In case the node has already been booted, NIS will return a JSON error object. See Appendix A: Error object for more information of the error object and Appendix B: NIS Errors for the error message. 

 
