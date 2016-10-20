# Extend `with` keyword support to record definitions [8107647] #

**Submitted by Dax Fohl on 5/25/2015 12:00:00 AM**  
**8 votes on UserVoice prior to migration**  

In the process of converting a large-ish Clojure app to F#, which I prefer due to the type safety, I find many situations where I have large records that differ by only an item or two.
For instance, in Clojure, I grab a user's huge configuration record from the DB, and then append a couple of calculated fields to it before returning to the next layer. So that means in F#, I need
type UserDbData = {...many fields..}
type UserData = {...many fields... ...calculated fields}
let createUserData(dbData:UserDbData) = {...many fields=many fields... ...calculated fields = calculate fields...}
let createUserDbData(userData:UserData) = {...many fields=many fields...}
It would be great to have language support for these situations, where you could define
type UserDbData = {fields}
type UserData = {UserDbData with other fields}
let createUserData(dbData:UserDbData) = {dbData with other fields}
let createUserDbData(userData:UserData) = {userData ::>> UserDbData} //or something like that
As to whether this would be done under the hood by inheritance or whether it's just shorthand for a new otherwise-unrelated record type, I can see pros and cons of each. I somewhat lean toward the latter.



## Response ##
** by fslang-admin on 2/5/2016 12:00:00 AM **

Thanks for the suggestion. I’ve merged it with /archive/suggestion-5673015-support-c-like-anonymous-types-in-f
Don Syme
F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/8107647)**


## Comments ##


#### Comment by Dax Fohl on 5/28/2015 7:59:00 AM ####
One reason inheritance might be the better option is that if the types are otherwise unrelated, is that you wouldn't be able to use a UserData in a function that accepts UserDbData, so that may lead to a bunch of logic duplication. But record inheritance seems antithetical to F#, so I just don't think I'd go that way.
So, this maybe would need to be combined with a structural typing feature (again, similar to Clojure where you do have named records but can add extra fields, but in F# that would be structurally-verified at compile time).
Or some statically-resolved type constraint feature would also work:
let myFunc<^user when ^user ::?>> UserDbData>(user: ^user) = ...


#### Comment by Nathan-Madonna Byers on 6/1/2015 1:07:00 PM ####
Something similar to Elm's record types (see http://elm-lang.org/learn/Records.elm) would be really useful in F#.


#### Comment by exercitus vir on 6/12/2015 8:21:00 PM ####
If they are related, then you could make them classes and inherit the base class and add the extra fields there. If you want the simplicity of records, then you could wrap the base record as a component of the record with additional fields.


#### Comment by Don Syme on 2/5/2016 5:10:00 AM ####
This is really related to the question of C#-style anonymous types for F#, since you are effectively making up a type definition on the fly. I will close this suggestion in favour of /archive/suggestion-5673015-support-c-like-anonymous-types-in-f and link it there.

