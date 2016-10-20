# Allow the syntax 1<=x<10 [5683305] #

**Submitted by Jon Harrop on 3/26/2014 12:00:00 AM**  
**17 votes on UserVoice prior to migration**  

This traditional mathematical notation is only allowed in a few elite programming languages. I would like F# to be one of them!
At the moment you have to write 1<=x && x<10.
Of course, what I really want is 1≤x<10 but we've got to start somewhere. ;-)



## Response ##
** by fslang-admin on 6/25/2014 12:00:00 AM **

This is a duplicate of /archive/suggestion-5726029-support-conjunctional-operator


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5683305)**


## Comments ##


#### Comment by Mastr Mastic on 4/3/2014 1:51:00 AM ####
I love this, and as for the last sentence I'd like to add that I always dream of the day languages would freely let you use Unicode and IDEs would allow you to insert them easily from your keyboard (like Windows does in some foreign languages). Especially when it comes to functional programming.


#### Comment by Goswin on 4/8/2014 3:39:00 AM ####
you could write 1 <. x .< 10 using these custom operators:
///* Point must be at middle of expression: like this: min <=. x .<= max
let inline (<=.) left middle = (left <= middle, middle)
let inline (.<=) (leftResult, middle) right = leftResult && (middle <= right)
let inline (>=.) left middle = (left >= middle, middle)
let inline (.>=) (leftResult, middle) right = leftResult && (middle >= right)
// Point must be at middle of expression: like this: min <. x .< max
let inline (<.) left middle = (left < middle, middle)
let inline (.<) (leftResult, middle) right = leftResult && (middle < right)
let inline (>.) left middle = (left > middle, middle)
let inline (.>) (leftResult, middle) right = leftResult && (middle > right)


#### Comment by Steve Gilham on 4/10/2014 3:56:00 AM ####
This is the same suggestion as /archive/suggestion-5726029-support-conjunctional-operator

