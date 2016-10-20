# support flexible types in type alias [13412529] #

**Submitted by Gauthier Segay on 4/13/2016 12:00:00 AM**  
**1 votes on UserVoice prior to migration**  

Ability to define
type CreateCommand = unit -> #IDbCommand
instead of
type CreateCommand<'T when 'T :> IDbCommand> = unit -> 'T
because the later forces me to specify the generic type (even with _) at places I'm using it.
I'm not clear if there are cases where it would create issues, but it would be nice to have some explicit ways to tell we are ok with implict polymorphism.



## Response ##
** by fslang-admin on 6/13/2016 12:00:00 AM **

Declined per my comment below
Don Syme
F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/13412529)**


## Comments ##


#### Comment by Don Syme on 6/13/2016 5:16:00 AM ####
This seems to create too many issues to make it feasible. It's effectively like adding a form of existential type to the language, since you're really defining
type CreateCommand = EXISTS ('T :> IDbCommand). unit -> 'T
That's not a trivial thing to add to F#

