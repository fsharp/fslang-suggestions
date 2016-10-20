# Add Dependent Types [6062821] #

**Submitted by Jared Hester on 6/16/2014 12:00:00 AM**  
**14 votes on UserVoice prior to migration**  

Dependent types allow types to be predicated on values. Full-spectrum dependent types would be preferable so that there is no restriction
on which values may appear in types. An example would be declaring a type 'Vector' a list that carries its size in the type.
The type decleration of a dependent type is actually declaring a family of types that maintain an invariant.
Functions can be defined on dependent types, for example a function 'vector_append' would append two Vectors, returning a Vector which is the sum of the lengths of the inputs.



## Response ##
** by fslang-admin on 9/3/2014 12:00:00 AM **

As mentioned in the comments, this is beyond the scope of F#. It could be considered in some future derivative language (and feel free to experiment!). See the comment by Loic in particular.
Closing this to give clarity and recycle the votes.
Don Syme, Current BDFL for F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6062821)**


## Comments ##


#### Comment by Loic Denuziere on 6/17/2014 8:34:00 AM ####
A few comments on this topic:
* Dependent types are a big effort and are far beyond the intended scope of F#. They also make type inference extremely difficult, and generally indecidable.
* For the particular example that you gave (encoding the length of a vector in the type), dependent types are overkill. GADTs are sufficient, and they are much smaller and easier to implement and infer. You are probably posting this in light of this article that has been making the rounds lately: http://www.thesoftwaredevelopmentlifecycle.com/an-almost-type-safe-library-for-linear-algebra/ Note that it talks about *fake* dependent types, and it actually uses GADTs, which can do this particular thing that have traditionally been associated with dependent types, but cannot do a lot of other things that dependent types can.
So in short: if what you want is Vector, ask for GADTs, not dependent types, at least they might be implemented in F# one day; dependent types almost certainly never will.
* You can have a look at F*, an F#-based dependently-typed language, maybe this can be interesting for you.


#### Comment by Jared Hester on 6/22/2014 10:27:00 PM ####
That's an interesting article, but I actually hadn't seen it before. I wanted to keep the example simple for people who are unfamiliar with dependent types. My interest in dependent types came from reading about Idris ( http://eb.host.cs.st-andrews.ac.uk/writings/plpv11.pdf , http://eb.host.cs.st-andrews.ac.uk/writings/idris-tutorial.pdf ), a desire to enforce strong type invariants that are checked at compile time, and I think it'd be pretty cool to instantiate a single algorithm across a variety of datatypes.
Perhaps there's a way to implement dependent types with restrictions or expand the type system to include datatype constructors in type declarations and datatypes to appear in Kind declarations (obviously Kinds would need to be added to F# as well) so that Datatype lifting would be possible.
Plus it seems like theres been some interesting research into building workable type inference systems for Dependent Types in the past year or two-
"Compositional and Lightweight Dependent Type Inference for ML" https://www.cs.purdue.edu/homes/suresh/papers/vmcai13.pdf
"Dependent Types: Easy as PIE - Work-In-Progress Project Description" http://research.microsoft.com/en-us/people/dimitris/pie.pdf
"Type Inference, Haskell and Dependent Types" https://personal.cis.strath.ac.uk/adam.gundry/thesis/thesis-2013-12-03.pdf
While F-star is an intriguing project, at its current state it's even more useless than Haskell =P


#### Comment by Don Syme on 6/24/2014 10:22:00 AM ####
I agree with Loic Denuziere that dependent types are well beyond the intended scope of F#, along with the other comments he makes.


#### Comment by Fraser Waters on 7/3/2014 3:15:00 PM ####
In regards to GADTs there's a paper from MS Research[1] about how GADTs are equivalent in expressiveness to parametric types and type equality constraints. Just adding type equality constraints would be enough to express GADT equivalent constructs in F#. Type equality constraints aren't too complex, I actually looked at them as my final year project [2], using "special" methods to declare constraints and cast with regards to those constraints and an F# checker that used Mono.Cecil to read the methods and check the methods and call sites matched the constraints.
[1] Generalized Algebraic Data Types and Object-Oriented Programming, Andrew Kennedy and Claudio V Russo
[2] https://github.com/Frassle/Imperial-FYP/blob/master/report.bib


#### Comment by Don Syme on 7/4/2014 6:47:00 AM ####
Hi Fraser - thanks for this, I have a copy of your final year project report and am looking forward to reading it.


#### Comment by Dude on 8/24/2016 5:27:00 AM ####
One less reason to learn F# I guess...

