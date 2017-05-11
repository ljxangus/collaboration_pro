# Simple Informational Only Scenario 

## Table of Contents
* [Scenario Motivation](#motivation)
* [Scenario Technical Introduction](#introduction)
* [Detailed Message Exchange](#message-exchange)
* [Scenario Conclusion](#conclusion)


## Motivation

We need a modulation type message specified in the "capability message". 
This is required to easily collabrate with the other networks.
The type of modulation and its parameters can be selected depending on the neighbours' modulation message parameters.

Without N1 having the ability to collaborate using modulation messages, it would be very difficult for N2 to decide what modulation schemes and bands it should use for its transmission. N2 therefore might not be able to effectively collabrate with N1. 

This scenario will show how the simplest interaction available in the Collaboration Protocol can solve this problem. 

## Introduction

This introduces a new message called "ModulationScheme". It gives a highlevel overview of all the SRN supported modulation schemes.   

This scenario involves a toy example of two Collaborative Intelligent Radio Networks, N1 and N2. 
They each have 5 radio nodes. communication within the N1's radio nodes are positioned such that it comes in the radio range of N2's radio nodes. 
If N1 chooses to send the data over DSSS modulation with a particular PN-sequence value, the same band can be reused by N2's node with a different PN-sequence without intefering with N1's transmission.

Hence specifying the modulation type of transmission in N1 nodes might be useful for N2 to reuse the same band.

## Detailed Message Exchange

1.  N1 sends N2 **Capability message**: modulation type message informs the other network its modulation type and parameters (band).  

2.  N2 receives **Capability message**: when N2 wants to send traffic in its nodes which might be neighbouring the N1 nodes, will choose an appropriate modulation type and its parameters.

3.  N2 can use the same channel to send data over a different PN-sequence that doesnot effect the transmission of N1.

##Conclusion

This scenario showed how two radio networks were able to acheive reuse of channel without interference using capability messages with modulation type in the Collaboration Protocol. 
 
This also helps in avoiding the inteference which occurs when both networks are using the same resources with inappropriate modulation type.
 
These factors are to be considered when the modulation scheme, parameters and the band is selected for transmitting on N2.
 