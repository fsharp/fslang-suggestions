# Add a way to prevent async execution at compiletime [9129526] #

**Submitted by Metastatic on 8/1/2015 12:00:00 AM**  
**3 votes on UserVoice prior to migration**  

There are sometimes operations such as COM that don't play very well with threading. It would be nice if there was a way to denote that a function is not threadsafe and cannot be used from within a thread. e.g. if someone tries to use parallel a compile error would show up indicating that the function cannot be used from within a thread.



## Response ##
** by fslang-admin on 9/7/2015 12:00:00 AM **

Many thanks for the suggestion
Declining this as it is not a specific design proposal, so it’s difficult to know what’s being voted on.
If you’d like to re-propose, please resubmit with a more detailed description of the problem with examples and/or a more concrete design proposal.
Don Syme
F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/9129526)**


## Comments ##


#### Comment by Fyodor Soikin on 8/9/2015 5:37:00 PM ####
What do you mean by "within a thread"? All code execution happens on _some_ thread. So if a particular function was prohibited from executing "within a thread", it could not be executed at all.

