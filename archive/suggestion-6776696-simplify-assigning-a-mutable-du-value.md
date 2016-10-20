# simplify assigning a mutable DU value [6776696] #

**Submitted by Steven Taylor on 11/27/2014 12:00:00 AM**  
**4 votes on UserVoice prior to migration**  

please provide a simplified way to work with mutable discriminated union values similar to the simplified announcement [1].
The current scheme depends upon the ref keyword. It would be nice to replace ref with mutable, and then be able to use the cleaner <- operator rather than :=. This would then be more consistent for folk who get used to the "it just works" syntax (see [1]).
Instead of:
type AST = | Keyword of string ref
let theDuValue = AST.Keyword (ref "test")
let (Keyword(v)) = theDuValue in v := "new value"
we could have:
type AST = | Keyword of mutable string
let theDUValue = AST.Keyword ("test")
let (Keyword(v)) = theDUValue in v <- "new value"
It's a slightly contrived example, but this syntax does have has its uses.
An example in ref form from Microsoft.FSharp.Compiler (file: tast.fs)
TraitConstraintInfo =
| TTrait of TTypes * string * MemberFlags * TTypes * TType option * TraitConstraintSln option ref
member x.Solution
with get() = (let (TTrait(_,_,_,_,_,sln)) = x in sln.Value)
and set v = (let (TTrait(_,_,_,_,_,sln)) = x in sln.Value <- v)
Note: TraitConstraintSln uses the option type. The "<-" here has nothing to do with a simplified syntax
[1] http://blogs.msdn.com/b/fsharpteam/archive/2014/11/12/announcing-a-preview-of-f-4-0-and-the-visual-f-tools-in-vs-2015.aspx
Closed Today at 2:12 AM by latkin
Please open as a feature request at UserVoice
comments
* latkin wrote Today at 2:12 AM
* Thanks for the feature suggestion. We ask that language feature requests be opened and discussed at https://fslang.uservoice.com/.
* Take a look at http://stackoverflow.com/a/2221803/1366219 for a discussion on this topic. There are various complications and design considerations that come into play here.



## Response ##
** by fslang-admin on 7/18/2015 12:00:00 AM **

Many thanks for this suggestion. It is being marked as declined – for discussion see the comments.
Further comments, use cases, information and discussion welcome
Don Syme, F# Language and Core Library Evolution.


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6776696)**


## Comments ##


#### Comment by Don Syme on 7/18/2015 1:26:00 PM ####
I think it's best to just define a settable property on the DU that does what you want.

