# Allow all inferrable SRTP constraints to be written in signatures [7887270] #

**Submitted by Don Syme on 5/9/2015 12:00:00 AM**  
**14 votes on UserVoice prior to migration**  

See https://github.com/Microsoft/visualfsharp/issues/392. Basically F# will in some situations infer statically-resolved-constraints like
(A or ^b) : (static member X : ...)
where A is a concrete class name. However these constraints can't be written in signatures. It is reasonable to lift this restriction



## Response ##
** by fslang-admin on 8/2/2016 12:00:00 AM **

Completed https://github.com/fsharp/FSharpLangDesign/blob/master/RFCs/FS-1017-fix-srtp-constraint-parsing.md
Further comments, use cases, information and discussion welcome
Don Syme, F# Language and Core Library Evolution.


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/7887270)**


## Comments ##


#### Comment by Mark Laws on 5/9/2015 7:43:00 AM ####
BTW, the real problem is that it's not just in signature files; it can make it hard to write the necessary constraints for actual code too.


#### Comment by Mark Laws on 6/22/2016 9:22:00 AM ####
PR made for RFC 1017 to track this issue: https://github.com/fsharp/FSharpLangDesign/pull/103

