# Implement try/fault expressions [5670027] #

**Submitted by Jack Pappas on 3/23/2014 12:00:00 AM**  
**5 votes on UserVoice prior to migration**  

I would like F# to have try/fault expressions. It would work along the same lines as the current try/with syntax, although the 'fault' block would be constrained to a return type of 'unit'. I don't expect the usage of this to be terribly common, but it would be very handy to have for logging purposes.
To answer the inevitable question, "Why not just use try/with and reraise()?" -- with try/with you're actually catching the exception; unless you remember to call reraise() to terminate all paths in the control flow within the 'with' block, you'll end up swallowing the exception and not getting the expected behavior. Similarly, if an inexperienced (or perhaps just inattentive) developer re-raises the exception with 'raise' instead of 'reraise', the stack trace information will be lost.
With try/fault, it'd be easy to log relevant information (e.g., variable values) from functions when unwinding the stack due to an exception being thrown, without the downside of being able to affect the control flow.



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5670027)**


## Comments ##


#### Comment by Jon Harrop on 3/26/2014 6:19:00 AM ####
Why not use try..finally?


#### Comment by Jack Pappas on 3/28/2014 6:33:00 PM ####
Jon -- With try/finally, the code in the finally block is always executed, whether an exception is raised within the protected (try) block or not. With try/fault, the code in the fault block is executed *only* when an exception has been raised in the try block.
It would be possible to emulate try/fault behavior with try/finally by writing something like this:
let mutable error = true
try
// code which may or may not raise an exception
error <- false
finally
if error then ... // execute the "fault" handler
but it's hacky and I'd prefer just to use a true 'fault' block (which is already a feature supported by the CLR). In addition, the code to implement try/finally in the compiler is basically identical to what's needed for try/fault, so it should be fairly straightforward to implement this. If this language feature were accepted, I'd be happy to contribute an implementation (or attempt to).


#### Comment by Don Syme on 2/5/2016 5:39:00 AM ####
My inclination is that we won't do this in F#. I can see the use cases though - are there really no other ways to achieve this in .NET, e.g. by calling a library function with two lambdas?


#### Comment by Don Syme on 2/10/2016 11:02:00 AM ####
One approach to this would be to add an OnException combinatory accepting a pair of functions. Likewise an Async.OnException.

