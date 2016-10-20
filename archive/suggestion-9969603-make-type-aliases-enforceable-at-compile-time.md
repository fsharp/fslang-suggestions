# Make type aliases enforceable at compile time [9969603] #

**Submitted by Ben Lappin on 9/29/2015 12:00:00 AM**  
**23 votes on UserVoice prior to migration**  

[<Measure>] is enforced by the compiler, but adds no performance overhead and causes no issues for interop.
It would be nice to have a similar attribute that could be applied to any type.



## Response ##
** by fslang-admin on 2/4/2016 12:00:00 AM **

Thanks for the suggestion. I’ve marked it declined with my reasons in the comments below.
Best regards
Don Syme, F# Language and Core Library Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/9969603)**


## Comments ##


#### Comment by Harald Steinlechner on 2/3/2016 6:25:00 AM ####
so you basically propose something like Haskell's newtype?


#### Comment by Don Syme on 2/4/2016 5:00:00 PM ####
We decided against this in F# 1.0
If we make a change here, it would be to implement single-case union types using structs, e.g.
[<Struct>]
type X = X of int
This will be just as performant as a "int" value and the type gets a proper new nominal type for reflection and other purposes.
Another factor is the set of members the type would support - when you think of the .NET representation, you can you define new members on the struct type, but not on a type alias.

