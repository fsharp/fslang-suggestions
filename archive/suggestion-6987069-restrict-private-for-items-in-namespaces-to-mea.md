# Restrict "private" for items in namespaces to mean "private to the namespace declaration group" #43 [6987069] #

**Submitted by Don Syme on 1/20/2015 12:00:00 AM**  
**4 votes on UserVoice prior to migration**  

For F# 2.x-4.0, as discussed in thie GitHub thread (https://github.com/Microsoft/visualfsharp/issues/43#issuecomment-70650925), a "private" module or type in a namespace is actually accessible from anywhere in that assembly contributing to the same namespace.
The suggestion is to emit a warning when such an item is accessed from outside the immediate namespace declaration group in which it is declared. For example, we would give a warning if it is accessed from another file in the same namespace in the same assembly.



## Response ##
** by fslang-admin on 7/17/2015 12:00:00 AM **

This problem should be fixed via a warning.
This is approved for inclusion in a future release of the F# language subject to an implementation and detailed design.
Don Syme, F# Language and Core Library Evolution.


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6987069)**


## Comments ##


#### Comment by Bryan Edds on 2/25/2016 4:43:00 PM ####
To help support abstract data types as explained here - https://vimeo.com/128464151 - and as discussed in a bug report here - https://github.com/Microsoft/visualfsharp/issues/984
I propose that we add one exception to the proposed rule, rendering it -
"Restrict "private" for items in namespaces to mean "private to the namespace declaration group" [except where functions are defined in a module with the same name as the type and in the same namespace.]"
We can create module with the same name as the type in namespace by using the [<CompilationRepresentation (CompilationRepresentationFlags.ModuleSuffix)>] attribute on the module, which is a common technique in F#.
This may seem like a minor exception, but it will keep from breaking code that heavily uses the above abstract data type style, such as here - https://github.com/bryanedds/Prime
- and here - https://github.com/bryanedds/NuGameEngine

