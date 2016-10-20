# Allow Pattern Matching on Types [5664335] #

**Submitted by Craig Stuntz on 3/21/2014 12:00:00 AM**  
**20 votes on UserVoice prior to migration**  

I'm deserializing into abitrary record types and need to parse the deserialized values into appropriate types for the constructor. I'd like to do:
match parameterInfo.ParameterType with
| typeof<int> -> parseInt (attributes.[key]) :> obj
| typeof<string> -> attributes.[key]) :> obj
...etc
Unfortunately, this doesn't compile. A (somewhat messy) workaround is:
match parameterInfo.ParameterType with
| x when x = typeof<int> -> parseInt (attributes.[key]) :> obj
| x when x = typeof<string> -> attributes.[key]) :> obj
...etc.



## Response ##
** by fslang-admin on 9/16/2014 12:00:00 AM **

Declining per my comments, and also the comments from Craig. IMHO there is an adequate workaround for this that is clear, even if a little more explicit.
Don Syme, Current BDFL F# Language/Library Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5664335)**


## Comments ##


#### Comment by Don Syme on 3/21/2014 12:50:00 PM ####
My feeling is that the "x = ..." is adequate - this makes it clear that what's really going on is an equality check.
Adding typeof<...> as a pattern may lead to false expectations that you can do things like "typeof<list<_>>" to match any list type.


#### Comment by Richard Minerich on 3/21/2014 4:35:00 PM ####
You could easily make an active patten for this.


#### Comment by Craig Stuntz on 3/21/2014 8:15:00 PM ####
Richard, I considered an active pattern, but it seemed less readable than the workaround above, insofar as it at least includes the real type, typeof<int>, instead of a wrapper for same.
Don's question is interesting. Should that work? I can see arguments both for and against.


#### Comment by Jon Harrop on 3/27/2014 5:34:00 AM ####
My serialization library does a lot of this to dissect values. I tried using active patterns but you quickly run out of 7 choices when you're looking at byte, char, int, float, decimal, string, arrays, lists, sets, maps and dictionaries. So I used a union type with "System.Type"s in it to perform one level of dissection via a separate function. Then you can match over the available types easily.


#### Comment by Mastr Mastic on 4/4/2014 1:26:00 AM ####
I agree with Don, but only because this instance isn't an extremely reoccurring one.
I also agree it would be nice to have this feature though.


#### Comment by Craig Stuntz on 7/5/2014 9:17:00 PM ####
Travis Brown pointed out tonight (on Twitter) that this feature, which is available in Scala, is "too easy" and is widely abused. I tend to agree, especially in a hybrid language with OO features. I still think it's the right answer for the specific example I gave, but I do agree the potential for abuse is high. I'm not sure how to rectify those two, conflicting opinions.


#### Comment by George on 12/10/2015 7:51:00 PM ####
typeof<> and typedefof<> are constants for non-generics. This fact alone should make them available as match targets. To keep form with F#, perhaps uppercased versions could be coined: TypeOf and TypeDefOf, respectively. In any event, the present work around breaks simplicity. The types in a program are a constant finite set.

