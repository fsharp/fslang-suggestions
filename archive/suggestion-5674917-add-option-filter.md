# Add Option.filter [5674917] #

**Submitted by Mark Seemann on 3/24/2014 12:00:00 AM**  
**4 votes on UserVoice prior to migration**  

It may be that I'm missing something obvious, but doesn't the Option module lack a filter function?
let x1 = Some 1
let x2 = Some 3
let y1 = x1 |> Option.filter (fun i -> i = 3) // Returns None
let y2 = x2 |> Option.filter (fun i -> i = 3) // Returns Some 3



## Response ##
** by fslang-admin on 11/8/2014 12:00:00 AM **

This is approved for F# 4.0+
An implementation and testing has been submitted to the “fsharp4” branch of visualfsharp.codeplex.com here: http://visualfsharp.codeplex.com/SourceControl/network/forks/ploeh/optionfilter/contribution/7011
The implementation has now been committed to the “fsharp4” branch


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5674917)**


## Comments ##


#### Comment by Mauricio Scheffer on 3/24/2014 6:46:00 PM ####
You could just use FSharpx ( https://github.com/fsprojects/fsharpx/blob/master/src/FSharpx.Core/ComputationExpressions/Monad.fs#L238 ) or ExtCore ( https://github.com/jack-pappas/ExtCore/blob/master/ExtCore/Pervasive.fs#L881 ) or FSharpPlus (the generic 'filter' function).
Just like filter, there are a lot of functions that could be included in FSharp.Core. IMHO it's best to leave FSharp.Core to be minimal and implement these additional functions in separate libraries that can evolve at their own speed.

