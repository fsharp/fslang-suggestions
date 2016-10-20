# Improve cloning record syntax [12515598] #

**Submitted by Alexei Odeychuk on 2/29/2016 12:00:00 AM**  
**1 votes on UserVoice prior to migration**  

It would be great and comfortable to write: { Record with field1 = x and field2 = y and field3 = z } instead of {{{ Record with field1 = x } with field2 = y } with field3 = z }.
I suggest to make it possible the alternative syntax { ... with ... and ... and ... and so on } for cloning records with multiple fields updated at once, and mark the current syntax {{{{ ... with ... } with ... } with ...} with ... so on } as obsolete in the language specification, but permissible for backward compatibility with the existing codebase.
I think F# syntax rules shouldn't push developers to use curly brakets (those relics of C# in the language with the indentation-based and depth-colorized syntax) in their code excessively.
Syntax "with ... and ..." here is mirroring the existing syntax for class properties: "...with get() = ... and set x = ... .



## Response ##
** by fslang-admin on 2/29/2016 12:00:00 AM **

See reply above – use a semicolon


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/12515598)**


## Comments ##


#### Comment by Don Syme on 2/29/2016 12:55:00 PM ####
Use { Record with field1 = x; field2 = y }

