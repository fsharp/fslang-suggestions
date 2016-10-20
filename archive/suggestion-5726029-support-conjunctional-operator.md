# Support conjunctional operator [5726029] #

**Submitted by bleis-tift on 4/3/2014 12:00:00 AM**  
**27 votes on UserVoice prior to migration**  

'a < x < b' means 'a < x && x < b'. (but x is evaluate only once)
Python implements this feature.



## Response ##
** by fslang-admin on 7/18/2015 12:00:00 AM **

I’m declining this because I feel the added expression form doesn’t make the very high bar for adding new expression constructs to the language. See the discussion for other comments.
Further input and discussion welcome
Don Syme, F# Language and Core Library Evolution.


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5726029)**


## Comments ##


#### Comment by Will Smith on 4/4/2014 3:10:00 AM ####
similar /archive/suggestion-5683305-allow-the-syntax-1-x-10


#### Comment by Goswin on 4/8/2014 3:52:00 AM ####
until this feature comes you could write 'a <. x .< b' by using these custom operators:
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


#### Comment by bleis-tift on 4/8/2014 4:50:00 AM ####
@Goswin
I want to write the code like this:
0 < x < y < ... < 100
Your approach needs more operators like the following:
let inline (.<.) (leftResult, middle) right = (leftResult && middle < right, right)
// and more...
0 <. x .<. y .<. ... .< 100
Dots are too noisy...


#### Comment by Don Syme on 6/20/2014 9:24:00 AM ####
My gut feeling is that this special case doesn't "make the cut", though the fact it is in Python is interesting and speaks in its favour.
Do we have ny information on how often is this used in Python?

