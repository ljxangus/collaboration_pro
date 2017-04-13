
#Table of contents 

* [Scenario Motivation] (#motivation)
* [Scenario Technical introduction] (# Introduction)
* [Detailed message exchange] (# message exchange)
* [Scenario Conclusion] (#Conclusion)

##Motivation 
This Scenario arises due to the delay and losses injected in the collabrative network between two gateway nodes.

##Introduction
This scenario involves the example of two collabrative gateway nodes N1 and N2 of two different competitors, A and B respectively. This scenario illustrates why ACK-ing between these nodes is essential.

##Message Exchange
1. Node N1 of one competitor A sends a "collaborate message" to node N2 of competitor B over the collaboration network, the packets can get lost if delay or losses is injected in the link (fig. 1).

2. In this senario, the sender node would be expecting a "collaborate message" with the requested information in return.

3. The receiver node has no clue of this as it did not receive this packet (fig. 2).

4. This can lead to miscommunication and this can be avoided if we have a "ACK message" from the receiver to the sender node after step 1. which informs the node of the correct arrival of the request. 

##Conclusion
In this scenerio, we introduce ACK messages to eliminate miscommunication between two gateway nodes due to loss of packets occuring on the collaborative network.

