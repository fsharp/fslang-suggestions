# Fix ReflectedDefinition for top-level pattern-matched let bindings [6475447] #

**Submitted by Loic Denuziere on 9/23/2014 12:00:00 AM**  
**9 votes on UserVoice prior to migration**  

Right now, when you do something like this:
[<ReflectedDefinition>]
let (a, b) = (1, 2)
The compiled result is roughly equivalent to:
let private generatedIdent = (1, 2)
[<ReflectedDefinition>] let a = fst generatedIdent
[<ReflectedDefinition>] let b = snd generatedIdent
As you can see, the actual expression (1, 2) doesn't get reflected. This makes such definitions unusable for most use cases of ReflectedDefinition. As far as I can tell, this could be fixed by simply adding a ReflectedDefinition of generatedIdent.



## Response ##
** by fslang-admin on 8/3/2015 12:00:00 AM **

I’ve marked this as approved for F# 4.x+.
An implementation and testing would need to be provided by someone in the F# community (possibly including Microsoft or Microsoft Research, though not limited to them). Currently, initial implementations of approved language design can be submitted as pull requests to the appropriate branch of http://github.com/Microsoft/visualfsharp. See http://fsharp.github.io/2014/06/18/fsharp-contributions.html for details on contributing to the F# language and core library.
Don Syme, F# Language and Core Library Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6475447)**


## Comments ##

