# custom set the 'last defined' [12951354] #

**Submitted by Steven Taylor on 3/15/2016 12:00:00 AM**  
**1 votes on UserVoice prior to migration**  

Say we implement something like:
type BinaryOp =
| And
| Or
| Not
| None
module test =
let aMatchFunction (s:string option) = match s with
| Some s -> printfn "%s" s
| None -> printfn "(none)"
// Error This expression was expected to
// have type string option but here has
// type BinaryOp
Some of the F# conventions are nice, and it'd be good to be able to stay consistent with them across our code base if we choose. In this case, I feel we shouldn't be forced to adopt the longhand convention of:
Option<string>.None just to get the point across to the compiler. Likewise, pushing the definition up the tree -- ie. in this case (aVarName : BinaryOp option) is not always the sensible thing to do.
This is just a simple example where it doesn't make much difference one way or the other. I suggest we have more preferences for hints and context. Pithy code probably leads to more name clashes. Sometimes these are acceptable.



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/12951354)**


## Comments ##

