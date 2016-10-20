# Allow overloading based on unit of measure [6183592] #

**Submitted by trek42 on 7/17/2014 12:00:00 AM**  
**1 votes on UserVoice prior to migration**  

It will be very useful if we could e.g.,
[<Measure>] type rad
[<Measure>] type deg
and call Math.Cosine(10.0<rad>) and Math.Cosine(10.0<deg>).
This can be useful in other scenarios, such as using one function "toSecond" to convert from <hour>, <minute>, etc.
Currently this is not allowed because after removing the measure tag these two functions have the exact same signature. There is a way to workaournd this by adding a dummy DU and using duck type (similar to http://stackoverflow.com/questions/21862335/f-operator-overloading-for-conversion-of-multiple-different-units-of-measure), but this seems too hacky. (plus, the DU is not optimized away in debug mode and makes testing more expensive due to garbage collection pressure).
Proposal: we could give these methods different [<CompiledName>] attributes to avoid conflicts, and compiler should then allow them to have the same name in FSharp, like
/// This should compile fine because these methods don't conflict in compiled assembly.
type Math =
[<CompiledName("CosineRad")>]
static member Cosine(x: float<rad>) = ...
[<CompiledName("CosineDeg")>]
static member Cosine(x: float<deg>) = ...



## Response ##
** by fslang-admin on 9/3/2014 12:00:00 AM **

Unfortunately limitations on compiled .NET code mean that this is not possible – .NET requires that erased signatures be distinct.
Don Syme, Current BDFL for F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6183592)**


## Comments ##

