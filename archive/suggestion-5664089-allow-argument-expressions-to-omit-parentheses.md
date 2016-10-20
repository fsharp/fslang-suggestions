# Allow argument expressions to omit parentheses [5664089] #

**Submitted by Stephen Swensen on 3/21/2014 12:00:00 AM**  
**24 votes on UserVoice prior to migration**  

For example, given let f x y = x + y, currently we must do
f ("hello".ToString()) ("world".ToString())
but it would be nice if we could omit the parenthesis:
f "hello".ToString() "world".ToString()
I understand that method application was deliberately weakened in the presence of functional application because it was thought that there would be confusion between application of tuples and application of method calls. But I believe that in practice this confusion does not exist and the majority of F# programmings would find omitting the parenthesis more natural and pleasant.



## Response ##
** by fslang-admin on 2/5/2016 12:00:00 AM **

Thanks for the suggestion. It has been marked declined, please see my comment
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5664089)**


## Comments ##


#### Comment by Jon Harrop on 3/21/2014 11:48:00 AM ####
So:
f("hello").ToString()
would have different meanings if "f" was a function or a member?


#### Comment by Loic Denuziere on 3/21/2014 11:49:00 AM ####
I think making this depend on the presence of a space between the method name and the opening parenthesis would make sense. It would be consistent with `foo().bar()` vs `foo ().bar()` (the first succeeds, the second fails saying that unit has no method bar).


#### Comment by Don Syme on 3/21/2014 12:40:00 PM ####
To be clear, what is being proposed is to allow high precedence application in argument position, specifically to remove the restriction here: https://github.com/fsharp/fsharp/blob/master/src/fsharp/pars.fsy#L3139

if hpa2 then reportParseErrorAt ...


#### Comment by Don Syme on 2/5/2016 9:37:00 AM ####
Tomas Petricek and I talked this over as part of reviewing issues. We decided to finally mark this as "declined". While the suggestion makes total sense, we feel that the code that would result is just too subtle - a single space can make a huge difference. Tomas pointed out that "f -3" already confuses people. If that's the case, this would be even more so.
Many thanks for the suggestion though, it is definitely interesting that this would be a feasible design point.

