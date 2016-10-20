# FSI #I directive to add path to process path environment variable [5821261] #

**Submitted by Christoph Rüegg on 4/23/2014 12:00:00 AM**  
**5 votes on UserVoice prior to migration**  

If a managed assembly that uses native DLLs with p/invoke is referenced in F# Interactive using #r and #I directives, using them may fail with a DllNotFoundException even if the native assembly is in the same folder as the managed one and the folder has been included using the #I directive. Note that it is not possible to reference native DLLs explicitly in .Net.
Suggestion: make the #I directive automatically add the specified path also to the process-local Path environment variable, this way it would help not only resolving managed but also native assemblies.
Windows only; loading libraries is quite different in Linux.
Original ticket with more details: https://github.com/fsharp/fsharp/issues/164



## Response ##
** by fslang-admin on 2/5/2016 12:00:00 AM **

Thanks for the suggestion! Declining per my comment below.
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5821261)**


## Comments ##


#### Comment by Don Syme on 2/5/2016 6:44:00 AM ####
It seems you can work around this by adding to the path manually. I think I would prefer to keep that as the solution rather than making implicit changes to the path.

