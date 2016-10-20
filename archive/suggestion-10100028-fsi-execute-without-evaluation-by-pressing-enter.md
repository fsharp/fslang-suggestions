# FSI execute without evaluation by pressing Enter [10100028] #

**Submitted by Yaar Hever on 10/6/2015 12:00:00 AM**  
**2 votes on UserVoice prior to migration**  

The way F# interactive is set now, code is executed when it is evaluated, i.e., when a line ends with a double semicolon and Enter.
Evaluation is indeed important, but FSI can also be used to interact with libraries or to get something from the standard output.
This feature refers mostly to "side effects" and might be seen contrary to the values of functional programming, but those are quite interesting and helpful in a scripting language where you want immediate results. FSI has the advantage of being able to access DLLs and execute functions quickly while still enjoying the power of type inference.
I suggest adding a sort-of "python" mode in which every piece of code is executed after pressing Enter, if it is well-formed and doesn't expect further arguments. Double semicolons would still be in use for evaluating. It can be referred to as "imperative mode".
Thus, typing:
> printfn "hello world" [Enter]
would output:
hello world
and start a new interactive line:
>
But typing
> printfn [Enter]
would start a new line and wait for an argument.
The same goes for bindings and other closures.
The problem of partial application can be solved by expecting the user to press Enter twice for execution:
typing:
> let printInt = printfn "%d" [Enter]
still expects another argument and doesn't execute, but pressing Enter again will bind printInt to a function: (int -> unit).
This means, of course, that a non well-formed piece of code followed by pressing Enter twice will have to fail and start a new line.



## Response ##
** by fslang-admin on 2/3/2016 12:00:00 AM **

Declined per comment


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/10100028)**


## Comments ##


#### Comment by Yaar Hever on 10/11/2015 1:53:00 PM ####
On second thought, I would like to restrict this suggestion. It doesn't make sense to have this faster evaluation option for bindings, since those could be easily evaluated with ';;' like now.
In fact, the only kind of expression that could be made faster and more efficient by not requiring the double semicolon in an interesting way are expressions that evaluate to a unit.
So I withdraw the two-'Enter' suggestion and suggest only that if this option is set, each time the user presses 'Enter', the accumulated buffer would be checked to see if it evaluates properly to a unit. If it does, then the buffer is executed and all of the side-effects take place.
To run an imperative library function that returns a value (say, a boolean marking success/failure), the use could add "|> ignore" which would make it evaluate to a unit.


#### Comment by Don Syme on 2/3/2016 2:45:00 PM ####
Given the complexity of implementing this (invoking the type checker) we are unlikely to make specific changes here until a major revamp of F# interactive is done.


#### Comment by Yaar Hever on 2/25/2016 6:16:00 PM ####
Thank you for your response. I hope this could be implemented in the future.


#### Comment by Otto Gebb on 10/11/2016 6:15:00 AM ####
In C# Interactive it works fine. Sad to see this was rejected. Having to type a double semicolon each time I want to see what a value of a variable is is annoying.

