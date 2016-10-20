# Implement a more idiomatic Flow Syntax [5827517] #

**Submitted by Bryan Edds on 4/24/2014 12:00:00 AM**  
**3 votes on UserVoice prior to migration**  

F#'s current FlowSyntax().WhitspaceHack() should be displaced with a more ML-style syntax -
// Multi-line usage.
// Please pardon the underlines, the webpage is eating my space chars...
with person do
____SetName "Joe"
____SetAge 35
____SetHeight 6.1
// Single-line usage.
with person do SetName "Joe"; SetAge 35; SetHeight 6.1
Of course, the actual keyword `with` could probably not be used since it's already pretty overloaded, but coming up with an alternative would be easy.
Visually tracking where the current F# flow-syntax hack is used is painful, and makes code formatting very inconsistent (a lot of people just use it everywhere without knowing it has special meaning). () is unit, and should be conventional have white space between it and its previous token.



## Response ##
** by fslang-admin on 7/18/2015 12:00:00 AM **

Many thanks for this suggestion. It is being marked as declined – for discussion see the comments.
Further comments, use cases, information and discussion welcome


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5827517)**


## Comments ##


#### Comment by Bryan Edds on 4/26/2014 7:19:00 AM ####
Addendum:
For the single-liner, I think an end token might be required -
with person do SetName "Joe"; SetAge 35; SetHeight 6.1 end
Otherwise the last two sections might be ambiguous to parse.


#### Comment by Don Syme on 7/18/2015 11:59:00 AM ####
For better or worse, removing or deprecating the existing syntax would not be possible at this stage of the language evolution. Adding another alternative syntax probably wouldn't achieve the goals and benefits outlined.

