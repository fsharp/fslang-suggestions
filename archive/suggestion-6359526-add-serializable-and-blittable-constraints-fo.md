# Add 'serializable' and 'blittable' constraints for types [6359526] #

**Submitted by Eirik George Tsarpalis on 8/28/2014 12:00:00 AM**  
**3 votes on UserVoice prior to migration**  

I think it would be a good idea to let the F# compiler reason about serializable types. This could be implemented along the lines of the 'comparison' constraint, i.e. based upon an assortment of criteria for deciding when it is satisfied.
For instance, a type could be statically deemed serializable iff
* it is primitive, string, byte array, etc.
* It is a subtype of System.Exception
* it is a managed class or struct that carries the Serializable attribute.



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6359526)**


## Comments ##


#### Comment by thinkb4coding on 8/28/2014 11:07:00 AM ####
That could be useful, it would avoid knowing this only at runtime.. But It makes me wonder if it could not be more generic and that you could create your own constraint that would run at design and compile time (like done with Type Providers)..
This way you could check various things about types used in a function to validate that behavior will be correct then at runtime... thoughts ?


#### Comment by Eirik George Tsarpalis on 8/28/2014 11:48:00 AM ####
@thinkb4coding you mean having arbitrary pluggable type predicates? I'm not even sure what the consequences would be to that.


#### Comment by Don Syme on 2/4/2016 6:13:00 PM ####
I've combined this with the suggestion for "blittable" types: /archive/suggestion-9989010-add-blittable-type-constraints-in-order-to-support


#### Comment by exercitus vir on 7/8/2016 2:12:00 PM ####
I think "serializable" and "blittable" are two completely different issues and should be kept seperate. Serialization is an abstract concept that can apply to any proper data type and "blittable" seems to be about unmanaged types (I don't really understand what blittable means).
I find serialization via attributes and Reflection less than ideal (slow and unsafe). The C# team actually wants to get away from serialization via Reflection.

