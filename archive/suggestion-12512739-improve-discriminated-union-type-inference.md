# Improve Discriminated Union Type Inference [12512739] #

**Submitted by Steven Taylor on 2/29/2016 12:00:00 AM**  
**1 votes on UserVoice prior to migration**  

Sometimes the most logical name for an element of a Discriminated Union (DU), is a common concept such as a list
-- something that you've used before elsewhere.
The only way around the last resolved resolution is either through namespaces, or by adopting a naming convention.
Sometimes getting nagged about name overuse can lead to clearer code, but what if our intention is exactly as
written? In the below, if we named elements to be ListOfA and ListOfB, then the problem goes away.
Sounds and often is simple, but it can lead to additional code noise and moves us away ever so slightly
from the problem domain.
type A =
| Element
| List of A list
type B =
| ElementB
| List of B list
let u : B = List([]) // okay : takes last defined
let v : A = List([]) // fails : last defined is B
let w = List([]) : A // fails : ignores hint
let x = A.List([]) // okay : fully qualified
let y = List([ElementA]) // fails : expects ElementA
note: this request is similar to this accepted request /archive/suggestion-7138324-record-based-improve-type-inference-bug?tracking_code=3364d3565b19a0c518474dccbc2a1ec0



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/12512739)**


## Comments ##

