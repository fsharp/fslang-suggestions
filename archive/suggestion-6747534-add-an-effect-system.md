# Add an effect system [6747534] #

**Submitted by Anonymous on 11/20/2014 12:00:00 AM**  
**17 votes on UserVoice prior to migration**  

https://www.cl.cam.ac.uk/~dao29/publ/haskell14-effects.pdf
Embed the ideas in this paper, but in F# instead of Haskell. I am pretty sure one of the authors is familiar with F#.



## Response ##
** by fslang-admin on 2/4/2016 12:00:00 AM **

Declined per my comment below
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6747534)**


## Comments ##


#### Comment by Richard Gibson on 12/3/2014 5:19:00 AM ####
Similar to StackOverflow, I feel that here you should post a summary of the idea, not just a link to something else (considering your link is to a whole paper, very few people will actually read it and therefore know what you're proposing).


#### Comment by Anonymous on 12/3/2014 10:42:00 AM ####
Thanks for the comment -- good point. To be fair to myself, I will not do the paper justice so was trying to avoid misrepresenting, but I will try to explain what it is that I want from this feature:
The Type System provides some information about what a function or expression does, but it currently does not describe everything that it does. Some functions have *side effects* and it is possible to embed those into the type system, or to enhance the type system with an effects system that keeps an honest accounting of what side effects might be happening.
The most well known example of a similar concept is checked exceptions in Java, although that is probably not a ringing endorsement.
The effects that you would be interested in would be exceptions, divergence, IO (or as Tomas has pointed out) a more granular view of IO, allocations, reads and writes (also see http://tomasp.net/blog/2014/update-monads/index.html for some details on a monad for something like this).
The key idea is that we can get some more honesty out of the type system by also tracking what the possible effects that a function might produce. We can then isolate Pure or Total code from code that we want to be at the boundaries.
See also http://research.microsoft.com/en-us/projects/koka/ for a Microsoft implementation of a similar idea.
One argument against would be that much of the BCL would be a hot mess of side effecting APIs. My strong suspicion is that adding an effects system would help to put pressure on API designers to design better, more functional APIs.


#### Comment by Suminda Sirinath Salpitikorala Dharmasena on 12/7/2014 12:39:00 AM ####
+1 for this. I have run out of votes but would vote for this.


#### Comment by Phylos on 1/18/2015 12:45:00 AM ####
While this would certainly be a nice addition to the language, the amount of effort and resources required would probably best be directed elsewhere. I would think it would be much more valuable to have the relatively limited resources available for core F# language development add type classes and higher kinds to the language. Such powerful additions would provide the basic building blocks to take F# to the next level.


#### Comment by Greg Rosenbaum on 3/14/2015 4:04:00 PM ####
This feature already exists in F*, which is an experimental language designed for proofs and verification of computer programs. The language is based on F#. Here is a tutorial on the language:
https://www.fstar-lang.org/tutorial/
Note that I don't support this feature, since I feel it's unnecessary. I'd really rather they added higher kinds and maybe type classes. I'm just telling you the code already exists.


#### Comment by Don Syme on 2/4/2016 11:26:00 AM ####
I agree with Phylos and others that adding an effect system is beyond the scope of F# as things stand, except in purely research/experimental versions (which as a researcher I'd love to play with!). See also my comments on dependent types, /archive/suggestion-6062821-add-dependent-types
Note that a Rust-like effect/ownership system aimed at the specific problem of data races in concurrent programs is listed as a separate suggestion: /archive/suggestion-6972958-mezzo-rust-like-features-for-f-code-to-be-data-ra (but would also be a huge undertaking)

