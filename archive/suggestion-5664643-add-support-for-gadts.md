# Add support for GADTs [5664643] #

**Submitted by Richard Minerich on 3/21/2014 12:00:00 AM**  
**219 votes on UserVoice prior to migration**  

Generalized Algebraic Data Types essentially extend standard union types to allow different generic instantiations when defined recursively.
You can see a simple explanation of how they work in haskell here: https://en.wikibooks.org/wiki/Haskell/GADT
They open the door to such fantastic type safe data structures as heterogeneous lists and so can vastly improve type safety within the language.



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5664643)**


## Comments ##


#### Comment by Radek Micek on 4/21/2014 3:31:00 PM ####
I don't think that benefits of GADTs outweight how they complicate type system and type inference (you may lose principal-type property).
BTW: you can do heterogeneous lists without GADTs.
BTW 2: you may be interested in Guarded Algebraic Data Types - http://gallium.inria.fr/~fpottier/publis/simonet-pottier-hmg-toplas.pdf


#### Comment by Suminda Sirinath Salpitikorala Dharmasena on 5/6/2014 8:49:00 AM ####
Since OCaml has this I don't see why not F#


#### Comment by Don Syme on 7/4/2014 6:48:00 AM ####
There are some relevant commments here too: /archive/suggestion-6062821-add-dependent-types


#### Comment by Don Syme on 2/3/2016 12:45:00 PM ####
A major consideration is that GADTs are difficult to compile to .NET IL efficiently. Specifically, it is not possible to recover an existentially-hidden type variable except via virtual dispatch. For example
type C
type D<T> : C
If we have a C, a GADT implementation may "know" that for certain cases T has certain values, or decomposes in certain ways. But you can't implement this in .NET IL generics - you have to use reflection to recover the value of T and instantiate the branch code with a specific value. Russo and Kennedy had a proposal for what to do about this for C#.
This is a significant blocking factor for adding this to F# - GADT code would need reflection and would be less efficient.

