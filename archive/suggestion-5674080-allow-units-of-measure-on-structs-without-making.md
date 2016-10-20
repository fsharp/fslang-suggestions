# Allow units of measure on structs without making them generic [5674080] #

**Submitted by Braden Evans on 3/24/2014 12:00:00 AM**  
**4 votes on UserVoice prior to migration**  

Currently you can create structs with a measure type argument like so:
[<Struct>]
type vec3<[<Measure>] 'u> =
val mutable X: float<'u>
val mutable Y: float<'u>
val mutable Z: float<'u>
This has the unfortunate side-effect of making the struct generic (and thus not blittable, and increasing the size by 8 bytes)
Since units of measure are erased at compile time and the struct does not actually have any fields with generic types this is disappointing! Enabling use on primitive structs would greatly enhance the utility of units of measure - since they "infect" the codebase it is hard to use in some places but not others.



## Response ##
** by fslang-admin on 7/18/2015 12:00:00 AM **

Many thanks for this suggestion. It is being marked as declined – for discussion see the comments.
As far as I can tell the underlying struct type is not generic (in compiled code). Is there another issue lurking here?
Further comments, use cases, information and discussion welcome
Don Syme, F# Language and Core Library Evolution.


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5674080)**


## Comments ##


#### Comment by Don Syme on 7/18/2015 1:25:00 PM ####
The underlying struct is not generic when a measure type parameter is added.

