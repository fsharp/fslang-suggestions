# Add new expression like ForIntegerRangeLoop but with step value [6405857] #

**Submitted by Alfonso Garcia-Caro on 9/7/2014 12:00:00 AM**  
**1 votes on UserVoice prior to migration**  

I guess there is a good reason that Expr.ForIntegerRangeLoop doesn't have a step argument, but I wonder why downto loops are not allowed in quotations. This could be also useful to optimize loops like:
for i in 0 .. 2 .. 10 do



## Response ##
** by fslang-admin on 9/16/2014 12:00:00 AM **

This suggestion is being declined for FSharp.Core itself because the primitive quotation forms supported are “fixed” and won’t be changed for backwards compatibility reasons.
However it is possible to add new Expr.* and DerivedPatterns.* functions and/or active patterns to create and/or detect additional derived constructs.
It is possible a library of these routines should be developed and share between the F# community.
Don Syme, Current BDFL F# Language/Library Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6405857)**


## Comments ##


#### Comment by Alfonso Garcia-Caro on 9/16/2014 11:23:00 AM ####
Thanks for reviewing the suggestion, Don. I was afraid that quotations couldn't be touched but I appreciate a lot your comment. I'll work in the direction you suggest and when I get satisfactory results, I'll share it with the community.
Cheers!

