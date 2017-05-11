# Simple Informational Only Scenario 

## Table of Contents
* [Scenario Motivation](#motivation)
* [Scenario Technical Introduction](#introduction)
* [Detailed Message Exchange](#message-exchange)
* [Scenario Conclusion](#conclusion)


## Motivation

This scenario is to avoid inteference with the neighouring nodes' transmission when the transmission on this node starts.

The node alerts all its neighbours 

	* before it starts to send on a particular channel
	* or/and before reroutes its path to the destination

This makes sure that the neighbouring nodes donot select the same channel as that of the node for its transmission. Or if they want to use that channel, the routes should be selected accordingly  

## Introduction

This scenario involves a toy example of two Collaborative Intelligent Radio Networks, N1 and N2. 
They each have 5 radio nodes. communication within the N1's radio nodes are positioned such that it comes in the radio range of N2's radio nodes. 
If nodes in the routing path for this communication send a beacon signal to its neighbouring nodes, the N2 network can reuse the same channel avoiding the nodes that comes in the radio range of N1's nodes. This way effective reuse of bands takes place.  

See the diagram.

**Beacon.png**

Without having the ability to collaborate, it would be very difficult for N2 to decide the route reusing the same bands. 
N2 is therefore might not be able to effectively collabrate with N1. 

This scenario will show how the simplest interaction available in the Collaboration Protocol can 
solve this problem. 


## Message Exchange

1.  N1 sends N2 **Beacon message**: The array contains the node id of the nodes present in the routing path and/or the rerouted path.  

2.  N2 receives **Beacon message**: N2 alerts the nodes neighbouring the node ids present in the beacon message against using the same channel as the one used by N1 nodes.

3.  N2 can use the same channel to send data over a path that does not involve the neighbouring nodes. This way, channel is reused and hence better collabration.


## Conclusion

This scenario showed how two radio networks were able to acheive reuse of channel without interference using beacon messages in the Collaboration Protocol. 
 
This also helps in avoiding the inteference which occurs in the neighbouring nodes when a node is down and the network reroutes the messages.

These factors are also to be considered when the route and the band is selected for transmitting. 

