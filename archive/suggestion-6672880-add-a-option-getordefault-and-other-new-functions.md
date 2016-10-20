# Add a Option.getOrDefault and other new functions to the Option module [6672880] #

**Submitted by Gustavo Guerra on 11/6/2014 12:00:00 AM**  
**15 votes on UserVoice prior to migration**  

Like List.nth, defaultArgs has the parameters in the "wrong order" to be able to be used in partial application. List.item is solving that problem, we should also do the same for defaultArg



## Response ##
** by fslang-admin on 2/29/2016 12:00:00 AM **

Approved-in-principle to make some sensible additions to the Option module
Details about naming and exact additions will need to be finalized.
We will create an RFC for this at https://github.com/fsharp/FSharpLangDesign/tree/master/RFCs
Thanks
Don Syme
F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6672880)**


## Comments ##


#### Comment by Vasily Kirichenko on 11/6/2014 7:58:00 AM ####
I think a better name is getOrElse (it's also used in Scala). I would also like to add several other functions, like:
ofNull
ofNullable
toNullable
attempt
orElse
getOrTry
orTry
flatten
(we use all of them in Visual F# Power Tools https://github.com/fsprojects/VisualFSharpPowerTools/blob/3299b8cc99bea9430149df0338304b60c8a6405b/src/FSharpVSPowerTools.Core/Utils.fs#L49-L91)
There are many others in ExtCore https://github.com/jack-pappas/ExtCore/blob/master/ExtCore/Pervasive.fs#L727-L923 and in FSharpx https://github.com/fsprojects/fsharpx/blob/master/src/FSharpx.Core/ComputationExpressions/Monad.fs#L86-L285
I think we should collect all of them in a table (like it's with collections on codeplex) and discuss what should be added into FSharp.Core (it'd be fine to do the same with Choice).


#### Comment by Richard Minerich on 11/6/2014 8:03:00 AM ####
I'm not sure if they've been defined in the 4.0 pull requests but I always define something like:
Option.resolve : 'T -> 'T option -> 'T
Option.resolveBy : (unit -> 'T) -> 'T option -> 'T
Option.tryResolve : 'T option -> 'T option -> 'T option
Option.tryResolveBy (unit -> 'T option) -> 'T option -> 'T option


#### Comment by Mark Seemann on 2/23/2016 3:56:00 AM ####
Other nice-to-haves:
Option.map2: ('a -> 'b -> 'c) -> 'a option -> 'b option -> 'c option
Option.map3: ('a -> 'b -> 'c -> 'd) -> 'a option -> 'b option -> 'c option -> 'd option
The List module defines map2 and map3, so it'd be natural to add these to the Option module as well.


#### Comment by Mark Seemann on 2/23/2016 4:16:00 AM ####
It'd also be nice with a built-in computation builder.


#### Comment by Mark Seemann on 2/23/2016 9:01:00 AM ####
Opened a GitHub issue for this: https://github.com/Microsoft/visualfsharp/issues/980


#### Comment by Enrico Sada on 3/1/2016 9:10:00 AM ####
created RFC https://github.com/fsharp/FSharpLangDesign/issues/60

