# Code robustness: Range of admissible values for class fields and record fields (from Ada 2012) [12803943] #

**Submitted by Alexei Odeychuk on 3/4/2016 12:00:00 AM**  
**1 votes on UserVoice prior to migration**  

I suggest introducing an aspect that can be applied to declarations of classes and record types with the aim of specifying ranges of admissible values for class fields and record fields easily.
This suggestion is an extension of my previous suggestion:
Code robustness: Types with ranges of admissible values (from Ada 2012)
Please see: /archive/suggestion-12802701-code-robustness-types-with-ranges-of-admissible-v
Example # 1: Record type with ranges of admissible values specified for its fields.
type Location = {
mutable Y: float range –1.0 .. 1.0 = 1.0
mutable X: float range -1.0 .. 1.0 = 0.0 // field X is default initialized to 0.0, its admissible values are in a range from -1.0 to 1.0
}
Example # 2: Class with ranges of admissible values specified for its private fields, and access methods to get and set its fields
type Location() =
let mutable x : int range -1.0 .. 1.0 = 1.0
let mutable y: int range –1.0 .. 1.0 = 0.0
member this.X with get() = x and set value = x <- value
member this.Y with get() = y and set value = y <- value
The aspect should be checked (checks for admissible values should be generated in compiled code by the F# compiler and performed) whenever an object of the type is default initialized, on assignments, on type casts, on parameter passing, in the match expressions and so on.
This change in the F# language syntax will not affect existing codebase. It requires introducing a new keyword: range. I think it's worth it. This syntax will help represent a programmer's intents in code, improve code robustness, clarity and expressiveness of the F# language.



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/12803943)**


## Comments ##

