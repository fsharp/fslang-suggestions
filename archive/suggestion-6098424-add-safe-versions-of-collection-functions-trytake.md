# Add safe versions of collection functions tryTake and trySkip. [6098424] #

**Submitted by Huw Simpson on 6/25/2014 12:00:00 AM**  
**0 votes on UserVoice prior to migration**  

The take and skip functions on the Seq module raise an error when bounds are exceeded. I suggest the following safe alternatives:
// Safely skip n elements of a sequence, and return the rest.
trySkip : count:int -> source:Seq<'T> -> Seq<'T>
// Safely take n elements from the beginning of a sequence, skip the rest.
tryTake : count:int -> source:Seq<'T> -> Seq<'T>
The suggested functions operate in a similar manner to their link equivalents which don't raise errors when bounds are exceeded.
If this suggestion is accepted it would make sense to implement these functions for List and Array also.



## Response ##
** by fslang-admin on 7/18/2015 12:00:00 AM **

Closing issue with no votes.


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6098424)**


## Comments ##


#### Comment by Huw Simpson on 6/25/2014 11:52:00 AM ####
Typo: "link equivalents" should be "LINQ equivalents"


#### Comment by Huw Simpson on 6/25/2014 12:03:00 PM ####
@dsyme has mentioned that the nth function is to be deprecated and replaced with item, also the corresponding tryItem is to be provided. See: https://github.com/fsharp/FSharpLangDesign/blob/master/CoreLibraryFunctions.md

