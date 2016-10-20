# Add curry and uncurry functions [6826972] #

**Submitted by Patrick McDonald on 12/10/2014 12:00:00 AM**  
**8 votes on UserVoice prior to migration**  

let curry f x y = f (x, y)
let uncurry f (x, y) = f x y
As implemented in Fsharpx. I have a sample implementation here:
[https://visualfsharp.codeplex.com/SourceControl/network/forks/PatrickMcDonald/visualfsharp?branch=curry]



## Response ##
** by fslang-admin on 7/17/2015 12:00:00 AM **

Many thanks for this suggestion. It is being marked as declined – for discussion see the comments above.
Further comments, use cases, information and discussion welcome
Don Syme, F# Language and Core Library Evolution.


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6826972)**


## Comments ##


#### Comment by Pierre Irrmann on 12/12/2014 4:48:00 AM ####
I was about to suggest the same one this morning! I give it my last remaining 2 votes...


#### Comment by Patrick McDonald on 12/12/2014 6:11:00 AM ####
It seems F# already has the uncurry function, AKA the "backward double pipe" operator (<||)
https://visualfsharp.codeplex.com/SourceControl/network/forks/PatrickMcDonald/visualfsharp/contribution/7759
I don't think the curry function can be implemented as an operator as it takes 3 arguments.
Also, it seems curry/uncurry has been discarded as an idea previously, from reading this discussion [although this discussion doesn't mention the existence of (<||)]:
https://github.com/fsprojects/fsharpx/issues/165


#### Comment by Isaac Abraham on 12/15/2014 6:58:00 AM ####
There's also ||> for uncurrying as well.


#### Comment by Don Syme on 7/17/2015 9:35:00 AM ####
F# has no flip/curry/uncurry operators in the prelude - we did consider them of course in F# 1.x but made a definite decision not to include them. OCaml made the same decision at that time. Code that uses these is often of reduced readability. Not always, but in my experience too often.

