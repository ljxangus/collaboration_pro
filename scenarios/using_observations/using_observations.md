# Using Observations in Informational Messages for Performance Optimization 

## Table of Contents
* [Scenario Motivation](#motivation)
* [Scenario Technical Introduction](#introduction)
* [Detailed Message Exchange](#message-exchange)
* [Scenario Conclusion](#conclusion)

## Motivation
This scenario introduces the concepts of _Observations_, _Resources_, and _Demands_. It also 
introduces how to relate a specific _Resource_ declaration to a specific _Demand_.

This scenario is intended to show how two intelligent networks can leverage one another's 
observations and performance feedback to learn when they are harming each other. It will also show
how intelligent networks can share how they intend to use specific resources to service their 
demands in the hopes that other networks will be able to work around them.

## Introduction

This scenario involves a toy example of two Collaborative Intelligent Radio Networks, N1 and N2. 
They each have 2 radio nodes. The radio nodes are laid out according to the diagram below, where 
one node from one network is in close proximity to a node from the other network. The radio 
networks are limited to a total of 40MHz bandwidth, from 2.400 GHz to 2.440 GHz.

In this scenario, each network has to move a large amount of traffic. With a spectral efficiency
of 1 bit per second per Hertz, each network would require 40 MHz of total bandwidth at 100% 
utilization. Splitting the available spectrum in half, 20 MHz per network, will result in half of 
each network's traffic being dropped. 

This scenaro will show how two networks optimize their power and frequency use with only 
Informational messages and sensing. 

**Network Laydown**

![](fig1.png)

This scenario will show how a radio network can optimize its use of the spectrum in terms of power 
and frequency using observations from another network.

## Message Exchange

1.  N1 sends N2 **Hello**: I support:
    *   InformationalDeclaration messages with DEMAND, RESOURCE, PERFORMANCE and OBSERVATION types
    *   InformationalDeclaration messages with Demand types Throughput and Priority
    *   InformationalDeclaration messages with Resource type SpectrumVoxel
    *   InformationalDeclaration messages with Performance type ScalarPerformance
    *   InformationalDeclaration messages with Observation types PSD and Location

2.  N2 sends N1 **Hello**: I support:
    *   MAKE_DECLARATION messages with DEMAND, RESOURCE, PERFORMANCE and OBSERVATION types
    *   InformationalDeclaration messages with Demand types Throughput and Priority
    *   InformationalDeclaration messages with Resource types SpectrumVoxel and Gain_Pattern 
    *   InformationalDeclaration messages with Performance type ScalarPerformance
    *   InformationalDeclaration messages with Observation types PSD, Spectrogram, and Location

3.  N2 now knows that N1 does not understand Spectrograms or GainPatterns, so it will not try to use 
    those for collaboration with N1.

    Both networks are given a massive amount of traffic to move between their nodes. Both networks 
    decide to service this demand by slicing up the entire band among their nodes in an FDMA 
    scheme and transmitting at a high duty cycle. Both networks use a 100 ms sensing window to try 
    to detect interferers. Both networks are a little lazy in their reporting, and only specify the
    resources they use at a very coarse level.

4.  N1 sends N2 **InformationalDeclaration**: starting at time 0 with a duration of 10 seconds including the
    following set of declarations:
    *   My Demand::Throughput is 40Mbps.
    *   I am using Resource::SpectrumVoxel which uses 30 dBm of transmit power from 2.400 to 
        2.440 GHz starting at time 0 and ending at time 900 ms. The Resource is periodic with a 
        period of 1 second.

5.  N2 sends N1 **InformationalDeclaration**: starting at time 0 with a duration of 10 seconds including the
    following set of declarations:
    *   My Demand::Throughput is 40Mbps.
    *   I am using Resource::SpectrumVoxel which uses 30 dBm of transmit power from 2.400 to 
        2.440 GHz starting at time 100 ms and ending at time 1 second. The Resource is periodic 
        with a period of 1 second.

    **Network 1 and Network 2's Plan**

    ![](fig2.png)
    
    Each radio network hears that the other network wants to transmit at high power across the 
    entire band at 90% duty cycle. Each radio network ignores what it was told over the 
    Collaboration Channel, hopes for the best, and locks in its approach for the next 10 seconds. 

6.  9 seconds pass

    Each radio network discovers that "hope" was not an effective interference mitigation strategy. 
    Network nodes 2 and 3 experience major interference due to one another.

    **Received Power at Each Node**
    
    ![](fig3a.png)
    
7.  N1 sends N2 **InformationalDeclaration**: my Performance::ScalarPerformance metric is 0.2 at time 0 to 
    9 seconds.

8.  N1 sends N2 **InformationalDeclaration**: starting at time 7.9 with a duration of 0.1 second including 
    the following set of declarations:
    *   My Observation::PSD at node 1 shows significant power in all my frequency bins
    *   My Observation::PSD at node 2 shows even higher power in all my frequency bins

9.  N1 sends N2 **InformationalDeclaration**: my Performance::ScalarPerformance metric is 0.1 at time 0 to 
    9 seconds.

10. N2 sends N1 **InformationalDeclaration**: starting at time 8 with a duration of 0.2 second including the
    following set of declarations:
    *   My Observation::PSD at node 4 shows significant power in all my frequency bins
    *   My Observation::PSD at node 3 shows even higher power in all my frequency bins

    **Each Node's Observation During Sense Window**
    
    ![](fig3b.png)
    
    At this point, each radio network has 1 second left for the action it has currently declared. 
    Both radio networks note that when they were not being interfered with, they had significant 
    amounts of excess signal to noise ratio. They also note that the other network is seeing a lot 
    of power over the frequencies they were using to transmit. As hoping for the best didn't work, 
    they each decide to reduce their transmit powers to mitigate their impact on the other radio 
    network. They also decide to be a little more specific in the resources they report using.

11. 1 second passes

12. N1 sends N2 **InformationalDeclaration**: starting at time 10 with a duration of 10 seconds including 
    the following set of declarations:
    *   My Demand::Throughput is 20Mbps from node 1 to node 2 
    *   I am using Resource::SpectrumVoxel which uses 10 dBm of transmit power from 2.420 to 
        2.440 GHz starting at time 0 and ending at time 900 ms. The Resource is periodic with a 
        period of 1 second.

13. N1 sends N2 **InformationalDeclaration**: starting at time 10 with a duration of 10 seconds including 
    the following set of declarations:
    *   My Demand::Throughput is 20Mbps from node 2 to node 1 
    *   I am using Resource::SpectrumVoxel which uses 10 dBm of transmit power from 2.400 to 
        2.420 GHz starting at time 0 and ending at time 900 ms. The Resource is periodic with a 
        period of 1 second.

14. N2 sends N1 **InformationalDeclaration**: starting at time 10 with a duration of 10 seconds including 
    the following set of declarations:
    *   My Demand::Throughput is 20Mbps from node 3 to node 4 
    *   I am using Resource::SpectrumVoxel which uses 10 dBm of transmit power from 2.420 to 
        2.440 GHz starting at time 0 and ending at time 900 ms. The Resource is periodic with a 
        period of 1 second.

15. N2 sends N1 **InformationalDeclaration**: starting at time 10 with a duration of 10 seconds including 
    the following set of declarations:
    *   My Demand::Throughput is 20Mbps from node 4 to node 3 
    *   I am using Resource::SpectrumVoxel which uses 10 dBm of transmit power from 2.400 to 
        2.420 GHz starting at time 0 and ending at time 900 ms. The Resource is periodic with a 
        period of 1 second.  

    **Network 1 and Network 2's New Plan**

    ![](fig4.png)

16. 9 seconds pass

    Each radio network detects that the interference from the farthest node has been reduced 
    significantly. However, they also notice that they guessed poorly at splitting up the spectrum 
    for the adjacent nodes. Each adjacent node is transmitting in the band that the node from the 
    other network is trying to receive on. Each network sends these observations to the other. 

    **Received Power at Each Node**
    
    ![](fig5a.png)

17. N1 sends N2 **InformationalDeclaration**: my Performance::ScalarPerformance metric is 0.2 at time 10 to 
    19 seconds.

18. N1 sends N2 **InformationalDeclaration**: starting at time 18 with a duration of 0.1 second including 
    the following set of declarations:
    *   My Observation::PSD at node 1 shows minimal power from 2.420 to 2.440 GHz
    *   My Observation::PSD at node 2 shows minimal power from 2.400 to 2.420 GHz and significant 
        power from 2.420 to 2.440 GHz

19. N1 sends N2 **InformationalDeclaration**: my Performance::ScalarPerformance metric is 0.2 at time 10 to 
    19 seconds.

20. N2 sends N1 **InformationalDeclaration**: starting at time 17.9 with a duration of 0.1 second including 
    the following set of declarations:
    *   My Observation::PSD at node 3 shows significant power from 2.400 to 2.420 GHz and minimal 
        power from 2.420 to 2.440 GHz 
    *   My Observation::PSD at node 4 shows minimal power from 2.400 to 2.420 GHz

    **Each Node's Observation During Sense Window**
    
    ![](fig5b.png)

    Network 1 has a laid back, "wait and see" style. Network 2 just wants to solve the problem as 
    quickly as possible. Network 1 decides to use the same strategy as the previous 10 seconds. 
    Network 2 decides that it should swap its transmit and receive frequencies

21. N1 sends N2 repeats of its previous Demand and Resource declarations, with updated timestamps.

22. N2 repeats its previous Demand and Resource declarations, but swaps which link uses which 
    SpectrumVoxel.

    **Network 2's New Plan**

    ![](fig6.png)

23. 9 seconds pass

    Nodes 1 and 4 are able to receive with no interference. Nodes 1 and 3 get a small amount of
    interference, but it does not impact their throughputs.

    **Received Power at Each Node**
    
    ![](fig7.png)

24. N1 sends N2 **InformationalDeclaration**: my Performance::ScalarPerformance metric is 0.9 at time 20 
    to 29 seconds.

25. N1 sends N2 **InformationalDeclaration**: my Performance::ScalarPerformance metric is 0.9 at time 20 
    to 29 seconds.

## Conclusion

In this scenario, two radio networks determined how to reuse spectrum and minimize interference
using Informational exchanges, optimizing their aggregate throughput. While they arrived at an 
acceptable solution, the networks interfered extensively with one another while trying to get to
that solution. 

Before you leave, consider the following:  

*   How could these networks have used Conversational exchanges to reduce their initial 
    interference?
*   How could these networks deal with changing channel conditions?
*   How could these networks have reduced their reliance on their sense windows to improve their
    throughput?
*   What should the networks have done if, even with frequency reuse, there was still was too 
    little channel capacity to handle their traffic loads?


