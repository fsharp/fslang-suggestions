# remove Seq.rev from FSharp.Core again [11602140] #

**Submitted by Steffen Forkmann on 1/27/2016 12:00:00 AM**  
**12 votes on UserVoice prior to migration**  

the collection regularization was a good idea. Unfortunately we introduced Seq.rev which internally converts to array. This working for most real-life sequences, but breaks laziness.
I suggest to mark the function as obsolete and remove it later.
See also https://github.com/Microsoft/visualfsharp/issues/902



## Response ##
** by fslang-admin on 2/4/2016 12:00:00 AM **

Marking as declined per my comments below.
That said, if you encounter situations where having Seq.rev has caused bugs, please contact me or post the details below. I’m still interested to know how often this bites in practice.
Don Syme, F# Language and Core Library Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/11602140)**


## Comments ##


#### Comment by Andrew Cherry on 1/27/2016 6:39:00 AM ####
Strongly agree. Having rev breaks an important mental model and is at some point going to be a source of the type of bugs that good type systems are designed to eliminate.


#### Comment by Mark Laws on 1/27/2016 6:42:00 AM ####
The potential implications of strictly evaluating the sequence by converting it to an array are dire--this function is a liability and ought to go.


#### Comment by Vasily Kirichenko on 1/27/2016 12:03:00 PM ####
Strongly agree.


#### Comment by Steffen Forkmann on 1/27/2016 12:46:00 PM ####
There was also the suggestion from Eirik that we change the signature to 'a seq -> 'a array to make the internal transformation more explicit


#### Comment by Don Syme on 1/28/2016 6:20:00 AM ####
Three somewhat obvious points:
* Several of the F# 2.0 Seq.* functions had the same implicit-loss-of-laziness property, for example Seq.groupBy and Seq.distinct. To be consistent we would also deprecate those. But I don't see us doing that after all this time.
* In general we avoid oscillating between design points: "which version am I on?" "Which functions can I use"? "How do I write code that works on all versions"?
* There are workarounds - e.g. define an obsolete Seq.rev in a common prelude shared by code you want to protect from implicit loss of laziness.
module Seq =
[<Obsolete("etc")>]
let rev xs = ...


#### Comment by NhlCrd on 1/31/2016 3:53:00 PM ####
+1 to Eirik's idea of making the signature explicit and returning an array.
It could also be applied to the other eager Seq.* functions that Don mentions. A lot of times you're perfectly OK with losing laziness, but it's best to know when that happens.
As far as I can't tell it shouldn't even break any existing code, outside of weird reflection corner cases.


#### Comment by Steffen Forkmann on 1/31/2016 4:02:00 PM ####
I think it's a interesting l idea, but it is breaking. And it's hard to make the transition easy with compiler warnings.


#### Comment by NhlCrd on 2/1/2016 8:39:00 AM ####
Since Array implements Seq, what sort of code would be broken by changing the signature?


#### Comment by Don Syme on 2/3/2016 10:42:00 AM ####
@NhlCrd - in compiled .NET code, the return type is significant in the "identity" of a function/method and effectively forms part of the linking data for a function. So changing the return type is a breaking change.
My inclination is to mark this as declined per my comments below.

