# Enable compression of FSharp.Core.dll with --standalone [9472671] #

**Submitted by Anonymous on 8/24/2015 12:00:00 AM**  
**4 votes on UserVoice prior to migration**  

Currently when one uses the --standalone+ option with fsc, all the binaries required to run the program (from a F# perspective, not including CLR) are pulled into the main target. This includes FSharp.Core.dll, which weighs in at 1.4MB, this is due to a large amount of strings, and compressing FSharp.Core.dll with 7ZIP yields a footprint of 319KB, which is significantly less overhead.
I propose that the --standalone command line should be equipped with the ability to compress binaries, perhaps --standaloneCompress.



## Response ##
** by fslang-admin on 2/3/2016 12:00:00 AM **

See comment – please use another tool such as ILMerge, and/or contribute to that tool if it doesn’t have required functionality.
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/9472671)**


## Comments ##


#### Comment by Don Syme on 2/3/2016 11:13:00 AM ####
You should be able to use ILMerge or other tools instead, which I believe have options for slicing out only the functionality that is used.

