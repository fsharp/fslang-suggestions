# Introduce array spread operator for pattern matching and [<ParamArray>] [11462964] #

**Submitted by Ryan Riley on 1/15/2016 12:00:00 AM**  
**18 votes on UserVoice prior to migration**  

Several languages have introduced a handy spread operator, ..., that can be used to pick up remaining arguments to a function call or when destructuring values. [1] This would be incredibly helpful in F# to reduce boilerplate in methods accepting a [<ParamArray>] or when trying to pattern match arrays:
match [|1;2;3;4|] with
| [||] -> // do stuff with empty array
| [|hd;…tl|] -> // do stuff with hd/tl
[1] https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_operator



## Response ##
** by fslang-admin on 2/3/2016 12:00:00 AM **

Declined per my comment below. We would not extend pattern matching for this one case, but Rick is right that improvements to active patterns may make sense
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/11462964)**


## Comments ##


#### Comment by Ryan Riley on 1/15/2016 2:17:00 PM ####
Testing hypothesis that broken windows applies equally to comments ... please share comments or alternatives! Craig Stuntz suggested a few things on Twitter which led me to explain further why I think this operator is a somewhat natural fit:
Array slices using a slightly similar operator, ..:
[|1;2;3;4|].[1..] = [|2;3;4|]
[|1;2;3;4|].[..2] = [|1;2;3|]
Suggestion to use [|hd::tl|]:
I _think_ :: is restricted to just lists as it is 1) used in the definition of the 'T list type (iirc) and 2) built into the compiler to expect lists (iirc).
Suggestion to use [|hd;;tl|]:
"error FS0010: Incomplete structured construct at or before this point in pattern” in FSI


#### Comment by Richard Minerich on 1/15/2016 3:33:00 PM ####
Instead of hard coding new pattern matches into the language I think it would be better if we could make the implementations of existing active patterns more flexible and require less overhead.


#### Comment by Ryan Riley on 1/18/2016 11:10:00 AM ####
@Rick I'm all for that. How might you amend this proposal to achieve more flexibility?


#### Comment by ADMIN
fsharporg-lang (F# Software Foundation Language Group, F# Software Foundation) on 1/23/2016 6:33:00 AM ####
As written this would require the allocation of a new array for "tl".
If you want "tl" to be a slice into the array, then you're probably better off writing an active pattern for this case.


#### Comment by Don Syme on 1/23/2016 11:34:00 AM ####
This seems fairly corner case since it only works over arrays (and presumably lists too). Given the presence of active patterns in the language I'd like to see a larger set of examples and how they look. For example, would "tl" be copy of the tail of the array?

