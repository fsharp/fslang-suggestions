# allow compiler directive to switch off inlining [15332553] #

**Submitted by Steven Taylor on 7/22/2016 12:00:00 AM**  
**8 votes on UserVoice prior to migration**  

to get around debugging issues with the inline macro device, this pattern creaps into the code base (taken from FsPickler):
#if DEBUG
let writeBoundedSequence
#else
let inline writeBoundedSequence
#endif
It would be nice to be able to turn off the effect of the inline keyword for files and entire projects while compiling for debugging purposes. Also, optionally setting ignore inline for code executed in an interactive session would be useful too.



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/15332553)**


## Comments ##


#### Comment by Abel on 9/25/2016 7:38:00 AM ####
I believe I have seen this request before. The problem is that "inline" changes the behavior and is often inevitable to create semi-polymorphic (duck-typed) functions and types. Consider:
let f a b = a + b // a and b are ints
let inline f a b = a + b // a and b requires member (+)
Or:
let f a b = int a * int b // a and b are ints
let inline f a b = int a * int b // a and b require op_Explicit
If you call this code:
let result = f 1.23 4uy // the first will work with both, inferred float -> byte -> int
let result = f 1.23 4L // works with "inline", does not compile without (wrong type)
If your only requirement is to remove optimization of "inline" and the different inference rules have no effect, it would make (some) sense to disallow it, esp. since during debugging it is beneficial to be able to step through the method.
You can simplify your above code somewhat:
let
    #if DEBUG
    inline
    #endif
    writeBoundedSequence ....
Though I would suggest you create a new compiler constant, say INLINE:
let
    #if INLINE
    inline
    #endif
    writeBoundedSequence ....
That is because you would want to be able to see debug behavior of the inlined version and this way you can better control when and where INLINE is used.

