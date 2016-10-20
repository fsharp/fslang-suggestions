# Add reverse pipe operator that is right associative and low precedence. [6135254] #

**Submitted by Mårten Rånge on 7/4/2014 12:00:00 AM**  
**9 votes on UserVoice prior to migration**  

The current reverse pipe (<|) is left-associative and same precedence.
Left-associativity is "unnatural" for reverse pipe making it's usage harder, ie this doesn't compile: let x = abs <| abs <| 2;
In addition sharing the precedence of |> makes mixing them harder.
There are already existing languages with such an operator ie Haskell and operator '$'.
I propose adding a right-associative low precedence reverse pipe operator to F# in order to improve reverse-piping.
I know some people disagree with reverse-piping but I personally like it as it can be used to remove parantheses. To me excessive amount of paratheses makes code harder to read (I guess this is the reason I struggle to enjoy LISP).



## Response ##
** by fslang-admin on 2/5/2016 12:00:00 AM **

Thanks for the suggestion, though I’m declining per my comment below.
Many thanks,
Don Syme, F# Language and Core Library Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6135254)**


## Comments ##


#### Comment by Mårten Rånge on 7/4/2014 1:18:00 PM ####
For the interested I a PR as a proposal: https://visualfsharp.codeplex.com/SourceControl/network/forks/marten_range/visualfsharp/contribution/7074


#### Comment by Don Syme on 2/5/2016 5:02:00 AM ####
This can always be added as an operator outside the core library.
I must admit I'm not a fan of encouraging the widespread use of reverse piping beyond a single "f <| x" It seems to me that reverse piping supporting a single function is reasonable but the other cases tend to code obscurity.
I will decline this since we don't plan to add such an operator to FSharp.Core, and because you can define an operator outside the core library in your own implementation code.

