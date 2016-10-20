# Allow TypeProviders to supply location with errors [6531829] #

**Submitted by Robert Jeppesen on 10/7/2014 12:00:00 AM**  
**6 votes on UserVoice prior to migration**  

When a custom type provider fails, the type provider will typically throw, there is not much else to do.
I suggest to add the ability to add an error location when something fails. This would allow to pinpoint with squigglies where the error is in ie json/sql/whatever.
Perhaps the simplest non-breaking implementation would be to add a known exception type that contains a file location and a range. So the TP still just throws, but adds this information where possible.



## Response ##
** by fslang-admin on 8/3/2015 12:00:00 AM **

Approved in principle for F# 4.0 (or later, depending), along with “allow type providers to report warnings”. subject to a suitable implementation being submitted. Both are entirely reasonable
Implementations of approved language design items can now be submitted as pull requests to the appropriate branch of http://github.com/Microsoft/visualfsharp. See http://fsharp.github.io/2014/06/18/fsharp-contributions.html for information on contributing to the F# language and core library.
Don Syme, F# Language/Library evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6531829)**


## Comments ##


#### Comment by ADMIN
fsharporg-lang (F# Software Foundation Language Group, F# Software Foundation) on 10/30/2014 6:58:00 AM ####
See also this proposal /archive/suggestion-5663288-allow-type-providers-to-report-warnings-to-the-com, these should probably be combined

