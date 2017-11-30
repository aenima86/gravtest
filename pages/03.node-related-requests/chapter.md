---
title: 'Node related requests'
taxonomy:
    category: docs
---

 
### Chapter

# Node related requests 
Nodes are the entities that exchange data in a network. A node is essentially a NIS instance running on a computer. To be able to communicate with the network, a node needs to be booted. Through node requests it is possible to discover other nodes in the network, learn about other nodes experiences and get information about their current chain height.

 
Node structure consists of 3 parts: identity, endpoint and meta data:

 
Every node is tied to an identity which is represented by an account. That way nodes are easier to identify. A node is given an identity during the boot process.

 
The endpoint of a node holds information about the IP address, the port and the protocol used for communication.

 
The meta data holds additional information about the NIS version and the platform NIS is running on.

 
A node groups the set of neighbor nodes into several subsets by assigning a status to each node. The possible statuses are:

 

| Parameter | Description |
|------|------|
|  active   |  Nodes that have this status can be successfully communicated with. Whenever a node is selecting a node for communication, it will pick a node from the set of active nodes.   |
|  inactive   |  Inactive nodes are nodes with which it is not possible to establish a connection.   |
|  busy   |  A node is set to status 'busy' if a connection can be established but the node did not answer a request within a certain time limit.   |
|  failure   |  The status failure is assigned to a remote node in case there is severe error during communication. This can for instance be due to the remote node using a different protocol or the remote node using an identity different from what was expected.   |
|  unknown   |  This status is given to a node if there is no information about the status available.   |

 
 Appendix A: Node has more information and an example JSON Node object. A node object has the following fields: 

 

| Parameter | Description |
|------|------|
|  name   |  The name of the node. This can be any string.   |
|  public-key   |  The public key used to identify the node.   |
|  protocol   |  The protocol used for the communication (currently only HTTP is supported).   |
|  port   |  The port used for the communication.   |
|  host   |  The IP address of the endpoint.   |
|  application   |  The name of the application that is running the node.   |
|  version   |  The version of the application.   |
|  platform   |  The underlying platform (OS, java version).   |

 
