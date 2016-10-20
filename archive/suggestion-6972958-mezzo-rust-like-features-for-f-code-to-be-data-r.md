# Mezzo/Rust-like features for F# code to be data-race free [6972958] #

**Submitted by Don Syme on 1/16/2015 12:00:00 AM**  
**27 votes on UserVoice prior to migration**  

Languages like Mezzo, Rust and the M# language (internal to Microsoft) either have or are looking at adding type system features that track the status of references that give access to shared memory.
Shared-memory coding is less prevalent in F# because of its functional ans Async features, and because of powerful concurrency collections in the .NET class libraries.
However writing code with data-races is still possible when using mutable data.
There is a fairly large and non-trivial design space to addressing this problem, but some type-based techniques are starting to mature. If done "right" they can make writing high-performance concurrent, shared memory code "data-race free", that is, some F# code would be provably data-race free.
Given the design of F#, there would likely be "back doors" to this feature, especially when libraries are used. It's status would be somewhat like "Checked arithmetic".



## Response ##
** by fslang-admin on 2/10/2016 12:00:00 AM **

Declining per comment below – this was a placeholder and much more concrete suggestions would be needed!


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6972958)**


## Comments ##


#### Comment by Jonathan Protzenko on 1/17/2015 11:20:00 PM ####
Disclaimer: I am the author of Mezzo; I am also not proficient in F#, especially the internals of the type-checking algorithm.
Such an addition would be great; however, the way I see it, there are a few difficulties.
- There needs to be a way to easily opt-out of the extended checks. The type system may be very smart, but it will never cover all possible patterns. The user should be able to either use run-time checks (locks?) or assert statically "I know what I'm doing" and disable the extended checks, possibly locally.
- Somehow related to the first point, we should be careful about not contaminating other codebases. In our experience with Mezzo, we often witnessed a library offer a "strong" interface that enforces data-race freedom, only to see clients of this library struggle to use it. As long as there's a way to easily opt-out of the extended checks, this should not be an issue.
- Having an easy way to convert existing codebases is also key to success. Regardless of the technical means that underpin this feature, users should be able to convert codebases piecewise.
- Implementation-wise, this would probably require changes to the type-checker. I don't know if it is unification-based or uses a flow-sensitive type-checking algorithms. It may be easier to implement these checks in the latter case. There's also the question of whether this should be a separate analysis or directly implemented deep within the type-checker. We chose the latter option for Mezzo, but are still unsure whether the former might have been easier.
François and I wrote this paper where we recount the story of Mezzo and try to figure out what worked, what didn't, and what could've been done better <http://gallium.inria.fr/~fpottier/publis/fpottier-protzenko-lessons-mezzo.pdf>. Hopefully, there's some knowledge in there that may be useful.
I'll follow this topic and I'll happily answer more technical questions, if any :).


#### Comment by Phylos on 1/18/2015 12:12:00 AM ####
This sounds like it would be a wonderful addition to F#, helping to make it the language of choice for writing safe and robust software for the .NET platform.


#### Comment by Don Syme on 2/10/2016 11:23:00 AM ####
I'm going to decline this suggestion (which was made by me) because it is too vague.
More concrete proposals welcome!!

