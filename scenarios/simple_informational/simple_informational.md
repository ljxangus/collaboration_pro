# Simple Informational Only Scenario 

## Table of Contents
* [Scenario Motivation](#motivation)
* [Scenario Technical Introduction](#introduction)
* [Detailed Message Exchange](#message-exchange)
* [Scenario Conclusion](#conclusion)


## Motivation

This scenario introduces the most basic apsect of Collaboration, "feedback." Feedback takes place 
through the protocol using the _Performance_ object. Currently these are the only "required" set of
messages that all networks must support. 

In this scenario, the reader will see how even the most basic form of the Collaboration Protocol 
can be leveraged by an intelligent radio network to help it make better decisions.

The Collaboration Protocol only expressly requires that networks support two fundamental messages: 

*   The **Hello** message, which allows a network to share the list of messages it understands with
    its peers

*   The **InformationalDeclaration::Performance::ScalarPerformance** message, which allows a network to 
    share how well it is doing in terms of a single, real valued number. 


These messages, while very basic, can still be used to dramatically improve the speed at which 
intelligent networks learn how to work with one another. This scenario provides an example of how 
two intelligent radio networks converge on a desirable solution using the simplest set of messages 
in the Informational subprotocol. 


## Introduction

This scenario involves a toy example of two Collaborative Intelligent Radio Networks, N1 and N2. 
They each have 3 radio nodes. One of N1's radio nodes is positioned such that it triggers a hidden 
node problem from the perspective of N2. No nodes from N2 can detect transmissions from this node. 
Both N1 and N2 start off with the (simple and bad) assumption that any node in the scenario could 
close a link to any other node. 

See the diagram below:

**Radio Node Laydown for Networks 1 and 2**

![](fig1.png)


Without having the ability to collaborate out of band, it would be very difficult for N2 to detect
node 1. N2 is therefore very likely to unintentionally interfere with N1. 

This scenario will show how the simplest interaction available in the Collaboration Protocol can 
solve this problem. 


## Message Exchange

1.  N1 sends N2 **Hello**: I fully support the **Hello** message and support **InformationalDeclaration**
    messages with **Performance** types. I only support the **scalar_performance** metric.

    The **my_dialect** field in the **Hello** message looks like:
    "0.1.1",
    "0.1.2",
    "0.3.102.100"

    This corresponds to:
    Collaborate.hello.my_dialect,
    Collaborate.hello.my_network_id,
    Collaborate.performance.scalar_performance

2.  N2 sends N1 **Hello**: I fully support the **Hello** message and support **InformationalDeclaration**
    messages with **Performance** types. I only support the **scalar_performance** metric.

    The **my_dialect** field in the **Hello** message looks like:
    "0.1.1",
    "0.1.2",
    "0.3.102.100"

3.  N1 starts up a TDMA network with each of its nodes getting a slice of the spectrum allocated. 
    N1 is using 60% of the time/frequency resources. 

    **TDMA Frame for Network 1**

    ![](fig2.png)

4.  N2 also starts up a TDMA network, but senses the spectrum first. It is able to estimate N1's 
    TDMA frame duration. Based on its observations, N2 assumes that only 40% of the time/frequency
    resources are used by N1. N2 ony requires 30% of the spectrum, makes a lucky guess, and 
    allocates free spectrum.

    **TDMA Frame for Network 1 with Network 2 Using Empty Slots**

    ![](fig3.png)

5.  5 seconds pass

    Since no one is transmitting on top of anyone else, both radio networks are happy. They don't 
    really need information from anyone, but they decide to share how great they're doing to let 
    everyone know that they aren't being interfered with and are very happy with the status quo. 

6.  N1 sends N2 **InformationalDeclaration**: my Performance::ScalarPerformance metric is 1.0 from time 0 
    to 5 seconds.
 
7.  N2 sends N1 **InformationalDeclaration**: my Performance::ScalarPerformance metric is 1.0 from time 0
    to 5 seconds.
 
8.  N2's traffic load increases such that it requires an additional 10% of time/frequency 
    resources. It still does not detect the transmissions from N1's hidden node and allocates 
    spectrum on top of the transmissions from the hidden N1 node 1. 

    **TDMA Frame for Network 1 Showing Interference from Network 2 Due to Extra Spectrum Use**

    ![](fig4.png)


9.  5 seconds pass
    
    N2 causes interference on the links from N1's hidden node back to its visible nodes, but is 
    oblivious to this fact. N2 reports to the world that it is still happy and hopes no one else 
    wants to change.

    N1 notices that it's performance was degraded pretty significantly. It hopes that if it tells 
    someone that something bad just happened, the other network will stop hurting it.

10. N1 sends N2 **InformationalDeclaration**: my Performance::ScalarPerformance metric is .83 from time 5 
    to 10 seconds.

11. N2 sends N1 **InformationalDeclaration**: my Performance::ScalarPerformance metric is 1.0 from time 5 
    to 10 seconds.

12. N2 realizes that its use of that extra 10% of resources is degrading N1. It thinks there is 
    still a spare 10% of resources elsewhere.
 
13. N2 deallocates its new spectrum use in conflict with N1 and tries out the other 10% of 
    resources it believes to be available.

    **TDMA Frame for Network 1 Showing Updated Network 2 Use**

    ![](fig5.png)

14. 5 seconds pass

    N1 breathes a sigh of relief. It doesn't know what happened, other than that it is now getting
    great performance again. It hopes nobody needs to change again.
 
    N2 is also still happy. It switched to a different set of resources and was able to get all the
    throughput it needed. It also hopes that no more changes are needed.

15. N1 sends N2 **InformationalDeclaration**: my Performance::ScalarPerformance metric is 1.0 from time 10 
    to 15 seconds.
 
16. N2 sends N1 **InformationalDeclaration**: my Performance::ScalarPerformance metric is 1.0 from time 10 
    to 15 seconds.


## Conclusion

This scenario showed how two radio networks were able to solve the canonical hidden node problem
using only the most fundamental messages in the Collaboration Protocol. This example used the 
Declarative form of messages, but it could have just as easily used the Interrogative 
**InformationalQuery** messages to arrive at the same result. 
 
While the two radio networks did stumble over each other at the start, they eventually came to a 
satisfactory operating point. Note that this was a simple example between two small stationary 
networks. Before you leave, consider the following: 

*   How well would this work if the environment was rapidly changing?
*   How could the networks have used the existing protocol to converge faster? 
*   What sort of information exchange could have prevented the networks from accidentally 
    interfering in the first place? 
