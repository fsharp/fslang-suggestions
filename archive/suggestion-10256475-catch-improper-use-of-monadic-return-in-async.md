# Catch improper use of monadic return in async [10256475] #

**Submitted by William Blum on 10/17/2015 12:00:00 AM**  
**11 votes on UserVoice prior to migration**  

The following code should issue a type checking error since return () should yield an Async<unit> and return 42 should yield an Async<int>.
let f c =
async {
return ()
printfn "You passed %A and I am returning 42" c
return 42
}
Additionally the following code should issue a warning since the return statement does not actually affect the flow of execution as the name suggests (The printf statement is actually executed).
let g c =
async {
return ()
printfn "You passed %A and I am returning 42" c
return ()
}



## Response ##
** by fslang-admin on 1/23/2016 12:00:00 AM **

See comment
Approved in principle, though definitely subject to a more detailed satisfactory design (not to adhoc,not specific to “async”)
Don Syme, F# Language and Core Library Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/10256475)**


## Comments ##


#### Comment by Vasily Kirichenko on 10/18/2015 3:09:00 PM ####
Return in computation expressions is the monodic "return" (or "pure") and has nothing in common with return in imperative languages like C#. What's more, return usually == yield.


#### Comment by Don Syme on 1/23/2016 11:50:00 AM ####
I do agree that ideally this should be caught, and some kind of warning given.
I don't specifically have a design in mind, but I am going to mark this as "planned", though subject to a detailed design, implementation and testing. I don't expect it to be a top-priority, but from the design perspective I'm ok with us looking for a solution to this specific problem.

