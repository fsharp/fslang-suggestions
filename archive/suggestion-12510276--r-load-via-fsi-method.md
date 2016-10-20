# #r #load via fsi method [12510276] #

**Submitted by Steven Taylor on 2/28/2016 12:00:00 AM**  
**1 votes on UserVoice prior to migration**  

fsi.Load("script.fsx")
fsi.Reference("bin/debug/someDllReference.dll")
It would be very useful to be able to fsi.Load / fsi.Reference through type providers, for use by those who are designing them.



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/12510276)**


## Comments ##


#### Comment by Don Syme on 2/29/2016 12:58:00 PM ####
While tempting, the problem is that type checking of a script would not detect these and so the static type checking of the script would not be possible.


#### Comment by Steven Taylor on 3/13/2016 7:00:00 PM ####
Is there a way to also dynamically insert into the static type checker?
In the spirit of exploratory programming, there are a range of useful cross .dll / tool chain workflows that this would enable. This would make it a more fluid experience. It would be quite useful for those who are new to whatever modelling domain it is. I've observed that the extra referencing exercise can be jarring to some programmers. Can provide additional use cases if of interest.
cheers.

