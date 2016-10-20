# Make call syntax simpler for statically resolved member constraints [8014059] #

**Submitted by Andrzej Kukuła on 5/18/2015 12:00:00 AM**  
**29 votes on UserVoice prior to migration**  

The idea is basically explained by the following code:
// this works as expected
type Example() =
member __.F(i) = printfn "%d" i
let inline f (x : ^a) =
(^a : (member F : int -> unit) (x, 1))
(^a : (member F : int -> unit) (x, 2))
f (Example())
// this doesn't work
let inline f (x : ^a when ^a : (member F : int -> unit)) =
// the compiler knows that there must be member F and its signature
// so the following should be possible
x.F(1)
x.F(2)
You can also view this code highlighted at http://pastebin.com/CHMj7xQG



## Response ##
** by fslang-admin on 2/4/2016 12:00:00 AM **

Approved in principle. Thanks for the suggestion.
We will add an RFC for this in due course, see https://github.com/fsharp/FSharpLangDesign/blob/master/RFCs
We will need to consider whether to simplify calls for static members as well.


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/8014059)**


## Comments ##


#### Comment by exercitus vir on 6/12/2015 6:32:00 PM ####
Oh yes, much more readable!
I have incorporated your suggestion in my suggestion for "Interfaces as simple, reusable and named sets of member constraints on statically resolved type parameters": /archive/suggestion-8393964-interfaces-as-simple-reusable-and-named-sets-of-m


#### Comment by Don Syme on 2/4/2016 5:35:00 PM ####
I think this is totally reasonable, marking it as approved-in-principle.
Note also that a naked type alias can imply multiple constraints, giving a way to name collections of constraints
https://gist.github.com/dsyme/bfed2eed788c7ba58ccc

