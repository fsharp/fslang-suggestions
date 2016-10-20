# add Async.Choice to FSharp.Core [10575069] #

**Submitted by Steffen Forkmann on 11/6/2015 12:00:00 AM**  
**12 votes on UserVoice prior to migration**  

Async.Choice is super useful (e.g. very important in Paket) but hard to implement. There are couple of implementations floating around like http://www.fssnip.net/dO but it's ahrd to decide which one is correct. We should add it to the core.



## Response ##
** by fslang-admin on 1/23/2016 12:00:00 AM **

Approved and completed, though not yet in any specific public release of F#.
PR https://github.com/Microsoft/visualfsharp/pull/744 completed.
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/10575069)**


## Comments ##


#### Comment by Eirik George Tsarpalis on 11/6/2015 4:38:00 AM ####
Btw, the implementation of http://www.fssnip.net/dO is flawed. I would consider using http://www.fssnip.net/dN instead.


#### Comment by Steffen Forkmann on 11/6/2015 4:41:00 AM ####
If I remember correctly that version didn't work in paket since it doesn't cancel running http requests


#### Comment by Steffen Forkmann on 11/28/2015 4:48:00 AM ####
PR is at https://github.com/Microsoft/visualfsharp/pull/744

