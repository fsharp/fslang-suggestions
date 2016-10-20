# Disable compiler warnings per line [5676502] #

**Submitted by Steven Taylor on 3/25/2014 12:00:00 AM**  
**2 votes on UserVoice prior to migration**  

Over time, the value of warnings get noisy and their value goes down if there's not a simple way to partition them into "as intended" and "could be a problem" buckets. Also, it would be good to ignore the "as intended" ones (is there a better way to do this than introduce an ugly pragma?).
Example: a warning pops up such as "This construct causes code to be less generic than indicated by...", you investigate, and determine that this is intentional. Normally you would not allow the way the doSomething function works, but in this case it is succinct, and you think an okay way to proceed given <insert situation & context here> .



## Response ##
** by fslang-admin on 2/3/2016 12:00:00 AM **

Close enough to being a duplicate of /archive/suggestion-6085102-allow-f-compiler-directives-like-nowarn-to-span


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5676502)**


## Comments ##


#### Comment by Robert Nielsen on 6/22/2014 10:49:00 AM ####
I have posted a vaguely related suggestion: /archive/suggestion-6085102-allow-f-compiler-directives-like-nowarn-to-span


#### Comment by exercitus vir on 6/19/2015 6:03:00 PM ####
This is related: /archive/suggestion-6085102-allow-f-compiler-directives-like-nowarn-to-span


#### Comment by Don Syme on 2/3/2016 2:35:00 PM ####
Closing as duplicate in favour of /archive/suggestion-6085102-allow-f-compiler-directives-like-nowarn-to-span

