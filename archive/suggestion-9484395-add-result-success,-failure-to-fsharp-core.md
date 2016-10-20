# Add Result<'Success,'Failure> to FSharp.Core [9484395] #

**Submitted by Oskar Gewalli on 8/25/2015 12:00:00 AM**  
**17 votes on UserVoice prior to migration**  

In order to be able to write code that you can easily consume that does not throw an exception have a fsharp core type with the following signature:
type Result<'TSuccess,'TError> =
| Success of 'TSuccess
| Error of 'TError
from
https://github.com/fsharp/fsharp/issues/479



## Response ##
** by fslang-admin on 8/2/2016 12:00:00 AM **

Completed. The RFC is here: https://github.com/fsharp/FSharpLangDesign/blob/master/RFCs/FS-1004-result-type.md
Don Syme
F# Language and Core Library Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/9484395)**


## Comments ##


#### Comment by Mauricio Scheffer on 8/28/2015 5:34:00 AM ####
There's already an isomorphic type in FSharp.Core : https://msdn.microsoft.com/en-us/library/ee353439.aspx .
I'd say error handling through discriminated unions belongs to the user lib area, e.g. FSharpx, Chessie, etc.


#### Comment by Ben Lappin on 12/28/2015 7:58:00 AM ####
I really like this model and believe it is useful enough to warrant inclusion in the language. Note the inclusion in other languages (e.g. Rust).
This model - specifically returning a success result (of varying type) or an error result (of a single type) - lends itself extremely well to the computation expression:
let resultOrError = result {
let! result1 = thingThatMayFail1()
let! result2 = thingThatMayFail2 result1
return result2 }
match resultOrError with
| Success x -> ... // proceed along success path
| Failure e -> ... //handle error
The expected behavior of this computation expression is fairly clear (at least to me), and it would be nice not to have to include a file or library to use it in all my projects (and I do use it all the time).
Additional reading: Scott W's description of "Railway Oriented Programming" http://fsharpforfunandprofit.com/posts/recipe-part2/


#### Comment by Don Syme on 2/5/2016 9:20:00 AM ####
In balance I think adding this type to FSharp.Core would be a good thing. Using Choice has obvious problems in clarity
One thing I wonder is if it should wait until a struct-union feature is available so the type could be a struct.


#### Comment by Oskar Gewalli on 2/7/2016 3:09:00 AM ####
What kind of testing would you like to be done?
Perhaps some example usage?
The obvious construct to also expose would be something like
Result.Try : (unit->'T1) -> Result<'T1, Exception>
as can be seen in Chessie:
https://github.com/fsprojects/Chessie/blob/master/src/Chessie/ErrorHandling.fs#L29
and in rust:
https://doc.rust-lang.org/std/result/#the-try-macro
however, "Try" collides with a .net keyword, so it not be ok to use.


#### Comment by thinkb4coding on 2/12/2016 3:24:00 PM ####
Yep, having struct union for this would be even more awsome


#### Comment by Enrico Sada on 2/14/2016 5:59:00 AM ####
Create F# RFC 1004 ( https://github.com/fsharp/FSharpLangDesign/blob/master/RFCs/FS-1004-result-type.md )
Please continue discussion in https://github.com/fsharp/FSharpLangDesign/issues/49

