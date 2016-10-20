# The base keyword shouldn't be a keyword. [6528970] #

**Submitted by Robert Fuszenecker on 10/6/2014 12:00:00 AM**  
**5 votes on UserVoice prior to migration**  

As the 'this' pointer is not a keyword, the 'base' identifier shouldn't be, too. We could use the form i.e.
type Derived() =
inherit Base() as someBase
member myDerived.Print() =
someBase.Print()



## Response ##
** by fslang-admin on 10/15/2014 12:00:00 AM **

See comment above.
To elaborate, the decision to make “base” a keyword as distinct from naming “this” was made in F# 1.×. We did consider allowing the naming of “base”, but decided against it, preferring to keep the OO-inheritance-base-call mechanism (which is kind of unpleasant) very syntactically distinct from the ability to name and recursively refer to “this” (which in to some extent can be used in nicely functional ways).
In general when decisions like this have already been made and are known, stable, tested and documented, then we are unlikely to change the decision unless it’s really critical to do so.
Thanks
Don Syme, BDFL F# Language/Core Library Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6528970)**


## Comments ##


#### Comment by Anonymous on 10/6/2014 2:00:00 PM ####
Hi,
Could be great in a more F#-ish way, i.e. inherit someBase = Base()


#### Comment by Loic Denuziere on 10/14/2014 9:45:00 AM ####
@Anonymous: I prefer Robert's proposal because it mirrors the "as this" syntax that we already have.


#### Comment by Don Syme on 10/15/2014 7:19:00 AM ####
I don't see there's anything much to be gained with changing this decision at this point. If you need to use "base" then use ``base``.

