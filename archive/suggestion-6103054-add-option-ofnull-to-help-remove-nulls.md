# add Option.ofNull to help remove nulls [6103054] #

**Submitted by Cameron Taggart on 6/26/2014 12:00:00 AM**  
**13 votes on UserVoice prior to migration**  

Many APIs and types support the use of null. To help remove null and promote the use of option, It would be good to add a standard function that can be used to wrap nullable types.
May be something like:
type Option<'A> with
static member ofNull (t:'T when 'T : null) = function
| null -> None
| x -> Some x
http://stackoverflow.com/questions/24418816/in-the-f-api-is-there-something-like-option-ofnull



## Response ##
** by fslang-admin on 1/21/2015 12:00:00 AM **

Completed for F# 4.0, see https://visualfsharp.codeplex.com/SourceControl/network/forks/dsyme/cleanup/contribution/7672
Don Syme, F# Language/Library Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6103054)**


## Comments ##


#### Comment by Cameron Taggart on 6/26/2014 6:27:00 PM ####
Or just:
type Option<'A> with
static member ofNull (t:'T when 'T : null) =
if t = null then None else Some t


#### Comment by Ruben Bartelink on 6/26/2014 6:38:00 PM ####
or call it Option.ofObj


#### Comment by Jerold Haas on 6/28/2014 12:03:00 AM ####
Perhaps the name isn't perfect, but I fully support the elimination of nulls by wrapping them.
Other names suggested, indicating its use outside Option<'A>: "deNull, tryNull, nullToOption, toOption"


#### Comment by Vasily Kirichenko on 6/28/2014 1:50:00 AM ####
I think it's not very productive to add one function at a time. Someone made a PR that contained only single function (Option.filter).
I suggest to pull all useful functions from here https://github.com/jack-pappas/ExtCore/blob/master/ExtCore/Pervasive.fs#L705 and here https://github.com/fsprojects/fsharpx/blob/master/src/FSharpx.Core/ComputationExpressions/Monad.fs#L84, discuss the list and add them all at once, including the tests.


#### Comment by Dave Thomas on 6/28/2014 3:40:00 AM ####
Integrating ExtCore would be nice, it's very well thought out and optimised.


#### Comment by Isaac Abraham on 7/3/2014 8:12:00 AM ####
Mapping between Nullable<T> and Option<T> would also be useful.


#### Comment by Don Syme on 11/10/2014 11:27:00 AM ####
I have submitted a PR with names Option.ofObj and Option.toObj, see https://visualfsharp.codeplex.com/SourceControl/network/forks/dsyme/cleanup/contribution/7672


#### Comment by George on 6/3/2015 1:09:00 PM ####
Excellent idea.
Also Option.ofNullable for mapping System.Nullable<T> into F# Option types and converse operations Option.toObj and Option.toNullable to map options to reference and value types, respectively.

