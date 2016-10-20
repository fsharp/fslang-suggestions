# Add syntactic sugar for lambda expressions in F# - lambda expression C# style [5665087] #

**Submitted by Maciej on 3/21/2014 12:00:00 AM**  
**17 votes on UserVoice prior to migration**  

Add syntactic sugar for lambda expressions in F# so that one can write lambda expressions in a even shorter form like in C# (no fun keyword, => symbol).
I do understand the lambda in F# are written this way because of many reasons, on the other hand I believe C# style lambda expressions are nice and concise and see no reason no to add optional syntax to the language.
Instead of writing
List.map (fun x -> x > ...) list we could write
List.map (x => x > ...)



## Response ##
** by fslang-admin on 2/4/2016 12:00:00 AM **

Closed as a duplicate since it is sufficiently close to /archive/suggestion-5663774-remove-fun-keyword-from-lambda-expressions


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5665087)**


## Comments ##


#### Comment by Jack Pappas on 3/22/2014 9:30:00 AM ####
This seems like a significant change to the language/compiler that only gains you the ability to not type 'fun' when writing lambdas. Would you rather the compiler team spent time implementing this, or implementing some new functionality (e.g., Intellisense in FSI)?


#### Comment by Mauricio Scheffer on 3/24/2014 9:29:00 PM ####
Duplicate of /archive/suggestion-5665087-add-syntactic-sugar-for-lambda-expressions-in-f (it has more votes).
Personally, I agree with Jack. IMHO this doesn't really buy you anything important.


#### Comment by Bryan Edds on 3/27/2014 10:07:00 PM ####
Please don't do this. Everytime you introduce a duplicate syntax, companies end up with even more inconsistency in their code bases.
The more ways there are to 'do it', the more ways in which it will be done!


#### Comment by Don Syme on 2/4/2016 11:17:00 AM ####
Will close this as a duplicate since it is sufficiently close to /archive/suggestion-5663774-remove-fun-keyword-from-lambda-expressions

