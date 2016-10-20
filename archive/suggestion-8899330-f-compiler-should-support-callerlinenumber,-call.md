# F# compiler should support CallerLineNumber, CallerFilePath etc [8899330] #

**Submitted by Weirong Zhu on 7/16/2015 12:00:00 AM**  
**15 votes on UserVoice prior to migration**  

.Net has attributes like CallerLineNumber, CallerFilePath (see MSDN https://msdn.microsoft.com/en-us/library/system.runtime.compilerservices.callerlinenumberattribute(v=vs.110).aspx). These are supported by C# compiler but not F# compiler. This seems to be an important feature to have. Especially when writing service components, the logging facility normally requires a compile-time approach to populate the file path and line number. In C/C++, this can be achieved by implementing the logging API using Macros. In C#, it can be done with CallerLineNumber, CallerFilePath attributes. There seems no viable approach in F#. Moreover, if there's an existing C# logging library that used CallerLineNumber attribute, such library cannot be taken advantage easily from F# (unless we passing __LINE__, __SOURCE_DIRECTORY__ and __SOURCE_FILE__ explicitly at every call site of logging API, which is tedious)



## Response ##
** by fslang-admin on 8/2/2016 12:00:00 AM **

Completed. RFC and link to pull request is here: https://github.com/fsharp/FSharpLangDesign/blob/master/RFCs/FS-1012-caller-info-attributes.md
This is an entirely reasonable recent .NET/C# standard to implement. Certainly, .NET object-type APIs using these attributes should be respected.
Don Syme, F# Language and Core Library Evolution.


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/8899330)**


## Comments ##


#### Comment by Lincoln Atkinson on 4/7/2016 12:17:00 PM ####
FYI - I am working on this feature as a project for the 2016 FSSF mentoring program with Avi Avni (@AviAvni3). Progress here: https://github.com/latkin/visualfsharp/tree/latkin-caller-info-attrs

