# Code clarity: Make syntax for sequence expressions as simple as syntax for lists [12900021] #

**Submitted by Alexei Odeychuk on 3/11/2016 12:00:00 AM**  
**4 votes on UserVoice prior to migration**  

I suggest simplifying syntax for generating sequences. It would be great to make it as simple as syntax for lists in F#.
For example,
let lst = [ 1; 2; 3; 4 ] // allowed
let sq = seq { 1; 2; 3; 4 } // not allowed, why?
// error FS0739: Invalid object, sequence or record expression.
Now, the F# syntax rules allow declaring a simple sequence expression as follows:
let se = seq { yield 1; yield 2; yield 3 }
I think syntax rules may well be simplified in that case. It would be more comfortable for language users to declare sequences with no need to write the yield keyword each time when they specify a new value for the sequence expression.
P.S. At the same time, there is no need to make any improvements in syntax for generating sequences using ranges specified in the form like 1 .. 10.
let lst = [ 1 .. 10 ] // allowed
let sq = seq { 1 .. 10 } // allowed, and that's good!



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/12900021)**


## Comments ##


#### Comment by Vasily Kirichenko on 3/13/2016 10:24:00 AM ####
You can write
let sq = seq [ 1; 2; 3 ]


#### Comment by Alexei Odeychuk on 3/14/2016 3:09:00 AM ####
Thank you, Vasily. Of course, I can, but let sq = seq { 1; 2; 3 } would be better and consistent with the existing F# syntax rules for sequence expressions, I mean the use of {}.


#### Comment by Jared Hester on 6/28/2016 12:23:00 AM ####
However this would not be consistent with the rules for computation expressions.
"Sequence expressions are an example of a computation expression, as are asynchronous workflows and query expressions." [1]
If you're using a seq expr it should be able to take advantage of complex internal logic, recursive looping, lifting nested sequences with yield!, etc.
Vasily is right, if all you want is a simple sequence use
seq [10;55;0] or seq [| 40; 5; 0; 40 |]|
Perhaps that error should be improved to say "invalid sequence expression ..." with some more details and a suggestion
[1] https://msdn.microsoft.com/en-us/visualfsharpdocs/conceptual/computation-expressions-%5Bfsharp%5D

