# Allow declaration of precedence for operators for writing internal DSLs [5699234] #

**Submitted by mikero on 3/29/2014 12:00:00 AM**  
**13 votes on UserVoice prior to migration**  

F# has great internals for DSLs, such as DU's and pattern-matching, but the operator definition rules are restrictive and baroque.
It would be great to be able to define operators with user-defined names, arity, fixity and precedence without restriction on what characters are in the operator for given operator class. Syntax modules with operator definitions (not behaviors) could be explicitly referenced.
This could be a step toward (and maybe as far as one need go) more general compile-time eval / macro support.
syntax module MyDSL
// Prology syntax here - but whatever
op ("==>", xfy, 200)
op ("not", fx, 1000)
...
open syntax MyDSL1, MyDSL2
...code here...
or could have a workflow-like syntax for including the operators in a specific scope:
MyDSL { .... }
I think I understand the bag of worms here, but it's worth it to me over having to move to another language for a project or write a parser (even if in FParsec, etc.) for an external file and then slowly interpret an AST or go through the effort of code-gen, which after all is what we have the compiler for.



## Response ##
** by fslang-admin on 2/5/2016 12:00:00 AM **

Thanks for the suggestion. Declined per my comment as part of house-keeping of old suggestions that have relatively few votes.
That said I understand the use cases here. and that internal DSLs are sometimes unsatisfactory in F#. But equally, having parsing be free of scoped declarations is a great simplification in the language, and means the “can of worms” is not opened too far :)
Best regards
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5699234)**


## Comments ##


#### Comment by mikero on 3/29/2014 11:45:00 AM ####
Missing in the op statements is the mapping from the syntax to the corresponding F# function
op ("==>", xfy, 200, Implies)
then the user would bind the syntax module to a class that implements Implies, Not, etc.


#### Comment by Peter Strøiman on 12/1/2014 7:49:00 AM ####
Just being able to control associativity would help me out greatly. I have a project where I needed my custom infix operator to be right associative. This forces me to choose the first character in the operator to be either * or ^.
Neither are particularly pretty.


#### Comment by Don Syme on 2/5/2016 6:53:00 AM ####
This is bag of worms territory :)
In F# 1.0 we decided against having notational declarations, and we've generally been sticking with this decision, e.g. see here /archive/suggestion-5663255-allow-infix-notation-on-functions and a few other suggestions. I'm going to decline this suggestion on the same basis.

