# Async.WaitTask for non generic Task [6092853] #

**Submitted by thinkb4coding on 6/24/2014 12:00:00 AM**  
**9 votes on UserVoice prior to migration**  

Async.WaitTask has an overload for Task<'T> but has no support for Task.
Adding a Task -> Async<unit> overload would make things easier when dealing with C# and BCL async methods.



## Response ##
** by fslang-admin on 11/8/2014 12:00:00 AM **

Approved for the F# 4.0+ stream – see discussion.
An implementation has now been submitted, reviewed and committed to the “fsharp4” branch, see https://visualfsharp.codeplex.com/SourceControl/network/forks/thinkb4coding/visualfsharp/contribution/7019
Further discussions should be directed there.


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6092853)**


## Comments ##


#### Comment by Dave Thomas on 6/24/2014 9:27:00 AM ####
This ones easy, I think its only a one or two line change, wont take you long :-)


#### Comment by Don Syme on 6/24/2014 10:10:00 AM ####
I consider this "approved in principle" for the F# language design, to be added as soon as implementation+testing is provided, for F# 4.0 or beyond.
I'd encourage you to contribute the implementation and testing for this one.
There is one small problem: adding an extra overload can be considered a breaking change, e.g.
let f x = Async.AwaitTask(x)
will no longer compile. For this reason, it looks sensible to call the new method "AwaitTaskUntyped", "AwaitTaskNonGeneric" or the like. A good satisfying name is hard to find.
Comments on names welcome.


#### Comment by Veikko Eeva on 7/29/2014 11:55:00 AM ####
I'm not sure if this is the right place for this, but it looks like there's on occassion a need to also convert Task<Unit> to plain Task.
Maybe something like this
let inline TaskUnitToTask(task: Task<Unit>) =
task :> Task
It may not be "easy" to discover one could do a plain upcast to transform a F# Task<Unit> to C# style Task. Which is the situation I've come across Task<Unit> types (e.g. C# function returning taking or giving plain tasks).

