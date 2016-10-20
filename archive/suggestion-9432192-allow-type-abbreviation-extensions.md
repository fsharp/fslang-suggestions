# Allow type abbreviation extensions [9432192] #

**Submitted by Robert Sim on 8/21/2015 12:00:00 AM**  
**1 votes on UserVoice prior to migration**  

Currently this code is disallowed:
type Statistics =
Map<string,double>
with
static member parse (inStr:string) =
...
It would be very useful to be able to extend type abbreviations so we don't have to wrap the underlying type inside a record.



## Response ##
** by fslang-admin on 9/7/2015 12:00:00 AM **

Thanks for the suggestion.
Given the way that type abbreviations are compiled (they are erased by the F# compiler), it is unlikely that we would allow extensions of abbreviations themselves – for example, would the method be available on the abbreviated type as well? How/where would the method exist in the compiled form?
FWIW we considered this in F# 1.0 but decided against it. I don’t think anything specific has changed to warrant us revising that choice at this stage.
As stated in the comment, using a single-case discriminated union or a single-element record type is a suitable workaround.
Don Syme
F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/9432192)**


## Comments ##


#### Comment by Will Smith on 9/6/2015 12:55:00 PM ####
What is wrong with this?:
type Statistics = Statistics of Map<string, double> with
static member parse (insTr:string)=
...

