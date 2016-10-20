# Add Haskell-style operator sections [7067304] #

**Submitted by luketopia on 2/7/2015 12:00:00 AM**  
**21 votes on UserVoice prior to migration**  

Imagine that you have a list of integers, and you want to filter it down to all the numbers greater than 10. You might erroneously try to partially apply the greater than operator as follows:
nums |> Seq.filter ((>) 10)
Unfortunately, this won't have the intended effect, because the arguments are applied to the operator in the wrong order. To get the intended effect you have to do
nums |> Seq.filter ((<) 10)
which looks backwards and is confusing. Therefore, you end up often just using a lambda to control the order of application without reversing the operator.
nums |> Seq.filter (fun x -> x > 10)
What you really want is Haskell's notion of operator sections, where you can place one of the operands inside the parentheses on either side of the operator to make it clear which argument you intend to apply first.
So for instance, to find all the numbers greater than 10 you do
nums |> Seq.filter (>10)
whereas to find all the numbers 10 is greater than you do
nums |> Seq.filter (10>)
I think this would fit very well with the existing syntax. Haskell has both notations and it doesn't cause any issues except with minus due to its duality as a unary and binary operator. As a side note, Haskell also allows sections to be used with functions called with the infix notation (that places the function name in backticks), which is sometimes more succinct than a lambda.
https://wiki.haskell.org/Section_of_an_infix_operator



## Response ##
** by fslang-admin on 7/17/2015 12:00:00 AM **

Many thanks for this suggestion. It is being marked as declined – for discussion see the comments.
Further comments, use cases, information welcome
Don Syme, F# Language and Core Library Evolution.


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/7067304)**


## Comments ##


#### Comment by Don Syme on 7/17/2015 8:29:00 AM ####
To me this doesn't sit well as an addition to F#. First, the resolution of "<" and ">" in the F# syntax is non-trivial because of their use as type applications. Next, the bar to change and extend the F# expression syntax is high indeed at this stage - the utility gained needs to be large, and the application domain broad.
So my inclination is to decline this.

