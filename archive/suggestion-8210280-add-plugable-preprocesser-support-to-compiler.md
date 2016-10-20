# Add plugable preprocesser support to compiler [8210280] #

**Submitted by Xavier Zwirtz on 6/2/2015 12:00:00 AM**  
**4 votes on UserVoice prior to migration**  

Add support for handing in a preprocessor dll to the compiler.
A preprocessor dll would be able to receive the AST at different stages of the compile process and modify it.
It would be specified with --pre assembly-name.dll
You would have a type Main that exposes different functions depending on the stage that you want to modify.
module Main =
// receives raw unprocessed text and returns a string to advance.
// would allow for extension of syntax and reader macros
let Reader code =
modify code
// receives an untype checked but syntactically valid AST.
// returns an AST
let ProcessAST ast =
modify ast
// recieves an a type checked AST.
// if your preprocesser does not need to process an untyped tree this simplifies development
let ProcessTypedAST ast =
modifyTyped ast
This would allow for a variety of compile time enhancements to be added to F# ala Lisp and D, with out locking the language down to a single implementation.
For instance, in Racket a file may be begun with #lang {nameOfLang} that directs the compiler to the language to use. Using the above
suggestion the same functionality could be added by the community, allowing for different languages to have transpilers written for them
and then transformed during the compile process.
It would also allow for more "simple" plugins to be made, like syntactic macros.



## Response ##
** by fslang-admin on 7/17/2015 12:00:00 AM **

Many thanks for this suggestion. It is being marked as declined – for discussion see the comments above.
Don Syme, F# Language and Core Library Evolution.


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/8210280)**


## Comments ##


#### Comment by Xavier Zwirtz on 6/2/2015 9:44:00 PM ####
This is a different suggestion to adding syntactic macros. This is more about making the compiler pluggable and customizable. Macros would still do better as a first class language feature, however they could be iterated on quickly by the community as a preprocesser extension and pulled back into the compiler when consensus is reached by the community.


#### Comment by Don Syme on 6/9/2015 12:55:00 PM ####
I believe the appropriate place for this suggestion would be FSharp.Compiler.Service. It is unlikely we would add full pluggable syntactic phase translations in the F# language specification itself.
Don Syme, F# Language and Core Library Evolution


#### Comment by exercitus vir on 6/13/2015 1:32:00 AM ####
@Xavier: Have you already posted this as a suggestion to FSharp.Compiler.Service?

