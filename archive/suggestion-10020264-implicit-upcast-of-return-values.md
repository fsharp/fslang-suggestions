# implicit upcast of return values [10020264] #

**Submitted by Anonymous on 10/1/2015 12:00:00 AM**  
**6 votes on UserVoice prior to migration**  

It gets to be very frustrating when working with many C# libraries from F# because F# lacks implicit upcasting of return values. In some cases, this is just annoying. But it is particularly intractable when dealing with libraries expecting Expressions, because upcasting changes how the expression is evaluated by the library. See this question, where in the comments, the author comes to the conclusion that he can't make it work with F#.
http://stackoverflow.com/questions/10647198/how-to-convert-expra-b-to-expressionfunca-obj
There does exist a work-around, but it is quite horrible.
http://www.fssnip.net/c7
Aside from this show-stopping issue, there are many other scenarios where libraries expect implicit upcasts and it becomes annoying to have to litter your code with explicit upcasts. Interfaces and System.Object are the usual suspects for upcasting.
Request implicit upcasting of return values.



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/10020264)**


## Comments ##

