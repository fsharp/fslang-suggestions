# Allow F# compiler directives like #nowarn to span less than an entire file. [6085102] #

**Submitted by Robert Nielsen on 6/22/2014 12:00:00 AM**  
**7 votes on UserVoice prior to migration**  

Idea posted here:
http://visualstudio.uservoice.com/forums/121579-visual-studio/suggestions/3338653-allow-f-compiler-directives-like-nowarn-to-span
A possibly related issue / suggestion is listed here:
/archive/suggestion-5676502-disable-compiler-warnings-per-line



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6085102)**


## Comments ##


#### Comment by exercitus vir on 6/19/2015 5:32:00 PM ####
You could use #endnowarn "[number]" to explicitely end a compiler directive.


#### Comment by Mark Seemann on 5/29/2016 2:11:00 AM ####
In C#, this feature exists, and has the following form:
#pragma warning disable 618
code...
#pragma warning enable 618
This enables you to suppress specific compiler warnings locally, which is quite important for evolving APIs: sometimes you need to deprecate a particular API (function, type), but keep it around for backwards compatibility. This means that your own code may still need to use the deprecated code for a while longer (for e.g. unit tests), so it'd be nice to enable that scenario without suppressing all other warnings.

