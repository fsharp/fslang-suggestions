# Code clarity: To change the default value returned by function Unchecked.defaultof<string> to "" from null [12882690] #

**Submitted by Alexei Odeychuk on 3/10/2016 12:00:00 AM**  
**2 votes on UserVoice prior to migration**  

I suggest changing the default value returned by function Unchecked.defaultof<string> to "" from null. I think the function should return a value of type string indicating an empty string "" as expected by a majority of language users who writes string processing code.
Null indicates that there is no value at all.
I am inclined to think from my own experience that null returned by Unchecked.defaultof<string> leads to unnecessary complications in the code dealing with value names of type string, namely in the form of mandatory checks both for "" and null, instead of a check for "" only in situations when you expect to encounter an empty string.
The change suggested in the F# language will allow writing more simple and clear code for string processing.



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/12882690)**


## Comments ##


#### Comment by Dax Fohl on 3/25/2016 12:16:00 PM ####
This would be a breaking change and would break the "principle of least surprise" for anyone coming from C#. I see the value but don't see this ever happening.


#### Comment by Richard Gibson on 4/13/2016 9:29:00 AM ####
Although I get where you're coming from, I don't think that changing what Unchecked.defaultof<> does is a good idea because: (a) it's a breaking change and (b) it's the equivalent of default(T) in other .NET languages.
I'd love for F# to support the idea of types that have a sensible default value (such as "" for strings, 0 for ints, [] for lists) but I don't know how you'd do it without support for higher kinds first.
Note: We *sort of* have this with static type member constraints, but unfortunately there's no common member name from .NET type to .NET type. Int defines 'Zero' (through F# extensions), String defines 'Empty', and I'm not sure if Array defines anything at all.

