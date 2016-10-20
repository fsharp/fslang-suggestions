# Extended record with syntax to work with nested properties [5663252] #

**Submitted by Gustavo Guerra on 3/21/2014 12:00:00 AM**  
**35 votes on UserVoice prior to migration**  

let's say we have the following:
type RecordA =
{ A : int
B : string }
type RecordB =
{ A : bool
B : RecordA }
let a = { A = false
B = { A = 2
B = "foo" } }
and want to update that 2 to a 3.
Currently, we need to do this:
let a' = { a with B = { a.B with A = 3 } }
which doesn't scale to more complex types
It would be nice to have something like
let a' = { a with B.A = 3 }
or something similar
It would also be nice to be able to have something similar with DUs:
type DU =
| Case of p1:int * p2:string
let a = Case(1, "foo")
let a' = { a with p1 = 2 }



## Response ##
** by fslang-admin on 2/4/2016 12:00:00 AM **

Closed in favour of /archive/suggestion-6906132-implement-first-class-lensing-lenses-in-f per comment below
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5663252)**


## Comments ##


#### Comment by Mark Seemann on 3/22/2014 3:40:00 AM ####
This sounds like a good idea.
Apologies if I don't understand this well enough, but isn't this really asking for Lenses in F#? http://bugsquash.blogspot.dk/2011/11/lenses-in-f.html


#### Comment by Don Syme on 2/4/2016 1:56:00 PM ####
I am going to close this in favour of /archive/suggestion-6906132-implement-first-class-lensing-lenses-in-f
That doesn't mean we would implement first-class lensing. But I think the linked issue opens up several important parts of the design discussion, for example how would this work on class types that are not record types (and also how would this work for collection types). At least we should look at the topic of functional update a bit more holistically than this specific request, even if in the end this is all we do.

