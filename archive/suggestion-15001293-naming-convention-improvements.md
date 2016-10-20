# Naming convention improvements [15001293] #

**Submitted by DonO on 6/27/2016 12:00:00 AM**  
**10 votes on UserVoice prior to migration**  

I don't think the language benefits from the use of abbreviations especially when they are not consistent. For example
type ResizeArray<'T> = System.Collections.Generic.List<'T>
I would say that should be named ResizableArray. The current naming sounds like a function. There are more examples of this type of abbreviation that I will try to add when I am reminded of them.



## Response ##
** by fslang-admin on 7/5/2016 12:00:00 AM **

While the suggestion is reasonable, this decision was made as part of the F# 2.0, and the slight improvement isn’t sufficient to justify the breaking change renaming at this point
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/15001293)**


## Comments ##


#### Comment by Jared Hester on 6/27/2016 7:57:00 PM ####
It the context of all the other collections it doesn't sound like a function. Modules requiring qualified access with the same name as the data structure they're operating over contain functions that are typically verbs.
Map.partition
Seq.filter
Array.iter
List.fold
Furthermore the purpose of the abbreviation is to prevent collisions with the List implemented in FSharp.Core
Other abbreviations used in core are:
unit, ref, list, obj, exn, nativeint, unativeint, string, float32, float, single, double, sbyte, byte, int8, uint8, int16, uint16, int32, int64, uint64, char, bool, decimal, int, array, option, seq
@Dono you haven't stated what is inconsistent about this abbreviation


#### Comment by DonO on 6/28/2016 8:21:00 AM ####
What's inconsistent in this example is that array is not abbreviated to Arr. "ResizeArr" You either abbreviate or don't you don't just pick words randomly to abbreviate and leave others.

