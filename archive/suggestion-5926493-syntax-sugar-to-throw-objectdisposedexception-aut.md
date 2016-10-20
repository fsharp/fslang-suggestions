# Syntax sugar to throw ObjectDisposedException automatically [5926493] #

**Submitted by knocte on 5/14/2014 12:00:00 AM**  
**9 votes on UserVoice prior to migration**  

I know that F# is not the holy grail that would save us from the nonRAII/ResourceLeaks problems that are common in garbage-collected languages, but at least maybe it can help us cope with them?
I'm now thinking about those pesky times when we need to create an IDisposable object, and then we need to be careful to throw ObjectDisposedException in *every* method and property checking if the object has been disposed already. Doing this manually is very tedious and subject to failure, so having some syntax sugar in F# to do it automatically (so under the hood it generated the typical "mutable bool disposed" field, and checks it before every call to any member...). This way it will prevent people going the AOP route, which is usually painful.



## Response ##
** by fslang-admin on 6/24/2014 12:00:00 AM **

I’m declining this, see the comment.“My feeling is that it would not be right to special-case this specific functionality in F#. It would have to be a specific use-case of some more general language feature”
I’m sympathetic to this kind of proposal: detecting very common cases of idioms and adding support for them in the language, but the solutions to the problem have to be very general purpose with broad applicability.
Generalizations of the proposal are of interest, as are more examples.
Don Syme, F# Lang Design


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5926493)**


## Comments ##


#### Comment by Don Syme on 6/20/2014 11:49:00 AM ####
My feeling is that it would not be right to special-case this specific functionality in F#. It would have to be a specific use-case of some more general language feature.

