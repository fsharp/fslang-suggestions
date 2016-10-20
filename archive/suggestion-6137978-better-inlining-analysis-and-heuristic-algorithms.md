# Better inlining analysis and heuristic algorithms [6137978] #

**Submitted by Nick Palladinos on 7/5/2014 12:00:00 AM**  
**22 votes on UserVoice prior to migration**  

It would be great if the compiler can inline away CPS compositions like the following.
let inline f k = (fun x -> k (x + 1))
let inline g k = (fun x -> k (x + 2))

(f << g) id 1 // 4
In general better inlining analysis and heuristic algorithms



## Response ##
** by fslang-admin on 2/5/2016 12:00:00 AM **

This is automatically approved – definitely something we want to do – but not individually tracked individually here. Let’s do it… Please submit your PRs for improved inlining :)
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6137978)**


## Comments ##


#### Comment by Jack Pappas on 7/6/2014 9:28:00 AM ####
There was a related question on StackOverflow yesterday which provides another case where the F# compiler's inlining analysis could be improved: https://stackoverflow.com/questions/24589480/why-cant-the-f-compiler-fully-inline-function-arguments-of-a-higher-order-func


#### Comment by Jack Pappas on 7/6/2014 9:56:00 AM ####
One more related StackOverflow question: https://stackoverflow.com/questions/23875598/why-is-function-composition-from-left-to-right-11x-to-19x-faster-than-right-to-l


#### Comment by Arbil on 7/7/2014 7:28:00 AM ####
The problem I've described in one of the links Jack has linked to is actually more basic than the OP's. It's that the first order function passed as an argument to a second order function is not inlined even if both the second and first order functions are marked as inline. This makes it so that using second order functions always comes with a performance penalty, which is not the case for first order functions.


#### Comment by Don Syme on 2/5/2016 6:22:00 AM ####
Note this suggestion is automatically "approved" under the general heading of "we accept optimization improvements". It's not a design change to the language per se.
> It's that the first order function passed as an argument to a second order function is not inlined even if both the second and first order functions are marked as inline
I would like to see this fixed!


#### Comment by Don Syme on 2/5/2016 9:56:00 AM ####
I'm going to close this because it's automatically approved.
We would _love_ some PRs to improve inlining.
I've tracked the potential optimization in the compiler guide here: https://github.com/fsharp/fsharp.github.io/commit/f33141115b0646450e872b86949ac25ab9d86f44

