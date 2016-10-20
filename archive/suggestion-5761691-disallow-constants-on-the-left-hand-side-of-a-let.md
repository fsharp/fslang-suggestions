# Disallow constants on the left hand side of a let binding [5761691] #

**Submitted by john palmer on 4/12/2014 12:00:00 AM**  
**4 votes on UserVoice prior to migration**  

Currently, the following code is valid
let 1 = 1
This will compile (and produce a warning) and is fine at run time.
Even more confusingly, this will compile
let 1 = 2
but it will fail at run time with a match failure exception.
The reason for this behavior is that currently the left hand side of the `let` can be anything used in a `match`. In the case of `match`, allowing constants makes sense, but for let this makes no sense.
According to Don, apparently some people write
let () = ...
instead of

do ....
so it might be possible to allow the unit literal, but not say int or string.
This will actually require a change to the spec, but it is relatively minor



## Response ##
** by fslang-admin on 6/20/2014 12:00:00 AM **

In my view, the warning is sufficient, as discussed above.
Declining this for now to recycle votes.
Thanks
Don Syme


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5761691)**


## Comments ##


#### Comment by Keith Battocchi on 4/14/2014 11:27:00 PM ####
This would be a breaking change, and the code you'd outlaw is reasonable (if not idiomatic) as a shorthand for asserting that a value is known. You say that the current behavior is confusing, but has anyone ever used it mistakenly? I don't see any real benefit to disallowing it.


#### Comment by Loic Denuziere on 4/24/2014 3:19:00 PM ####
I think the current behaviour of throwing a warning is sufficient. Keeping consistency (ie. `let` behaves exactly like `match`) is more important IMO.


#### Comment by Bryan Edds on 4/24/2014 8:04:00 PM ####
I don't know why anybody would write `let () = expr` when they could more idiomatically write `let _ = expr`...


#### Comment by Bryan Edds on 4/24/2014 8:08:00 PM ####
I don't know why anybody would write `let () = expr` when they could more idiomatically write `let _ = expr`...
As to keeping syntactic similarity between let and match, I think that's conceptually baseless. There's no semantic relationship between them, AFAICT.


#### Comment by Loic Denuziere on 4/25/2014 11:36:00 AM ####
There is a semantic relationship between let and match:
let <pattern> = x in y
is equivalent to
match x with <pattern> -> y
As for `let ()` vs `let _`, the former makes it explicit that the type of `expr` is unit, whereas the latter leaves a doubt as to whether we're ignoring a value that could be useful. But anyway `do` does it just as well; I suspect people only use `let ()` because they come from OCaml where you can't use `do` for this purpose.

