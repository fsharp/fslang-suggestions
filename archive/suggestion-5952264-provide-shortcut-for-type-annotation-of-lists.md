# Provide shortcut for type annotation of Lists [5952264] #

**Submitted by Gulshanur Rahman on 5/21/2014 12:00:00 AM**  
**4 votes on UserVoice prior to migration**  

I suggest to provide a shortcut syntax ( `[<typname>]` ) for type annotation of F# Lists. Instead of this-
let upto (a:int): int list = [1..a]
I want to have-
let upto (a:int): [int] = [1..a]
Then list of list of int will be `[[int]]` instead of `int list list`. When type gets complex, we tend to use more brackets for clarity like- `(int list) list`. This proposed annotation should reduce some verbosity maintaining clarity. As in F#, `[..]` is already associated with lists, I am for using this in type also.



## Response ##
** by fslang-admin on 9/16/2014 12:00:00 AM **

Declining per my comment
Don Syme, Current BDFL F# Language/Library Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5952264)**


## Comments ##


#### Comment by Don Syme on 9/16/2014 5:23:00 AM ####
My feeling is that this is not appropriate for F#, given the existiing availability of "int[]" for arrays.

