# Remove the need for an arbitrary self-identifier (e.g. x) when declaring a member [5666097] #

**Submitted by Jorge Fioranelli on 3/21/2014 12:00:00 AM**  
**8 votes on UserVoice prior to migration**  

Being able to use any word or letter as self-identifier makes the code inconsistent quite easily.
member x.MethodA() = ...
member this.MethodB() = ...
Proposed solution:
member MethodA() = ...
or using just "." before the name:
member .MethodA() = ...
To call any other member from inside the method, we can do it the same way, either just using the method name or adding "." before it, no need to use a self-identifier.



## Response ##
** by fslang-admin on 2/5/2016 12:00:00 AM **

Thanks for the suggestion, though declined per my comment below.
Best regards
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5666097)**


## Comments ##


#### Comment by Jon Harrop on 3/26/2014 9:46:00 AM ####
How do you then refer to self in the body of an instance method?


#### Comment by luketopia on 3/29/2014 5:21:00 PM ####
@Jon Harrop
It's already possible to define a self-identifier at type level:
type Foo() as this =
member __.Bar() = 5
member __.Baz() = this.Bar()


#### Comment by Jorge Fioranelli on 5/1/2014 11:52:00 PM ####
Jon, like in C#, you don't need to, just write the function name and if there is one defined in the scope of the object use that one. E.g.
member MethodA() = 1
member MethodB() = MethodB() + 1


#### Comment by Frank Joppe on 11/16/2014 9:46:00 AM ####
IMHO, it would make the code more readable if you'd introduce a standard (keyword), like 'this' instead of letting it free, and one can use 'x', the other can use 'y'. A standard may prevent questions when coding, or educating the language.


#### Comment by Don Syme on 2/5/2016 5:08:00 AM ####
We decided in F# 1.0 to make this identifier compulsory, for purposes of code regularity. Since this has served us well and nothing has really changed since we made that decision, I will decline this.
Frank - requiring one single identifier causes problems when you have nested object expressions . Also IMHO forcing "this" encourages a certain style of OO thinking rather than the more algebraic thinking used in functional languages.

