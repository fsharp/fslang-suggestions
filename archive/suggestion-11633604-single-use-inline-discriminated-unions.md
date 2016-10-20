# Single-use / inline discriminated unions [11633604] #

**Submitted by Isaac Abraham on 1/29/2016 12:00:00 AM**  
**8 votes on UserVoice prior to migration**  

I noticed something similar to this in Typescript and it got me thinking - there are occasions when you have a discriminated union that you only want to use as a "one off" e.g.
type WindDirection = N | S | E | W
type Weather = { WindDirection : WindDirection; IsRaining : bool }
Could this be simplified to something like this: -
type Weather = { WindDirection : (N | S | E | W); IsRaining : bool }
Almost like a "nameless DU" - similar in a way to active patterns - which might be useful in making code more concise and / or reasoning about.



## Response ##
** by fslang-admin on 2/3/2016 12:00:00 AM **

Declined – see my comment above.
It’s not a bad idea, but I feel the use of type names is too important in the language to justify the feature (which after all only saves a couple of lines in type definitions, which are themselves rare)
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/11633604)**


## Comments ##


#### Comment by Will Smith on 1/29/2016 3:19:00 PM ####
Interesting idea, but it needs to be able to have a type. What would a function signature that returns one of these WindDirections look like?


#### Comment by Maciej J. Bańkowski on 2/1/2016 3:01:00 PM ####
@Will Smith The background compilation could make up the type on the fly, just like with anonymous types in C#. Unless type with this exact shape already exists the name would be equal to the property name - "WindDirection" in this case. Seems like it may be implementable.
The only question is: is it really worth the effort?


#### Comment by Don Syme on 2/3/2016 10:27:00 AM ####
The Mercury language has this feature (or had, the last time I used it, a long time ago now). We considered it for F# but decided against.
For example, the type would need a name in error messages, quickinfo and inferred signatures. Also, union types accept struct, comment and all sorts of other attributes. Finally the type names are used to disambiguate case names (and ambiguity becomes quite likely here).

