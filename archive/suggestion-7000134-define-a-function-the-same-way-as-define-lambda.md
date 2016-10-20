# Define a function the same way as define lambda [7000134] #

**Submitted by vanh on 1/23/2015 12:00:00 AM**  
**3 votes on UserVoice prior to migration**  

Currently the way we define function is: let add1 x = x +1 which is not consistent with the way we define lambda fun x -> x +1. More importantly this will help new learner like me easily distinguish between a function and a value. When reading code, I always find it easier to find a lambda expression because of the fun keyword and the -> than the function. Since code is read more than write it would help save time too.



## Response ##
** by fslang-admin on 2/14/2015 12:00:00 AM **

While we appreciate the feedback, this kind of fundamental syntax change is beyond the scope of the kind of change we would consider for the F# language at version F# 4.0.
Thanks
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/7000134)**


## Comments ##


#### Comment by Richard Gibson on 1/23/2015 6:37:00 AM ####
Sorry, I guess I'm not sure what you're asking for.
let add1 x = x + 1
is just short for
let add1 = fun x -> x + 1
Both are legal F#. Is there something else you're after?


#### Comment by Vanh Phom on 1/27/2015 6:41:00 PM ####
What I mean is:
fun add1 x -> x + 1 define a function name add1 with parameter x and body x + 1
fun x -> x +1 define a no name function (lambda) with parameter x and body x + 1


#### Comment by Vasily Kirichenko on 2/8/2015 1:32:00 AM ####
Currently "fun add1 x -> x + 1" is a (curried) lambda function, so you cannot use this syntax for anything else.

