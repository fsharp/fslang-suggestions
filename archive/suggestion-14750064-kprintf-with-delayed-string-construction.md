# kprintf with delayed string construction [14750064] #

**Submitted by mk on 6/8/2016 12:00:00 AM**  
**10 votes on UserVoice prior to migration**  

Currently kprintf and friends take in a continuation function and a StringFormat and return a curried function that when applied builds the string.
It would be nice for logging frameworks to have an overload where the continuation does not build the string rather provides a delayed function to build the string.
That way I can do something like:
let public logWithFormat logLevel logFormat =
kprintf (fun stringBuilder -> if logLevel > currentLoggingLevel then sprintf "%s" (stringBuilder())) logFormat



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/14750064)**


## Comments ##


#### Comment by mk on 6/9/2016 4:31:00 AM ####
A related stack overflow thread with the same issue: http://stackoverflow.com/questions/31442608/how-to-wrap-sprintf-conditionally-in-f


#### Comment by Robin Munn on 7/13/2016 10:06:00 PM ####
If this is implemented, I'd suggest a name incorporating "d" for "delay", e.g. one of the following naming schemes:
dprintf, dbprintf, dfprintf, dsprintf
dkprintf, dkbprintf, dkfprintf, dksprintf
kdprintf, kdbprintf, kdfprintf, kdsprintf
kprintfd, kbprintfd, kfprintfd, ksprintfd
Personally, I like the last scheme best, where the "d" is appended at the end of the "normal" kprintf names. That fits with the printf / printfn function naming, where the two functions do ALMOST the same thing with one minor change (whether a newline is appended or not). Since no kprintf-family functions have an "n" overload, there won't be any confusion over whether to put the "d" before or after the "n", and the parallels to printf / printfn are clear (the "d" functions work almost the same as the non-"d" functions, but delay calling the continuation).

