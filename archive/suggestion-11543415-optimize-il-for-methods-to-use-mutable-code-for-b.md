# Optimize IL for methods to use mutable code for better performance [11543415] #

**Submitted by knocte on 1/22/2016 12:00:00 AM**  
**1 votes on UserVoice prior to migration**  

It turns out that using immutable algorithm is not always the best thing in regards to performance. An interesting story about this is http://viralfsharp.com/2015/12/27/look-and-say-f/
So mutable code can actually be better in regards to performance (because it involves less allocations?). So maybe, in the cases in which it can be assured that no race condition can happen (i.e. mutable locals instead of mutable fields, because the former cannot be shared between threads), the F# compiler should try to optimize the IL generated for methods, to mutable-locals-optimized IL.
An example of how Streams could be optimized: https://github.com/nessos/Streams



## Response ##
** by fslang-admin on 1/23/2016 12:00:00 AM **

I’m marking this as declined since the proposal is not concrete enough. What specific design changes are proposed?
The Streams library is great, but can already be used from F#, as can most other mutable programming techniques.
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/11543415)**


## Comments ##


#### Comment by knocte on 1/25/2016 2:57:00 AM ####
Thanks for your reply Don, inline:
> What specific design changes are proposed?
My general wandering here is 'can what Nessos has accomplished, be completely automated at the IL-optimization level?'.

