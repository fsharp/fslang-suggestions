# Warn when literal attribute is used with lowercase name [6668206] #

**Submitted by Daniel Bradley on 11/5/2014 12:00:00 AM**  
**8 votes on UserVoice prior to migration**  

The identifier of a literal must begin with an uppercase letter (as defined in 7.1 of the spec). If you assign the literal attribute with an identifier with lowercase first letter, it will ignore the literal attribute without any warning. Could we emit a warning when the literal attribute is not in effect due to the identifier used?



## Response ##
** by fslang-admin on 6/23/2016 12:00:00 AM **

This is approved, for F# 4.x or later
Completed her:e https://github.com/Microsoft/visualfsharp/pull/666
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6668206)**


## Comments ##


#### Comment by Daniel Bradley on 11/5/2014 11:39:00 AM ####
Here's a link to a SO question where the behaviour is currently confusing: http://stackoverflow.com/questions/3890037/literal-attribute-not-working


#### Comment by Sergey Tihon on 11/8/2014 2:18:00 PM ####
I think that it is already supported in FSharpLint tool http://fsprojects.github.io/FSharpLint/
see `LiteralNamesMustBePascalCase` rule in http://fsprojects.github.io/FSharpLint/FSharpLint.NameConventions.html

