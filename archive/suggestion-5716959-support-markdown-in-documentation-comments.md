# Support markdown in documentation comments [5716959] #

**Submitted by Anonymous on 4/2/2014 12:00:00 AM**  
**19 votes on UserVoice prior to migration**  

F# currently supports documentation comments with either XML tags or no tags. The no tags format is convenient to write, but does not allow formatting the comments for the VS IDE. Use of XML tags allows formatting the documentation comment, but the act of writing the documentation comment becomes a heavy burden as XML is not a very convenient format for manual editing. I would like to suggest supporting some lighter-weight formatting syntax such as markdown.



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5716959)**


## Comments ##


#### Comment by Tomas Petricek on 4/3/2014 10:46:00 AM ####
The F# Formatting library (http://tpetricek.github.io/FSharp.Formatting/metadata.html) already partly lets you do this. It is not integrated with the compiler, so it won't work nicely in Visual Studio - but if someone added transformation that generates standard XML comments from the Markdown that we already parse, it would work nicely at least for libraries. There is even an open issue for this: https://github.com/tpetricek/FSharp.Formatting/issues/44
I think this is quite close - and with the transformation, you could document libraries with Markdown perfectly. But further integration with compiler would make it even nicer.


#### Comment by Mastr Mastic on 4/7/2014 10:48:00 AM ####
I would love this, and especially if the VS would support this in the IntelliSense tooltips.

