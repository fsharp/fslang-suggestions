# Allow match! in async workflows [8169411] #

**Submitted by Anonymous on 5/30/2015 12:00:00 AM**  
**32 votes on UserVoice prior to migration**  

Instead of writing:
async {
let! m fetch_something()
match m with
| ...
}
it would be nice to write
async {
match! fetch_something() with
| ...
}



## Response ##
** by fslang-admin on 2/3/2016 12:00:00 AM **

Closing per my comment below


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/8169411)**


## Comments ##


#### Comment by Anonymous on 6/1/2015 9:01:00 AM ####
Is this different from Joinads?
/archive/suggestion-5663965-integrate-joinads-extension


#### Comment by Don Syme on 6/9/2015 12:56:00 PM ####
@Anonymous - yes, it is different (and much simpler)


#### Comment by George on 6/10/2015 10:37:00 AM ####
Nice.


#### Comment by exercitus vir on 6/12/2015 8:13:00 PM ####
Yes, this consistent with the other keywords.


#### Comment by Don Syme on 7/17/2015 6:42:00 AM ####
We considered this in the F# language design but declined it, partly because of the possibility to reserve the syntax for the joinad feature.
If we did something in this area it would probably be to allow an "await" or "bind" at any point in the non-higher-order (non-lambda) control-flow structure of an F# expression, for particular kinds of computation expressions which support rewriting to a local CPS style. However that is a larger feature than the one proposed here.

