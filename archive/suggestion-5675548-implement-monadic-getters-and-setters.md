# Implement monadic getters and setters [5675548] #

**Submitted by Anonymous on 3/24/2014 12:00:00 AM**  
**3 votes on UserVoice prior to migration**  

The get/set syntax for F# is very cool, but it has an issue: sometimes, the property we would like to get and set is only available through a workflow/monad, like the async workflow.
Thus, I would like to alter the typechecking rules for getters and setters. This is what they are right now (pseudocode) for the Async monad:
Property x : Async<'a>
get : unit -> Async<'a>
set : Async<'a> -> unit
IndexedProperty x : 'k -> Async<'v>
get : 'k -> Async<'v>
set : 'k -> Async<'v> -> 'unit
This is what I would like to see made possible:
type Id<'a> = 'a
Property x : Async<'a>
get : unit -> Async<'a>
set : 'a -> Async<unit>
IndexedProperty x : 'k -> Async<'v>
get : 'k -> Async<'v>
set : 'k -> 'v -> Async<unit>



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5675548)**


## Comments ##


#### Comment by Mauricio Scheffer on 3/24/2014 6:50:00 PM ####
Interesting, could you post a snippet illustrating how the current syntax/typechecking is insufficient, and how this suggestion would make it better?


#### Comment by Don Syme on 2/3/2016 2:59:00 PM ####
I am very sympathetic to this proposal. However, please note that the items would likely not be "proper" .NET properties since those are required to have "unit" return type on the setter method.

