# Compound types [7228061] #

**Submitted by Greg Rosenbaum on 3/16/2015 12:00:00 AM**  
**4 votes on UserVoice prior to migration**  

This is a feature present in Scala.
A compound type is an extension of flexible types that involves multiple type constraints on a type parameter. You specify compound types like this:
let example (a : 'a :> I1 & I2) = ...
let example (a :> I1 & I2) = ...
let example<'a when 'a :> I1 & I2>() = ...
These are similar to:
let example (a : 'a when 'a :> I1 and 'a :> I2) = ...
let example<'a when 'a :> I1 and 'a :> I2>() = ...
The & symbol is chosen not to conflict with the word 'and' when specifying multiple type constraints.



## Response ##
** by fslang-admin on 2/3/2016 12:00:00 AM **

Declining – see comment below from Don Syme


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/7228061)**


## Comments ##


#### Comment by Jon Ludwig on 3/23/2015 1:25:00 PM ####
Syntactically I think it would be nice to use the word "and" instead of "&" since we already use "and" in the more verbose version.


#### Comment by Greg Rosenbaum on 4/1/2015 1:00:00 PM ####
@Jon Ludwig, yes I initially wanted to use the word 'and', but it makes things more difficult to parse, both for humans and for the compiler. E.g. consider `let example<'a, 'b when 'a :> I1 and I2 and 'b :> I2>. I think it should be possible to immediately distinguish between a compound type and another type constraint. Other options are 'a :> I1 I2 (just using a space), 'a :> I1+I2, 'a :> I1 with I2 (this is how it's written in Scala). I'm also hesitating of using the comma.


#### Comment by Don Syme on 6/9/2015 2:02:00 PM ####
As a piece of history, we proposed a variation on compound types for C# and .NET many moons ago (in 1999) http://blogs.msdn.com/b/dsyme/archive/2012/07/05/more-c-net-generics-history-the-msr-white-paper-from-mid-1999.aspx :)
Do you want "I1 & I2" to be a first-class type?
Don Syme, F# Language Evolution


#### Comment by Don Syme on 2/3/2016 3:04:00 PM ####
I'm inclined to decline this. While I appreciate the logic of compound types it doesn't seem to add enough to the F# language design to do this, given the lack of votes here and the complexity it will inevitable bring.

