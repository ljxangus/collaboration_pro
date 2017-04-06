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

# Suggestions without a corresponding code merge request (thoughts for the future)

- CIRNs would likely love to have a messaging means of asking (and answering) the question of WHY something occured (i.e. "Why did you rate your performance over the last interval as 0.5"). This could be answered in a variety of forms
- CIRNs would likely love to have a means in the *transactional* dialect to share "What's in it for me/you" (WIIFM/Y)
