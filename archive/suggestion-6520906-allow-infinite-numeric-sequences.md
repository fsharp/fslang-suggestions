# Allow infinite numeric sequences [6520906] #

**Submitted by luketopia on 10/3/2014 12:00:00 AM**  
**12 votes on UserVoice prior to migration**  

F# has various syntaxes for defining numeric sequences. Some examples:
> { 0 .. 5 };;
val it : seq<int> = seq [0; 1; 2; 3; 4; 5]
> seq { 0 .. 5 };; // Same thing (seq keyword is optional)
val it : seq<int> = seq [0; 1; 2; 3; 4; 5]
> { 0 .. 2 .. 10 };;
val it : seq<int> = seq [0; 2; 4; 6; 8; 10]
> [for x in 0 .. 5 -> x * x];; // brackets can be omitted in for .. in loop
val it : int list = [0; 1; 4; 9; 16; 25]
I think it would be useful to omit the final argument to allow infinite sequences. I'm envisioning something like this:
{ 1 .. } // The positive integers
{ 2 .. 4 .. } // The positive even integers
These are IMO more readable than their Seq.initInfinite equivalents:
Seq.initInfinite ((+)1)
Seq.initInfinite (fun n -> 2 * (n + 1))
We could also use three dots for the final ellipsis to make the intent more explicit, but I'm not sure this is really useful.
Haskell allows this functionality as follows:
[ 1 .. ] -- The positive integers
[ 2, 4 ... ] -- The positive even integers
Another nice thing Haskell allows you to do is count down with sequences, but attempting to do that with F# will result in an empty sequence.
seq { -1 .. -2 .. -10 } // F# - empty sequence
[-1, -2 .. -10 ] -- Haskell - all negative integers
That probably can't be changed due to backwards compatibility, and I'm not even sure if it would be desirable anyway.



## Response ##
** by fslang-admin on 2/4/2016 12:00:00 AM **

Thanks for the suggestion. Declined per comment below.
Best regards
Don Syme
F# Language and Core Library Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6520906)**


## Comments ##


#### Comment by Christoph Rüegg on 10/4/2014 3:04:00 AM ####
Regarding counting down: "seq { -1 .. -2 .. -10 }" returns -1,-3,-5,-7,-9 for me, so it does seem to be supported (tried in LINQPad 4, not sure which F# version it uses).


#### Comment by luketopia on 10/4/2014 4:31:00 AM ####
Hmm... I must have tested it without including the step. In that case, it works just like Haskell, so you can ignore that last part. Good catch!


#### Comment by Don Syme on 2/4/2016 6:10:00 PM ####
I'm quite OK to leave infinite sequence literals out of F#. They are just a bit of a minefield waiting to go off when the sequence accidentally gets iterated. It think it's better to be much more explicit when creating infinite sequences. e.g. Seq.initInfinite etc.

