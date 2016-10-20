# Revert the access modifier on FSharpFunc<T, TResult> constructor to be protected again. [14266899] #

**Submitted by Mikkel Christensen on 5/27/2016 12:00:00 AM**  
**1 votes on UserVoice prior to migration**  

It has been changed to public in 4.4, which is a rather odd construct for an abstract class.



## Response ##
** by fslang-admin on 6/13/2016 12:00:00 AM **

Declined per my comment below
Don Syme
F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/14266899)**


## Comments ##


#### Comment by Don Syme on 6/13/2016 5:50:00 AM ####
I don't particularly recall why this change was made, but I don't think we'll change it back now for the sake of stability.

