# Recommended Additional Abstract Noun: *Capability*

## Motivation

Resources (spectrum time/frequency in space) are what the CIRs use, demands are what they need to use resources for, observations tell them about what is occuring or planned on resources, and performance is how they are achieving their goals / servicing their demands. These are all good concepts for the CIRs to collaborate on but none of them tell the other CIRs anything about the CIR itself. Specifically, if you were collaborating in a relay race on a course that had very challenging hills as well as easy flat legs, you'd like to know if you have only millenials on your team who average sub 6-minute miles, or whether you have a group of slackers who barely made it through their couch to 5k training. Therefore, a class of information related to helping CIRs understand what the other CIRs around it can do would be useful to enable the best collaboration.

## Example Concrete Noun Types

```
'Channelization:
{
	double min_chan_bw_hz,
	double max_chan_bw_hz,
	int32 min_chans,
	int32 max_chans,
	bool static_fcs,
	bool is_contiguous,
	}
Framing:
{
	bool is_static,
	optional: int64 frame_duration_ps,
	optional: int64 frame_ref_toNTP_ps (offset relative to second mark of NTP),
	optional: repeated int64 slot_durations_ps, 
		}
```

## Examples

Consider our CIRN operating in the presence of another CIRN. If we observe (and confirm through a RequestYourResourceUse message) that the other CIRN has used a specific resource block, we still have no idea (other than what we can infer from the observation and usage message) if the other CIRN will adhere to implicit time frequency bounds like in the prior usage in the future. If they have sent (or we request) what their channelization and/or framing is, then with the above information we can create a much better representation of what the CIRN is likely to do in the future without having to train up exquisitely complicated model estimators.


## New message type related to *Capability*

Similar to how the existing protocol has methods for requesting information related to the other data types (especially resources), a *ResquestYourCurrentCapabilityUse* message type is recommended:

```
RequestYourCurrentCapabilityUse
{
	type
	start_time
	duration_ps
	my_network_id
	optional: source/destination
	}
```

# Recommended new field in *interrogative* messages & an additional message type *RequestDenied*

## Motivation

Declarations already have a way to invalidate them, it would be best if the interrogative messages had a way for the receiptiant CIRNs to let the requester know that they will not be servicing the request (even if they have the dialect ability to do so). This can save throughput on the collaboration channel by cutting down on messaging that will take longer to collect the data for and send over the collaboration channel than the data will be useful for. 
This requires two elements. First, there must be a request_id field in all interrogative messages sent between CIRs (similar to the statement_id field in declaritive messages). This gives the receiving CIRN a reference to use when responding. Second, it would imply a *RequestDenied* message, which a CIRN could use to respond over the collaboration channel to politely let another CIRN know that he requested information will not be forth coming.

## Example

The simplest example for this need is if a CIRN sends a request that the receiving CIRN determines is going to take a significant amount of its resources (over the air transmissions between nodes, etc.) and that by the time the information can be collected, the specified duration in the request would have already passed. It would be save the receiving CIRN a lot of time, and would be polite to the requesting CIRN, if a simply *denied* message could be returned, thereby saving the receiving CIRN time as well as saving the sending CIRN from a period of expecting a response and having the requested window fly by without one.

```
RequestDenied
{
	request_id
	my_network_id
	}
```

# Suggestions without a corresponding code merge request (thoughts for the future)

- CIRNs would likely love to have a messaging means of asking (and answering) the question of WHY something occured (i.e. "Why did you rate your performance over the last interval as 0.5"). This could be answered in a variety of forms
- CIRNs would likely love to have a means in the *transactional* dialect to share "What's in it for me/you" (WIIFM/Y)
