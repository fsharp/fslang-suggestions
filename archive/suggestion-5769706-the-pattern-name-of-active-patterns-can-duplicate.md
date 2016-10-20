# The pattern name of Active Patterns can duplicate define [5769706] #

**Submitted by Anonymous on 4/13/2014 12:00:00 AM**  
**3 votes on UserVoice prior to migration**  

When input parameters different from each other, the pattern name of Active Patterns can duplicate define, It will be cool as below.
[<AutoOpen>]
module ActiveModule=
let (|HasError|HasNotError|) (input:QueryResult)=
if input.HasError then HasError (input:>ResultBase)
else HasNotError (input.ResultData)
let (|HasError|HasNotError|) (input: ExecuteResult) =
if input.HasError then HasError (input:>ResultBase)
else HasNotError input



## Response ##
** by fslang-admin on 6/20/2014 12:00:00 AM **

Realistically, we’re not going to add this to the active pattern feature.
Type-directed overloading of this kind doesn’t fit well with the feature.
If active patterns could be defined on objects as members we might consider adding type-directed overloading like this.
Declining this for now to recycle votes.
Don Syme


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5769706)**


## Comments ##

