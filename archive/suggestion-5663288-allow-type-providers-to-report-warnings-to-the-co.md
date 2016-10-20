# Allow type providers to report warnings to the compiler [5663288] #

**Submitted by Gustavo Guerra on 3/21/2014 12:00:00 AM**  
**11 votes on UserVoice prior to migration**  





## Response ##
** by fslang-admin on 8/3/2015 12:00:00 AM **

This is approved-in-principle for F# 4.x+
A detailed design is needed. I would prefer one that is idiom-based and doesn’t force type providers to use a later FSharp.Core.dll
Implementations of approved language design items can now be submitted as pull requests to the appropriate branch of http://github.com/Microsoft/visualfsharp. See http://fsharp.github.io/2014/06/18/fsharp-contributions.html for information on contributing to the F# language and core library.
Don Syme, F# Language and Core Library Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5663288)**


## Comments ##


#### Comment by Gustavo Guerra on 6/28/2014 1:26:00 PM ####
Maybe if the class that implements ITypeProvider has a public event named "WarningGenerated" or something like that, the compiler could plug into it and listen. It's a bit hack-y, but as there is a canonical implementation of ITypeProvider in TypeProviderForNameSpaces, we could create a method there called "EmitWarning", and hide how it's implemented, so there would not be a requirements for a specific FSharp.Core.
Unfortunately, I'm not remembering the case I was thinking about that I wanted to generate a warning on. I think it was in CsvProvider, but can't remember exactly


#### Comment by exercitus vir on 6/19/2015 6:01:00 PM ####
I also think that this would allow for many more interesting use cases for type providers.

