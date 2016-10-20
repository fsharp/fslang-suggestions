# Allow to define types at expression scopes [5663202] #

**Submitted by Gustavo Guerra on 3/21/2014 12:00:00 AM**  
**36 votes on UserVoice prior to migration**  

The suggestion is to allow "type X = ..." in an expression, e.g.
let f () =
type X = A | B
let x = (A,A)
let y = (B,B)
if (x=y) then true else false



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5663202)**


## Comments ##


#### Comment by Phillip Trelford on 3/21/2014 8:09:00 AM ####
At a minimum type aliasing at local scopes as per C++ typedef would be really handy. Nested type declaration would also be nice.


#### Comment by Don Syme on 3/21/2014 1:12:00 PM ####
The technical questions that arise are
(a) can these include full type definitions - including members? If so, can these capture values from scope?
(b) can these types appear in the inferred type of the function?


#### Comment by Gustavo Guerra on 10/26/2014 5:24:00 PM ####
(b) Should not be possible, as these types should be private to the function, so an error should be issued on that case
(a) Yes, they should be full type definitions. Capturing values from scope would be an added bonus, but would be also ok if that wasn't supported, I guess.


#### Comment by Gustavo Guerra on 10/26/2014 5:27:00 PM ####
Actually, even if members weren't allowed this would be already very useful. On local scope we usually use a lot of tuples, and refactoring to records or DUs is usefull, but it's a bit annoying that you have to do that at global scope


#### Comment by Vasily Kirichenko on 10/27/2014 2:46:00 AM ####
This is now it's implemented in D https://gist.github.com/vasily-kirichenko/95a2cabfba599884b61d
So, no-static types can capture local variables and cannot escape the function scope.


#### Comment by Don Syme on 2/4/2016 1:04:00 PM ####
What if only type aliases were allowed?


#### Comment by Gustavo Guerra on 7/22/2016 5:38:00 AM ####
This was also added to TypeScript: https://www.typescriptlang.org/docs/release-notes/typescript-1.6.html


#### Comment by Gustavo Guerra on 7/22/2016 5:38:00 AM ####
Type aliases only would help a bit but not really solve the problem completely. Having local records and DUs would be much better


#### Comment by Anonymous on 7/24/2016 1:58:00 PM ####
I was surprised to find this isn't inherently supported, when I first coded it it seemed quite natural because I can declare an inner function within a parent function and the inner function is known only within that parent, I added a simple enum type - also within some parent function and the compiler complained.

