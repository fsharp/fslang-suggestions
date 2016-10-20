# Make Set.count O(1) [12880410] #

**Submitted by Zhen on 3/10/2016 12:00:00 AM**  
**3 votes on UserVoice prior to migration**  

Seems easy to track items when they are added and removed



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/12880410)**


## Comments ##


#### Comment by Robert Pickering on 3/11/2016 3:28:00 PM ####
Sadly, not as straight forward as it sounds, since set also support filter and partition as well as add. filter and partition work directly on the SetTree type that represents set internally, so these operation would need to return the new count. It could be done, but the question is should it be done, as the extra over heads may out weight the perf gains from have Set.count O(1). Difficult call to make imho.


#### Comment by Jack Fox on 3/13/2016 12:08:00 PM ####
You are going to incur the cost somewhere. It's usually preferable to incur it when you request count.

