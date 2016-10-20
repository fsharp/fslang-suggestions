# Types with default initial values specified (from Ada 2012) [12800967] #

**Submitted by Alexei Odeychuk on 3/4/2016 12:00:00 AM**  
**3 votes on UserVoice prior to migration**  

I suggest introducing an aspect that can be applied to declarations of enumeration types, discriminated union types and user-defined numeric types with the aim of specifying their default initial values in code easily.
This suggestion is an extension of my previous suggestion:
Types with predicates to create subtypes easily (from Ada 2012)
Please see it for more details:
/archive/suggestion-12564486-types-with-predicates-to-create-subtypes-easily-f
Example # 1:
type OK = bool [with] default true // type with true as its default initial value
Example # 2:
type Animals =
| Tiger
| Lion
| Cat
| Mouse
| Hamster
[with] default Cat
type Prey = Animals
with function
| Mouse
| Hamster -> true
| _ -> false
[and] default Hamster
let a : Prey array = Array.zeroCreate 3 // array of 3 hamsters
Remark: "[and]" or "[with]" means that the "and", "with" keywords are optional in the above-mentioned lines of code.
It's not a breaking change in the language; no new keywords are needed to implement this syntax in the F# language. I think this syntax will help represent a programmer's intent in code and improve the expressiveness of the F# language.



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/12800967)**


## Comments ##


#### Comment by Jack Fox on 3/6/2016 11:41:00 AM ####
I suggest making the "and" and "with" keywords mandatory...I think it improves readability.


#### Comment by Richard Gibson on 4/13/2016 9:56:00 AM ####
This would be great, especially if the F# library would come with a function similar to `genericOne` and we can use this as a static type constraint.
That way you could write a generic function that works on any type that defines a default value.

