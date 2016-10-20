# Make reflected definitions easy to access [10922358] #

**Submitted by zjv on 12/1/2015 12:00:00 AM**  
**3 votes on UserVoice prior to migration**  

Given a reflected function like this:
[<ReflectedDefinition(true)>]
let foo (x) = ...
I would like to be able to get the reflected definition like this:
foo.TryGetReflectedDefinition()
instead of ugly code like this (note how I had to write the method name as a string):
let fooType = foo.GetType().DeclaringType.GetMethod("foo")
let fooExpr = Expr.TryGetReflectedDefinition(fooType)



## Response ##
** by fslang-admin on 2/3/2016 12:00:00 AM **

See comment from Don Syme


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/10922358)**


## Comments ##


#### Comment by Don Syme on 2/3/2016 2:55:00 PM ####
Using a quotation <@ foo @> will make it easier to accurately get the method name.
I will decline this: the existing mechanism seems good enough considering this is relatively rare.

