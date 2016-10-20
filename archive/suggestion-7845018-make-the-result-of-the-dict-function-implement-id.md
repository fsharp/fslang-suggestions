# Make the result of the dict function implement IDictionary [7845018] #

**Submitted by Richard Minerich on 5/6/2015 12:00:00 AM**  
**21 votes on UserVoice prior to migration**  

The fact that the type returned by dict doesn't implement IDictionary makes reflection difficult and inefficient, it also make this type different than all other .NET Core Dictionary implementations



## Response ##
** by fslang-admin on 7/17/2015 12:00:00 AM **

This is approved for inclusion in a future release of the F# core library subject to an implementation and detailed design. Completion of the pull request to implement this feature will be necessary, see the link above.
Don Syme, F# Language and Core Library Evolution.


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/7845018)**


## Comments ##


#### Comment by Paul Westcott on 5/10/2015 9:49:00 PM ####
IReadOnlyDictionary<_,_> as well would be good.


#### Comment by Steffen Forkmann on 5/11/2015 5:18:00 AM ####
I tried to implement this at https://github.com/Microsoft/visualfsharp/pull/436

