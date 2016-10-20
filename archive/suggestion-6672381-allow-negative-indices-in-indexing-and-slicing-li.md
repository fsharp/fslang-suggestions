# Allow negative indices in indexing and slicing like python [6672381] #

**Submitted by Gustavo Guerra on 11/6/2014 12:00:00 AM**  
**39 votes on UserVoice prior to migration**  

Example: permit usage of a.[..-2] instead of a.[..a.Length-1]
The compiler could just do that conversion behind the scenes, so it would work with existing types that have custom indexing and slicing



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6672381)**


## Comments ##


#### Comment by Kit Eason on 11/6/2014 6:32:00 AM ####
This would be so freakin' useful in the code I am writing right now!


#### Comment by Goswin on 11/10/2014 8:46:00 AM ####
I am not sure if this schould be default.
I am doing this with an extension member:
let inline getNegIndex i len =
let j = if i<0 then len + i else i
if j<0 || j >= len then failwithf "Cannot get index %d from %d items (for given negative index %d ) " j len i
else j
type ``[]``<'T> with
member inline arr.GetItemNeg i = arr.[getNegIndex i arr.Length]


#### Comment by Richard Gibson on 11/13/2014 5:15:00 AM ####
I remember this discussion coming up in CoffeeScript and it's surprisingly hard to do when you involve variables. For example:
arr.[..x] // Should the compiler insert a check to see if x is negative?


#### Comment by Brody Berg on 2/9/2015 1:13:00 PM ####
Here is the CoffeeScript discussion: https://github.com/jashkenas/coffeescript/wiki/FAQ
I don't think the CoffeeScript source-to-source compilation-time constraints apply to the F# compiler in this case.


#### Comment by Gusty on 9/29/2015 8:28:00 AM ####
I like it. FSharpPlus had that feature longtime:(https://github.com/gmpl/FSharpPlus/blob/0f0550000077cb9da3f340612a84911e92c1a790/FSharpPlus/Extensions.fs#L49)
note that the GetSlice there support also negatives at the beginning of the string.
But now I see that in F#4.0 it doesn't work anymore since GetSlice was added in the F# core (without the negatives) and shadows the method in F#+ so if this feature is not accepted an option would be to avoid shadowing those functions further defined in Libraries.
This way everybody is free to decide to use negative indexing by using a library or writing an extension method.

