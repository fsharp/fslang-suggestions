# Add support for implicit parameters [5810569] #

**Submitted by Radek Micek on 4/21/2014 12:00:00 AM**  
**14 votes on UserVoice prior to migration**  

Implicit parameters in Scala are used to simulate type classes or to pass singleton values (eg. database connection) to functions without explicitly writing them.
We will need: syntax to mark parameters as implicit, syntax to mark values eligible for use as implicit arguments and syntax to call functions with implicit arguments written explicitly. Additionally we will need to invent scoping rules for implicit values.
Pros: It can make F# programs more modular and it can nicely play with other .NET languages (eg. they will see parameter with attribute `Implicit`).
Cons: It can make programs harder to read.



## Response ##
** by fslang-admin on 9/16/2014 12:00:00 AM **

This is now a duplicate of /archive/suggestion-5762135-support-for-type-classes-or-implicits


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5810569)**


## Comments ##


#### Comment by Loic Denuziere on 5/3/2014 12:13:00 PM ####
I actually think that the best way to go if we want a typeclass/implicit-like feature is to have it show up in the F# language as type classes, and be imlemented in .NET the way you suggest.


#### Comment by Nelak on 6/20/2014 3:25:00 PM ####
There's nothing avoiding writing a type with an op_implicit member, also doing the implicit conversion is possible if you do something like what Thomas describes here:
http://stackoverflow.com/questions/10719770/is-there-anyway-to-use-c-sharp-implicit-operators-from-f
I tried to take the concepts a little bit further by implementing something similar with a computation builder a while ago. This seems to play nice with the language but got I got stuck trying to implement ctor implicit casting and haven't been able to continue investigating it for a while, if you are interested you can take a look at it here:
https://github.com/nelak/FSharp.Implicit

