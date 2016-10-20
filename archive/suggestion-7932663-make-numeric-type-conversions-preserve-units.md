# Make numeric type conversions preserve units [7932663] #

**Submitted by Mat P on 5/13/2015 12:00:00 AM**  
**4 votes on UserVoice prior to migration**  

Currently it's awkward to convert between numeric types and preserve the units, since we end up with a whole raft of conversion functions like:
let i2f (x: int<'u>) : float<'u> =
float x |> LanguagePrimitives.FloatWithMeasure
where for N numeric types, we have N^2 of these functions.
Ideally, the functions int, float, decimal, etc., would preserve the units automatically.



## Response ##
** by fslang-admin on 7/18/2015 12:00:00 AM **

Many thanks for this suggestion. It is being marked as declined – for discussion see the comments.
Further comments, use cases, information and discussion welcome
Don Syme, F# Language and Core Library Evolution.


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/7932663)**


## Comments ##


#### Comment by Don Syme on 6/9/2015 1:39:00 PM ####
I suspect the breaking change implications of this would make it tricky to do.
Don Syme

