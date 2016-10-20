# Avoid boxing when comparing value types [6686290] #

**Submitted by Greg Chapman on 11/8/2014 12:00:00 AM**  
**4 votes on UserVoice prior to migration**  

When emitting code for comparison operators, the F# compiler already special-cases numeric types. I suggest that, when other value types have the appropriate operator, code is emitted to use it. I.e., the compiler should produce the equivalent of:
let inline (<=) (x: ^a when ^a: struct) (y: ^a) =
(^a: (static member (<=): ^a * ^a -> bool) (x, y))



## Response ##
** by fslang-admin on 11/10/2014 12:00:00 AM **

This is effectively a duplicate of /archive/suggestion-6098490-add-a-module-of-efficient-non-structural-equality
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6686290)**


## Comments ##


#### Comment by Abel on 12/17/2015 8:50:00 PM ####
Just a note: while this has status "declined", it was a duplicate and the duplicate has been completed/resolved in F# 4.0.

