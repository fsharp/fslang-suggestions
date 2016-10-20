# Internationalized printf formatting of numbers [6063696] #

**Submitted by Goswin on 6/17/2014 12:00:00 AM**  
**8 votes on UserVoice prior to migration**  

Most non-english speaking countries use "," as deciamal separator.
it would be nice if I could write <sprintf "%,1f" 2.222> instead of <sprintf "%.1f" 2.222> to get a comma as a decimal separator.



## Response ##
** by fslang-admin on 8/3/2015 12:00:00 AM **

This is a reasonable suggestion. From the point of view of the F# language design, I would be happy to see a well-considered set of extensions to printf added to F# 4.x or later versions.
An implementation and testing would need to be provided by someone in the F# community (possibly including Microsoft or Microsoft Research, though not limited to them).
We would strongly welcome an implementation proposal and initial testing for this.
Implementations of approved language design can now be submitted as pull requests to the appropriate branch of http://github.com/Microsoft/visualfsharp. See http://fsharp.github.io/2014/06/18/fsharp-contributions.html for information on contributing to the F# language and core library..
Thanks
Don Syme, F# Language and Core Library Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6063696)**


## Comments ##


#### Comment by Don Syme on 6/20/2014 6:40:00 AM ####
This is a reasonable suggestion. From the point of view of the F# language design, I would be happy to see a well-considered set of practical extensions to printf added to F# 4.0 or later versions. This could be one of them.
An implementation and testing would need to be provided by someone in the F# community (possibly incuding Microsoft or Microsoft Research, though not limited to them).Currently, initial implementations of approved language design can be submitted as pull requests to the "fsharp4" branch of https://visualfsharp.codeplex.com/SourceControl/latest.
If provided, the design should be
- analyzed and extended with respect to a broader set of potential non-english-speaking numerical formats
- sent for community discussion, for example by adding a link to a more detailed proposal to the end of this post, or by submitting a concrete implementation
Thanks
Don Syme, current "BDFL" for F# Language Design


#### Comment by Don Syme on 6/25/2014 12:04:00 PM ####
Adjusted the title to match my earlier comment


#### Comment by Goswin on 6/30/2014 3:56:00 AM ####
related:
http://stackoverflow.com/questions/21462617/how-to-get-culture-aware-output-with-printf-like-functions

