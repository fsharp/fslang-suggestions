# F# interactive could support saving and loading its state to/from a file [8784865] #

**Submitted by Anonymous on 7/9/2015 12:00:00 AM**  
**9 votes on UserVoice prior to migration**  

It would be great to be able to do something like:
#save "CurrentState.dmp"
...
#restore "CurrentState.dmp"
It would be especially useful for interactive experimentation that deals with larger data



## Response ##
** by fslang-admin on 2/4/2016 12:00:00 AM **

Closing per my comment below., please take a read.
Don Syme, F# Language and Core Library Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/8784865)**


## Comments ##


#### Comment by Don Syme on 7/17/2015 5:54:00 AM ####
I don't know of any implementations of process checkpointing on Windows. See also https://en.wikipedia.org/wiki/Application_checkpointing


#### Comment by Don Syme on 7/17/2015 5:56:00 AM ####
I presume on Linux that existing process checkpointing techniques could be used, but it would be interesting to have it documented.
A state-serializing implementation based on the Nessos Vagabond library may be technically feasible, but only for a limited range of serializable data.


#### Comment by Don Syme on 2/4/2016 4:45:00 PM ####
I'm closing this because it's very hard to achieve in a cross-platform way, and out of scope for fsi.exe/fsharpi in the core tooling
However it would be totally reasonable to build a checkpointing fsharpi on Linux based on the F# Compiler Service, where you can build and design your own F# Interactive executable utilizing what is available in the FSharp.Compiler.Service DLL

