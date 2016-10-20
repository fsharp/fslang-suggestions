# Give 'A+B+...' as a type shorthand for Choice<A,B,...> [9526842] #

**Submitted by Ed A on 8/28/2015 12:00:00 AM**  
**1 votes on UserVoice prior to migration**  

We can't have anonymous discriminated unions but sometimes we don't want to bother making a new type for simple choices. At the moment, Fsharpers have a shorthand for Tuple<A,B>, Tuple<A,B,C...> so why not have a shorthand for choices as well? I agree that using discriminated unions to do this normally is very good practice because we can label each case to help us see the meaning of the type. But there are cases where we just want to quickly say "this can return an A or a B'. This happens a lot if you are writing functions that do a job inside another function. Writing a new union type for this one function is overkill so we use Choice<_>.
The only problem I can see is that forming and unpacking things of type Choice<A,B,C> is a bit tedious and involves using the Choice1of3 etc union types. As an extra (and this is might be a terrible idea) we could do terse pattern matching on A+B+C by writing something like
let f : (int+int+string) -> int =
function
//first case
|a -> a
|+|
//middle case
|0 -> 1
|b -> (2 + b)
|+|
//final case
|str -> (str.length)
Or some similar syntax where we identify which case we are working on by separating them in the same order. If our Choice type was bigger than 3, this would of course become somewhat unmaintainable and not very readable. But if we are only working with a small number of choices in a one-off function, this might help avoid unnecessary clutter.
There also might be a way of making a terse replacement for the 'Choice1of3' syntax. Perhaps in1, in2 in3 etc



## Response ##
** by fslang-admin on 9/7/2015 12:00:00 AM **

Thanks for the suggestion. While I appreciate the intent here, this is something we decided against in F# 1.0 in order to balance code readability v. special syntax. I don’t think anything specific has changed to warrant us revising that choice at this stage.
Many thanks
Don Syme
F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/9526842)**


## Comments ##

