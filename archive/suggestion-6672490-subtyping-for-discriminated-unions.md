# subtyping for discriminated unions [6672490] #

**Submitted by exercitus vir on 11/6/2014 12:00:00 AM**  
**4 votes on UserVoice prior to migration**  

We need be able to explicitly specify (structural) subset relationships of discriminated unions (similar to polymorphic variants in OCaml but defined at type definition). There are many uses cases for this.
For example:
type Superset = A | B | C
//structural subset relation must be explicitly declared, but only in the definition
type Subset :> Superset = A | B
//no need to repeat subset relation because a superset can always handle all cases of any subset
let accept_subset (superset : Superset ) =
match superset with
| A -> "A"
| B -> "B"
| C -> "C"
//it does not matter that A is ambiguous (Superset.A and Subset.A) because subset case would be cast to Superset type anyway
//but it should also be possible to specify Subset.A, which would be cast to the Superset type
let accepted_subset = accept_subset A
let accept_superset (subset : Subset ) =
match subset with
| A -> "A"
| B -> "B"
//it does not matter that A is ambiguous (Superset.A and Subset.A) because superset case would be cast to Subset type anyway
//but it should also be possible to specify Superset.A, which would be cast to the Subset type
let accepted_superset = accept_superset A
This would not break backwards compatibility as it is currently possible to hack this together using explicit static member constraints and additional interfaces (one interface per case), but that is really ugly and repetitive.



## Response ##
** by fslang-admin on 2/5/2016 12:00:00 AM **

Many thanks for the suggestion. I’ve declined it per my comment below, please see what I wrote there
Best wishes
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6672490)**


## Comments ##


#### Comment by exercitus vir on 6/14/2015 1:21:00 PM ####
I just realized that this is enables nominal subtype polymorphism, not structural subtype polymorphism since the subtype relationship is made explicit with `:>`.


#### Comment by Don Syme on 2/5/2016 9:14:00 AM ####
I renamed the suggestion to clarify that it is about introducing new nominal subtypes.
This is definitely an interesting idea. Of course it's the natural partner to allowing nominal subtyping on records, which we don't allow
Although this is a fascinating suggestion, my inclination is that I have to decline this simply because I would decline the corresponding nominal-subtyping-on-records feature.


#### Comment by exercitus vir on 7/9/2016 10:47:00 AM ####
I don't understand the reason for declining this. Could you please reconsider?
I can see no use cases for subtyping of records, but there are common use cases for subtyping of unions. Not all F# features need to be symmetric.

