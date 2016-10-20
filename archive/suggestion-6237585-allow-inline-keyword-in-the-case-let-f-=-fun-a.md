# Allow "inline" keyword in the case "let f = fun a -> ..." [6237585] #

**Submitted by Yusuf Motara on 7/31/2014 12:00:00 AM**  
**3 votes on UserVoice prior to migration**  

Currently, the code "let inline f = fun a -> ..." does not compile, but the code "let inline f a = ..." does compile. Since the two mean the same thing, "inline" should be allowed on both.



## Response ##
** by fslang-admin on 7/11/2016 12:00:00 AM **

This is approved for inclusion in a future release of F# subject to completion of an RFC and implementation.
An RFC can be submitted to https://github.com/fsharp/FSharpLangDesign/tree/master/RFCs
A pull request to implement this feature will be necessary and we encourage contributors to submit one with adequate design detail and testing to http://github.com/Microsoft/visualfsharp.
Discussion of the particular version for this to be included in can be made once an implementation is available.


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6237585)**


## Comments ##


#### Comment by amazingant on 3/21/2015 9:01:00 PM ####
Posted an issue on the fsharp/FSharp.Compiler.Service repository over on GitHub here:
https://github.com/fsharp/FSharp.Compiler.Service/issues/315
Don Syme suggested either moving it to the Microsoft/VisualFSharp repository as a bug or posting it as a feature request here, and seeing as it's already mentioned here, I'll tag along for the ride.
Adding my +3 for the time-being :)


#### Comment by exercitus vir on 5/21/2015 5:09:00 PM ####
I have the exact same problem (also inspired by your suggestion in the comments on Haskell-style type annotations).
I feel that this is a bug - not a feature request - because it is valid syntax and compiles to exactly the same code as the more standard 'let inline f a = ...'.


#### Comment by exercitus vir on 5/21/2015 5:36:00 PM ####
I've also posted this as a bug on https://github.com/Microsoft/visualfsharp/issues/467


#### Comment by Don Syme on 7/18/2015 1:30:00 PM ####
This is not something I see as a priority (because there is an adequate way of working around the problem), but a pull request (with adequate testing etc.) that implements this could well be accepted, assuming no gotchas are found along the way.


#### Comment by Don Syme on 7/11/2016 8:15:00 AM ####
I'm changing this to be marked as "approved". This means someone can propose a PR for the issue. PRs should be submitted to http://github.com/Microsoft/visualfsharp.

