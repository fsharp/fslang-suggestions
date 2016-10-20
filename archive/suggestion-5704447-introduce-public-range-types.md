# Introduce public Range types [5704447] #

**Submitted by Eirik George Tsarpalis on 3/31/2014 12:00:00 AM**  
**10 votes on UserVoice prior to migration**  

Range types exist in F#, as they manifest themselves in computation expression for loops:
for i in 1 .. 100 do ()
These take the form of internal IEnumerable implementations. Therefore, one cannot define a .For method override that only permits range types at its domain, instead having to cover all possible IEnumerable's.
Why could this be a problem, you may ask? It is the case that many IEnumerators are not serializable, whereas certain computation expressions inherently demand a persistable execution state. In such cases we are forced to only support concrete manifestations of collections such as arrays, resulting in the following inefficient and awkward use:
for i in [| 1 .. 100 |] do ()
Making Range types public would remedy this issue.



## Response ##
** by fslang-admin on 2/5/2016 12:00:00 AM **

Declined, per my comment, thanks!
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5704447)**


## Comments ##


#### Comment by Don Syme on 2/5/2016 4:13:00 AM ####
My understanding is that one way to solve this is to make sure the enclosing cloud/monadic computation has a Delay method.


#### Comment by Don Syme on 2/5/2016 4:14:00 AM ####
I will close this as I don't think chasing down non-serializable sequence objects one by one is the way we will solve this?

