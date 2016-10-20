# Code expressiveness: Add loops with test condition in the middle [13380336] #

**Submitted by Alexei Odeychuk on 4/11/2016 12:00:00 AM**  
**2 votes on UserVoice prior to migration**  

Sometimes programmers need to first make a calculation and exit the loop when a certain condition is met. However when the condition is not met there is something else to be done. Hence we need a loop where the test condition is in the middle. That loop was first suggested in 1972 by Ole-Johan Dahl, a Norwegian computer scientist who is deemed to be one of the fathers of object-oriented programming.
I suggest using the syntax for that loop that requires no new keywords:
do
(* indentation to indicate the first part of the loop body *) body-expression
while test-condition (* this line of code has to contain the test condition only for code readability *)
(* indentation to indicate the second part of the loop body *) body-expression
done
Remark: I think the syntax: “do … while test-condition do … done” containing the do twice would be verbose. We can visually separate the two parts of the loop body by enforcing that the line of code beginning with the while keyword contains the test condition only.
The do .. while .. done loop evaluates its test expression in the middle of the loop instead of the top or bottom. Therefore, the first part of the loop body is always evaluated at least once before the condition is tested. If the test condition is true, the second part of the loop body evaluates and the flow of control jumps back up to do. This process repeats until the given test condition becomes false. Indentation indicates which expressions are in the first or second part of the loop body; the line of code beginning with the while keyword contains the test condition only, so code is clear and easy-to-understand.
I like that F# is a functional-imperative programming language suitable for writing real-world applications. It would be nice if F# would be a language fully developed in terms of imperative programming features, a language containing loops with the test condition at the beginning, in the middle, and at the end. It would improve the F# popularity and facilitate the migration of imperative code from other mainstream languages.
P.S. This suggestion is an extension of my previous suggestion about introducing loops with the test condition at the end: /archive/suggestion-13306077-add-the-do-while-loops-to-the-language-from-ja



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/13380336)**


## Comments ##

