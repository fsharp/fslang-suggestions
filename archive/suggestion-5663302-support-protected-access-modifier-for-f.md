# Support 'protected' access modifier for F# [5663302] #

**Submitted by Gustavo Guerra on 3/21/2014 12:00:00 AM**  
**98 votes on UserVoice prior to migration**  

Original item: http://visualstudio.uservoice.com/forums/121579-visual-studio/suggestions/2262739-support-protected-access-modifier-for-f



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5663302)**


## Comments ##


#### Comment by Jack Pappas on 3/22/2014 8:40:00 AM ####
This is one feature I'd really like to see in F#, and it seems like it should be very simple to implement. If the 'protected' modifier was omitted from the language to nudge developers away from OO-style code, I think that may have been the wrong way to go about it, because it makes it impossible to re-implement OO-heavy C# projects in F# in such a way that the change is transparent to any consumers. Consequently, I've had to pass on using F# to replace some C# projects -- the downside of having to re-architect large parts of an existing codebase because F# classes can't declare 'protected' members is very often going to outweigh any upsides that could be had from re-implementing a single project in F#.


#### Comment by Blair Davidson on 8/4/2014 7:40:00 AM ####
Please do this. It make using OOP facilities such in F#.


#### Comment by Gauthier Segay on 8/5/2015 7:01:00 AM ####
I concur that we need fuller support of .net type system.


#### Comment by Troy Robinson on 8/11/2015 1:30:00 AM ####
Scala has it. C# has it. Let's do it! I can't replicate certain classes in my arsenal without it!


#### Comment by Surya Halim on 9/10/2015 1:59:00 PM ####
I concur with this suggestion. IIRC, one of the reasons given was the access of protected data member defined in base class inside a closure caused very tricky situation because the closure technically should not be able to access the data member. C# solved this through clever compiler trick. Why can't this clever compiler trick be applied to F#? Will it defeat the type soundness of F# as a programming language?
I love F# for being a non-dogmatic functional-first programming language and this missing feature does indeed dampen the expectation a little.

