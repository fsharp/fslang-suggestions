# add a keyword for module-local construction but public deconstruction of types [12913179] #

**Submitted by Adnan Gazi on 3/12/2016 12:00:00 AM**  
**5 votes on UserVoice prior to migration**  

Similar to dependant types, except you wouldn't enforce the predicate on which the type is dependant on to be defined WITH the type.
This keyword could stop clients of a module from constructing the type, but would allow them to 'see' that it exists, and therefore allow them to deconstruct it for their own use.
For example, if you want a string constrained to 50 chars, you could have
type String50 = constrained String50 of string
let createString50 s = if String.length s <= 50 then Some s else None
where 'createString50' is a constructor.
Correct me if I am mistaken, but it seems to be a lot less complicated than dependant types since the dependancy is implicit, and therefore wouldn't be as difficult for the type inference



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/12913179)**


## Comments ##


#### Comment by trek42 on 3/17/2016 9:01:00 PM ####
I think this is a good idea. Similarly for record types, it would be very useful to restrict record type so that external (outside of the module) user code can use the fields (like A.field), but not construct the record or use the { A with field =... } syntax. Having this restriction for records can make code maintenance a lot easier, especially when adding new fields or new invariants among fields we are sure the invariants are always held.
Probably it's better to use an attribute instead of a keyword. Something like [<PrivateConstructor>] would be good.
A new

