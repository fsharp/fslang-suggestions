# Add constraints as a language construct [8509687] #

**Submitted by Jared Hester on 6/22/2015 12:00:00 AM**  
**36 votes on UserVoice prior to migration**  

Allow the declaration of named constraints that can have other named constraints nested within them and are resolved at runtime or compile time based on their structure , e.g.
constraint (^a:eatsDrinksSleeps) =
when ^a : equality
and ^a : comparison
and ^a : (static member Hungry: bool)
and ^a : (member chews: string -> bool)
and ^a : (member drinks: float -> bool)
and ^a : (member sleepsFor: float with get,set)
let inline go_wild (beast:^a when ^a: eatsDrinksSleeps) = ...
--------------------------------------------------------------------------------
They could also be defined on flexible types that take generic parameters -
constraint (#seq<'a> : greatData) =
when 'a: struct
and 'a: comparison
and 'a: equality
let calc (col:'a when 'a:greatData) = ....



## Response ##
** by fslang-admin on 2/10/2016 12:00:00 AM **

Thanks for the suggestion. It is entirely reasonable and it’s taken me a long time to mark it as declined. I’ve listed the reasons below – and /archive/suggestion-5762135-support-for-type-classes-or-implicits can be used as a placeholder for requests in the type-class/constraint area
Don Syme
F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/8509687)**


## Comments ##


#### Comment by exercitus vir on 6/22/2015 3:32:00 PM ####
Related suggestion: /archive/suggestion-8393964-interfaces-as-simple-reusable-and-named-sets-of-m?tracking_code=bd9d860150afdb439a2ef3ab649e0374
The advantage of that suggestion is that it simplifies the syntax of explicit member constraints, does not require a new keyword (albeit a new operator) and can reuse existing interfaces and its syntax.


#### Comment by Don Syme on 2/4/2016 6:49:00 PM ####
This gist shows how to name collections of member constraints today: https://gist.github.com/dsyme/bfed2eed788c7ba58ccc


#### Comment by Don Syme on 2/10/2016 11:19:00 AM ####
Because it is already possible to name sets of constraints using the technique below, I am going to decline this request. Also the request /archive/suggestion-5762135-support-for-type-classes-or-implicits is overlapping and can be used to cover the general suggestion to have a trait/constraint/type-class facility in the language


#### Comment by Gauthier Segay on 2/28/2016 7:31:00 AM ####
Don, in your gist, you can't use the members without restating the constraints, what the point?
I think Jared was after something like this:
let inline go_wild (beast:^a when ^a: eatsDrinksSleeps) =
(* *) beast.chews "snack"
(* *) beast.drinks "potion"
(* *) if not beast.Hungry then printfn "BURP!"
not something which force to state the constraint in a cryptic way at each usage of beast.


#### Comment by William Blum on 5/1/2016 11:08:00 PM ####
Thanks Don for sharing the Gist but unfortunately the type alias trick does not solve the problem for purely static member constraints. In the following example for instance I want to express the same set of constraints for both ^T1 and ^T2 without having to repeat them.
type Combine< ^T1,^ T2 when
^T1 : (static member print : string -> unit)
and ^T1 : (static member flush : unit -> unit)
and ^T2 : (static member print : string -> unit)
and ^T2 : (static member flush : unit -> unit)
> =
static member inline printAndFlushBoth m =
(^T1:(static member print : string -> unit) m)
(^T2:(static member print : string -> unit) m)
(^T1:(static member flush : unit -> unit) ())
(^T2:(static member flush : unit -> unit) ())
Following your gist I could define a type alias encoding the two constraints (write and flush) but my constraints being entirely static I have no way to refer to the type alias it in a type annotation since there exist no variable of static type.
Another benefit of named constraints is that the 'comparison' and 'equality' constraints could be defined in the F# core library instead of being hard-coded in the language.
Do you have another trick up your sleeve for the above example? If not, would you consider reopening this suggestion?

