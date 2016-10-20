# Make tuple defined DU cases more consistent with tuple [12820011] #

**Submitted by Gauthier Segay on 3/5/2016 12:00:00 AM**  
**9 votes on UserVoice prior to migration**  

It is possible to pattern match tuples in a flexible way:
let a = 1,2
match a with
| 1, _ -> ()
| _ -> ()
but it's not possible to do this on tuple defined DU cases, one has to write this:
match pat with
| SynPat.LongIdent(_, _, _, _, _, _) -> ()
| ...
which breaks whenever the case definition change (even at place where we don't care of the contents)
while supporting this would be friendlier / more resilient to DU case change:
match pat with
| SynPat.LongIdent _ -> ()
or even
match pat with
| SynPat.LongIdent foo -> () // can deconstruct foo like a normal tuple



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/12820011)**


## Comments ##


#### Comment by Gauthier Segay on 3/5/2016 2:38:00 PM ####
Actually found out it works with enclosing parens:
match pat with
| SynPat.LongIdent(_) -> ()
but it doesn't work with identifier (case whose utility is close to 0)
match pat with
| SynPat.LongIdent(a) -> ()


#### Comment by Alexei Odeychuk on 3/5/2016 3:02:00 PM ####
I support the idea shared by Gauthier Segay in respect of "match pat with
| SynPat.LongIdent foo -> ..."! When I developed a natural language processing application in F#, I often wrote something like: match arabicLexeme with
| Participle(_, _, _, _, _, _, _) -> ...
| FiniteVerb(_, _, _, _, _, _, _, _, _, _) -> ... Right now, the F# 4.0 compiler emits an error FS0019: This constructor is applied to 1 argument(s) but expects 6 in response to a line of code like "match pat with SynPat.LongIdent foo -> ...". There is no doubt, syntax for discriminated union cases is worth to be improved in this context.
P.S. As to "match pat with SynPat.LongIdent _ ->" I tested it and found that the compiler (F# 4.0, Visual Studio 2015, Windows 7) accepted it.
My test code for the F# Interactive was:
type SynPat =
| LongIdent of int * int * int * int * int * int
let x : SynPat = LongIdent(1, 2, 3, 4, 5, 6)
let y = match x with LongIdent _ -> true
The F# Interactive response was:
type SynPat = | LongIdent of int * int * int * int * int * int
val x : SynPat = LongIdent (1,2,3,4,5,6)
val y : bool = true
No warnings or errors from the F# 4.0 compiler.
P.P.S. When I tried to write in the F# Interactive:
let y = match x with LongIdent foo -> true
I received a compiler error FS0019: This constructor is applied to 1 argument(s) but expects 6.

