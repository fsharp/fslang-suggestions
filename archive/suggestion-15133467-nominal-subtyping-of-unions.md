# Nominal subtyping of unions [15133467] #

**Submitted by exercitus vir on 7/9/2016 12:00:00 AM**  
**8 votes on UserVoice prior to migration**  

This is basically a repost of "subtyping for discriminated unions" (/archive/suggestion-6672490-subtyping-for-discriminated-unions), but with more details and a description of a concrete use case.
I am reposting because I would like more discussion on this and because I think that declined requests are no longer tracked by Don Syme (and others).
Don Syme declined the feature because he likes features to be generic and symmetric for types in F#. This is a good general rule and I trust in Don's good taste, but I think that this feature request is an exception to the rule, so the decline should be reconsidered for the following reasons:
Nominal subtyping cannot be implemented for records because records are compiled to sealed classes, which is a good thing and I see no use cases for subtyping of records anyway (there is also already ambiguity for records with the same fields that needs to be resolved manually with type annotations). So far we agree.
But this is completely different for unions. This feature only makes sense for unions because of the nature of unions (i.e. limited number of cases where subsets of cases can be fully handled by pattern matches of supersets). Unions are not compiled to sealed classes and there are many uses cases for subtype polymorphic unions. Nominal subtyping of unions is different from structural subtyping of unions (e.g. polymorphic variants in OCaml) in that it is completely safe (i.e. the compiler can still check for exhausiveness). There is also no technical reason that I see (other than maybe a more complex parser, which is an acceptable reason for declining this feature).
Here is a concrete example. Let's say you want to model a financial trading domain where a broker connects to multiple exchanges and submits orders to multiple exchanges. Each exchange supports a subset of a fixed number of possible order types (e.g. limit order, market order, stop limit order, stop market order, trailing stop order, fill or kill order, etc. ) and a subset of timing options for the order (Good Till Day, Good Till Cancel, Good Till Date, Immediate or Cancel, etc.).
Unions are perfect for that except that there is no way currently to generically work with order types and timing options from different exchanges (in a clean way). How would you do this right now in F# without lots of boilerlate and really ugly code (i.e. one interface or member constraint per supported case)?. This feature would allow to express the model directly and I am sure there are many more examples where this is really valuable.
What I value about F# the most is the expressiveness of it and this is the only feature (and higher-kinded types maybe) that do not let me express something cleanly.What do you think? Any issues with this that I am overlooking?



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/15133467)**


## Comments ##

