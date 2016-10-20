# Record type inference suggestion [7138324] #

**Submitted by Steven Taylor on 2/24/2015 12:00:00 AM**  
**1 votes on UserVoice prior to migration**  

Note that if the record {a: int; b: int} is declared last, then type + argument name type inference will not work. Switching the order around resolves the issue. However, this behaviour can be a little mentally jarring.
The lightweight syntax is very useful. It'd be great to strengthen it up.
module Eg1 =
type AB = {a: int; b: int}
type A = {a: int}
type B = {b: int}
let a = {a=1}
let b = {b=2}
let ab = {a=1;b=2}
module Eg2 =
type A = {a: int}
type B = {b: int}
type AB = {a: int; b: int} // <- NB. only the order has changed
let a = {a=1} // fail
let b = {b=2} // fail
// note that example 3 resolves the ambiguity with the dot syntax on the first named field, but that's not the point.
module Eg3 =
type A = {a: int}
type B = {b: int}
type AB = {a: int; b: int}
let a = {A.a=1}
let b = {B.b=2}
let ab = {a=1;b=2}



## Response ##
** by fslang-admin on 2/5/2016 12:00:00 AM **

Marking this as approved-in-principle, per my comment below
We will open an RFC for this in due course, though the change should not be large
https://github.com/fsharp/FSharpLangDesign/tree/master/RFCs
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/7138324)**


## Comments ##


#### Comment by Gauthier Segay on 2/28/2015 7:19:00 AM ####
There was a relevant thread there:
https://groups.google.com/forum/#!topic/fsharp-opensource/vb3pTUAcRVs


#### Comment by Don Syme on 2/5/2016 5:38:00 AM ####
Yes, it looks reasonable to be more flexible here. I will mark this as approved-in-principle

