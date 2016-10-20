# Add support for implicit operators to facilitate language interop [5663709] #

**Submitted by Nelak on 3/21/2014 12:00:00 AM**  
**15 votes on UserVoice prior to migration**  

Add support for implicit operators to facilitate language interop instead of having to write an explicit operator like:
http://stackoverflow.com/questions/10719770/is-there-anyway-to-use-c-sharp-implicit-operators-from-f



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5663709)**


## Comments ##


#### Comment by Richard Minerich on 3/21/2014 4:51:00 PM ####
Please no, I don't want any implicit conversions ruining my type safety.


#### Comment by Daniel Fabian on 3/22/2014 3:22:00 AM ####
I agree, the work-around with a local operator using duck-typing seems like a small cost, when compared to losing the very strong typing we have right now.


#### Comment by Nelak on 3/22/2014 12:53:00 PM ####
I'm not proposing to relax strong typing but to add someway to ease language interop.
I don't see why we can't have something like an [<AllowImplicit>] that would be able to handle implicit operators without sacrificing type safety. In this way you need to opt-in for the desired behaviour
e.g.:
[<AllowNull>]
The null keyword is a valid keyword in the F# language, and you have to use it when you are working with .NET Framework APIs or other APIs that are written in another .NET language. The two situations in which you might need a null value are when you call a .NET API and pass a null value as an argument, and when you interpret the return value or an output parameter from a .NET method call.

