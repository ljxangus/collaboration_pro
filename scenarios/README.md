# Collaboration Protocol Scenarios

This directory contains a set of scenarios that each describe a subset of the Collaboration 
Protocol. Scenarios should be thought of having 3 main purposes:

1.  A new scenario should accompany any proposed additions to the Collaboration Protocol to explain 
    to the Collaboration Protocol maintainer why the new messages would be useful. How do the new 
    messages enable behaviours that are not currently possible? Why are these behaviors useful? 

2.  If accepted into the Collaboration Protocol, scenarios serve to illustrate to others the value 
    of new functionality and convince others to support this subset of the Collaboration Protocol.
    Messages will only be useful if enough users support them.

3.  Provide additional context in how to use the Collaboration Protocol messages 


Scenarios should comply with the following guidelines:

*   Each scenario should be in markdown format, similar to this file. See here for directions on 
    formatting markdown files: https://docs.gitlab.com/ee/user/markdown.html

*   Each scenario should have its own subdirectory. Each scenario is put in its own subdirectory to 
    allow users to include supporting diagrams if needed (this is strongly encouraged). A picture 
    is worth a thousand words. This is equally true for sequence diagrams. 

*   Each scenario should include the following sections:

    *   Motivation: Why is this scenario and the messages described within relevant? What problems 
        is it trying to solve and why is it better or unique from what has already been discussed 
        in other scenarios? 
    
    *   Introduction: Ground the scenario in a concrete example. What radio networks are 
        participating? How many nodes do the networks each have? Where are they? How does the 
        scenario setup support the goals outlined in the Motivation section? 

    *   Message Exchange: Walk through the scenario in time. Explain what information is exchanged
        between networks, the needs or demands driving each network towards a given decision, and 
        what actions each network is taking. 

    *   Conclusion: Wrap up the scenario with any closing comments. The Collaboration Protocol 
        maintainers may use this section to prompt users with other things to consider. 

Clear, consistent documentation will help all users and the SC2 Team understand the intent of newly 
added functionality.

----------------------------------------------------------------------------------------------------
# Scenario Abstracts

Scenarios are grouped into a series of sections based around which subprotocol they are focused on. 

_Note: The scenarios are intended to be illustrative, but not fully inclusive of all possible 
functionality._

----------------------------------------------------------------------------------------------------
## Informational Collaboration

All scenarios in this section exclusively use the Informational subprotocol of the Collaboration 
Protocol. The Informational subprotocol is a set of "one-way" messages. These may be thought of as broadcasting out statements or facts using the Declarative set of messages, or requesting 
information from another network using the Interrogative set of messages. 

The initial version of the Collaboration Protocol has broken up the subjects of Informational 
messages into 4 broad classes. These 4 classes should cover nearly everything a radio network 
would need to include in a Declarative or Interrogative message:

*   **Resource:** Something that a radio network might use, like the spectrum at a given location 
    or the gain pattern that results from steering a null using multiple antennas. 

*   **Demand:** Something that is driving the network with some requirements, ie required 
    throughput, Quality of Service metrics, etc.

*   **Performance:** Something that encapsulates a metric important to the network, often closely
    correlated to a requirement imposed by a Demand on the network. Examples are throughput, 
    bit error rate, etc.

*   **Observation:** Something directly viewable by a node or nodes in an intelligent radio network.
    Examples might be a power spectral density measurement or spectrogram at a given location. 


While Informational messages are a useful means of exchanging information, they lack the ability
to form formal agreements between intelligent radio networks. It is anticipated that the 
Conversational subprotocol, described later, will enable that capability. See below for a list of
the scenarios focused on the Informational subprotocol.

### Informational Scenarios
1. [Simple Informational](simple_informational/simple_informational.md)

    This scenario shows one of the simplest possible collaborative exchanges between two 
    intelligent radio networks. In this scenario, the two radio networks use simple performance 
    feedback to solve the hidden node problem.

2. [Using Observations](using_observations/using_observations.md)

    This scenario is an example of how intelligent radio networks can express intent and leverage 
    the observations of others to reduce the time required to converge to a satisfactory soltuion. 
    This scenario illustrates how networks may share observations to do simple optimizations in 
    power and frequency use.

3. [Introduction to Capabilities](capability_intro/capability_intro.md)

    This scenario explains the concept of capabilities. 

4. [Using ACK Messages](using_ack_messages/read_me.md) 

    This scenario is an example of how to use ACK messages to make the Collaboration Channel more
    efficient under unreliable channel conditions.

5. [Introduction to Modulation Types](modulation_type/modulation_scheme.md)

    This scenario motivates the use of Modulation types in the Collaboration Protocol.

6. [Introduction to Spectrum Usage Preferences](spectrum_preferences/spectrum_usage_preference.md)

    This scenario explains how to use Network Level Spectrum Usage preferences to allow an
    ensemble of CIRNs to use the spectrum more efficiently.

7. [Using Beacons](using_beacons/beacon.md)

    This scenario shows how to use beacon or Node Level Resource Usage messages to allow CIRNs to
    share the spectrum more efficiently

8. **To Be Added By Competitors** Reactive to Priority




----------------------------------------------------------------------------------------------------
## Conversational Collaboration

All scenarios in this section use the Conversational subprotocol of the Collaboration Protocol. 
This subprotocol is intended to support the ability for networks to make proposals to one another,
reject them or make counter proposals, and seek agreement or consensus rather than taking action
unilaterally and hoping for the best.

**To Be Added By Competitors** 
