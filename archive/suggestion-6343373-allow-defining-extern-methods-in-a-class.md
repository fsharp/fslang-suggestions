# Allow defining extern methods in a class [6343373] #

**Submitted by Kevin Jones on 8/25/2014 12:00:00 AM**  
**3 votes on UserVoice prior to migration**  

Currently it appears that extern methods for platform invoke only work properly when used inside of a module (see this discussion: http://stackoverflow.com/questions/22275072/why-does-the-f-compiler-give-an-error-for-one-case-but-not-the-other) this limitation poses problems when organizing your code in an efficient manner and results in having multiple modules defined (for an example, see here: http://stackoverflow.com/questions/25004314/working-with-safehandles-in-f)
It would be nice if extern methods could be defined in classes (and work correctly) even if the scope of the method is always limited to the type itself.



## Response ##
** by fslang-admin on 8/3/2015 12:00:00 AM **

This is now “approved in principle” for some version of F# 4.x or beyond. It is entirely reasonable to eventually allow this for F#.
However, because there is a workaround (using a module), and because the implementation and testing is a little complicated, involving new code paths, it may be that the feature is not seen as high priority. Only a fully implemented and tested feature would be accepted.
Implementations of approved language design items can now be submitted as pull requests to the appropriate branch of http://github.com/Microsoft/visualfsharp. See http://fsharp.github.io/2014/06/18/fsharp-contributions.html for information on contributing to the F# language and core library.
Don Syme, Current BDFL for F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6343373)**


## Comments ##

