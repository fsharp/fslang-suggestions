# Compiler-enforced defensive coding: Parentheses to surround the if or match expression within another expression (from Ada 2012) [12798519] #

**Submitted by Alexei Odeychuk on 3/4/2016 12:00:00 AM**  
**1 votes on UserVoice prior to migration**  

I suggest using the if or match expression immediately surrounded by parentheses (on both sides) so long as it is used as part of another expression:
let a = b + (if x then y else z) + c // parentheses required
let a = b + (match x with y -> y | _ -> z) + c // parentheses required
I think the F# compiler should emit a warning (not an error, so it is not a breaking change in the F# language) so long as the if or match expression is not immediately surrounded by parentheses within another expression.
Remark: It's an error preventing code from compiling in Ada 2012, but that language is used for writing hard real-time software that can cause severe loss if its code contains a bug, namely threatening human lives or damaging the surroundings physically, so the Ada compiler is oriented to prevent potential logical errors in code at any cost).
The if or match expression needs not be surrounded by parentheses so long as it is used alone (just as the current F# syntax allows):
let a = if x then y else z // parentheses are not required
I think it's a good idea of defensive coding. It can be implemented easily in the F# compiler and allows preventing potential logical errors in F# code and improving code readability.



## Response ##
** by fslang-admin on 3/4/2016 12:00:00 AM **

Per comment, please add this to FSharpLint.
Don Syme
F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/12798519)**


## Comments ##


#### Comment by Don Syme on 3/4/2016 6:53:00 AM ####
Like most other style checks like this, we'd prefer this goes into FSharpLint

