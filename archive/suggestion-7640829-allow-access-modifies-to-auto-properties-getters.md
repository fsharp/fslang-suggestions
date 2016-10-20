# Allow access modifies to auto properties getters and setters [7640829] #

**Submitted by Виктор Милованов on 4/21/2015 12:00:00 AM**  
**30 votes on UserVoice prior to migration**  

member val Property = 10 with get, private set



## Response ##
** by fslang-admin on 2/4/2016 12:00:00 AM **

Marked approved-in-principle, see comments. This won’t be high priority but is we get a quality PR for it we will accept it.


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/7640829)**


## Comments ##


#### Comment by ADMIN
fsharporg-lang (F# Software Foundation Language Group, F# Software Foundation) on 2/4/2016 5:39:00 PM ####
I'm fine with this suggestion. We considered it for F# 3.0 but cut it, since you can always implement this pattern in a more expanded form using "let" and explicit get/set.
It won't be high priority for myself, but if some one does it, that is great
Will mark this approved-in-principle (will show as "planned")

