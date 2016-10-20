# Add combinators in the Async module [6367266] #

**Submitted by Loic Denuziere on 8/30/2014 12:00:00 AM**  
**16 votes on UserVoice prior to migration**  

I think the Async module could use some extra functions, such as:
* Async.Map : ('a -> 'b) -> Async<'a> -> Async<'b>
(self-explanatory)
* Async.Bind : ('a -> Async<'b>) -> Async<'a> -> Async<'b>
(I guess this would just be a curried, static version of async.Bind)
* Potentially other classic functor/monadic operations (filter, etc)
* Async.ParallelChoice : seq<Async<'a>> -> Async<'a>
(similar to Async.Parallel, except it stops as soon as one returns and cancels the others)
Most functor/monadic operations are trivial to implement for yourself, but would still be nice to have as standard. ParallelChoice, on the other hand, is not obvious to get right and is useful even if you exclusively use a computation expression style (I've seen it requested several times on Stack Overflow).



## Response ##
** by fslang-admin on 2/5/2016 12:00:00 AM **

Declining per my comment (note, Async.Choice has been added in a separate request)
Don Syme
F# Language and Core Library Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6367266)**


## Comments ##


#### Comment by Vasily Kirichenko on 10/5/2014 2:58:00 AM ####
FSharpx contains all these and much more https://github.com/fsprojects/fsharpx/blob/master/src/FSharpx.Core/ComputationExpressions/Monad.fs#L27
ExtCore contains lots of stuff like AsyncChoice, AsyncMaybe, StatefulChoice and so on, see the list of available computation expressions here https://github.com/jack-pappas/ExtCore/blob/e693e34ecc9ad4649fe08f1bb75c2531d992d147/ExtCore/Control.fs#L1725
Also ExtCore contains a bunch of modules that allow operations on collections of monadic values, like this https://github.com/jack-pappas/ExtCore/blob/e693e34ecc9ad4649fe08f1bb75c2531d992d147/ExtCore/ControlCollections.AsyncChoice.fs#L31
Personally, I reference ExtCore (and often FSharpx) in every F# project, so I see no value to add a (small) subset of the mentioned functionality right into FSharp.Core.


#### Comment by Mark Seemann on 4/5/2015 12:02:00 PM ####
Here are some examples where Async.map would have been useful:
- http://stackoverflow.com/a/6793961/126014
- http://stackoverflow.com/a/29459410/126014
While, as Vasily Kirichenko points out, it's available in FSharpx and other libraries, I never understood why it should be an argument against including such functionality in FSharp.Core. It's quite fundamental functionality that's isolated, in that it doesn't drag in unwanted dependencies. The fact that it's available in several add-on libraries is only an indication that this functionality is needed and missed.


#### Comment by Don Syme on 2/5/2016 6:14:00 AM ####
Async.Choice has been added in FSharp.Core 4.4.1.0+ (not yet released_
I think the others can be written with async { ... } easily enough and I agree with Vasily that they can go in other libraries, or in utility code.


#### Comment by Isaac Abraham on 3/12/2016 4:43:00 AM ####
Just my two cents... I can understand some of the larger pieces not being in FSharp.Core but some of the fundamental ones e.g. map, bind, iter should IMHO be there - I create them on virtually every project I work on.


#### Comment by Kevin Ransom on 3/12/2016 11:40:00 AM ####
If these are common and idiomatic, then having them in Fsharp.core ensures a consistent cross platform, cross profile implementation available and documented, and included in books.
The principle for including an API in the core library should be:
1. It is generally applicable, I.e most programs would make use of it.
2. It is platform agnostic, I.e it doesn't tie the core to a specific platform.
3. It supports idiomatic F# programming styles
Adding these or similar APIs to core will make them more generally available, and available with the same implementation all platforms.


#### Comment by Mark Seemann on 3/12/2016 11:56:00 AM ####
I complete agree with Kevin Ransom's and Isaac Abraham's comments.
The issue isn't that these features are easy to write. The problem with most software isn't how easy or difficult it is to write, but how easy or difficult it is to read.
Programmers spend more time reading than writing code; often by orders of magnitude.
While everyone can implement these features easily enough by themselves, there will be all sorts of slight variations. People will give the functions different names, or implement them slightly differently. This will slow down code reading, because whenever you encounter such a function, you can never be sure that it has behaviour identical to what you expect.
Or, even worse, you'll assume that it behaves in a particular way, but this particular version behaves differently, and you'll now waste a couple of hours troubleshooting some subtle bug, and you can't see the source of it because your assumptions are invalid.
Putting general-purpose logic into the core library will prevent such problems.

