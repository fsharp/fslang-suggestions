# Allow type providers to affect update-check [7090613] #

**Submitted by Robert Jeppesen on 2/13/2015 12:00:00 AM**  
**2 votes on UserVoice prior to migration**  

In short, if a TP uses a file, and that file changes, the needs-update check has no way of knowing to rebuild the project.
Some suggestions here: https://github.com/Microsoft/visualfsharp/issues/234



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/7090613)**


## Comments ##


#### Comment by Don Syme on 7/18/2015 1:20:00 PM ####
Looking at the original issue, @latkin confirmed that using the "Content" item type should solve things. If that's not the case please add more detail to that issue.

