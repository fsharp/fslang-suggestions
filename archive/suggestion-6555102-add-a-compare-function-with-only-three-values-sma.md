# Add a Compare function with only three values Smaller, Equal or Greater [6555102] #

**Submitted by Hans Rischel on 10/13/2014 12:00:00 AM**  
**1 votes on UserVoice prior to migration**  

// The below function
//
// compareWith: 'a -> 'a -> CompareWithResult
// when 'a : comparison
//
// enables the convenient programming style:
//
// match compareWith x y with
// | Less -> ...
// | Equal -> ...
// | Greater -> ...
//
// This is well-known in SML but not (yet) available in F#.
type CompareWithResult = | Less | Equal | Greater
let compareWith x y =
if x < y then Less
else if x = y then Equal
else Greater



## Response ##
** by fslang-admin on 10/15/2014 12:00:00 AM **

Declined, see comment above


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6555102)**


## Comments ##


#### Comment by Don Syme on 10/15/2014 7:08:00 AM ####
For better or for worse, the ship has sailed on this. FSharp.Core already uses three representations of comparers
1. the "implicit" comparison semantics of the "compare" operation
2. Curried comparison functions T -> T -> int
3. IEqualityComparer objects (which have an OO version signature of #2)
Adding another representation of the return type for comparison would I think be too problematic for the overall library design. The decision to use an integer was effectively made in .NET 1.x and in F# 1.x we decided to stick with this decision.

