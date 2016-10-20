# Allow infix notation on functions [5663255] #

**Submitted by Colin Bull on 3/21/2014 12:00:00 AM**  
**32 votes on UserVoice prior to migration**  





## Response ##
** by fslang-admin on 2/4/2016 12:00:00 AM **

Marking as declined per my comment below


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5663255)**


## Comments ##


#### Comment by Steve Gilham on 4/10/2014 4:11:00 AM ####
This is an ML feature, so is not something new to the language familty
Whether this is done by something like an #infix pragma (there being no suitable reserved keyword), or by a compiler flag that allows functions named `op_<whatever>` to be invoked as infix operators `<whatever>` (inverting the current behaviour where operators compile to functions `op_<something>` which can be invoked by that mangled name in prefix -- or even allows things like `let (myOperator) = ...` compile to infixable `myOperator` and prefixable `op_myOperator` for arbitrary identifier `myOperator`.


#### Comment by Don Syme on 2/4/2016 12:59:00 PM ####
We decided in F# 1.0 not to allow fixity to depend on scope, and that like OCaml we would have a fixed set of precedences. This simplifies the implementation and also means that parsing is independent of the set of files referenced or namespaces opened.
My inclination is to apply the rule that nothing specific has changed that would lead us to revisit this decision, so we should stick with it.

