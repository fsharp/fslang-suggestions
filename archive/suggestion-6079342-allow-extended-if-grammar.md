# Allow extended #if grammar [6079342] #

**Submitted by Don Syme on 6/20/2014 12:00:00 AM**  
**6 votes on UserVoice prior to migration**  

Allow an extended grammar for #if/#elif.
#if expr
#elif expr
with grammar:
expr =
| expr && expr
| expr || expr
| not expr
| (expr)
| IDENT
With usual precedences. The syntax !IDENT should also be parsed and interpreted as “not”, though a warning given that “not” should be used instead in F# code.
The implementation must also provide sufficient tests.



## Response ##
** by fslang-admin on 1/21/2015 12:00:00 AM **

Completed for F# 4.0+ see https://github.com/Microsoft/visualfsharp/pull/55
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6079342)**


## Comments ##


#### Comment by Don Syme on 6/20/2014 12:22:00 PM ####
I consider this approved in principle, though details may need to be sorted out.
If you think this should not be done, please chime in with details below.
If you have specific questions on the design, please chime in below.
An implementation and testing would need to be provided by someone in the F# community (possibly including Microsoft or Microsoft Research, though not limited to them).Currently, initial implementations of approved language design can be submitted as pull requests to the "fsharp4" branch of https://visualfsharp.codeplex.com/SourceControl/latest. F# 4.0 is open for business.
I encourage you to work towards an implementation and testing for this feature.
Don Syme, current BDFL, F# Language

