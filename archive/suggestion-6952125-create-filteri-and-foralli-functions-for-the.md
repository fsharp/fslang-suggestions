# Create 'filteri' and 'foralli' functions for the various collections Array, List, Seq [6952125] #

**Submitted by Richard Dalton on 1/11/2015 12:00:00 AM**  
**13 votes on UserVoice prior to migration**  

mapi allows us to map a collection using not just the items in the collection but also the index of each item.
Could we do something similar with filter?
let nums = [0; 1; 2; 3; 4; 5; 6; 7]
let atEvenPos = List.filteri (fun i x -> i%2=0) nums
Result
atEvenPos = [0; 2; 4; 6]



## Response ##
** by fslang-admin on 2/4/2016 12:00:00 AM **

Declined per my comment below – using Seq.indexed is enough in F# 4.0, though if necessary the user can write fresh functions explicitly.
Don Syme, F# Language and Core Library Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6952125)**


## Comments ##


#### Comment by Don Syme on 7/18/2015 1:40:00 PM ####
Combining this with /archive/suggestion-6368913-add-array-foralli to cover both "filteri" and "foralli"


#### Comment by Don Syme on 2/4/2016 5:51:00 PM ####
In F# 4.0 we added List/Array/Seq.indexed, that's enough to satisfy the most common use cases for these without exploding the range of possible functions.

