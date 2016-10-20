# Code succinctness: Relax syntax rules for the else branch of an if expression (from Ada 2012) [12805656] #

**Submitted by Anonymous on 3/4/2016 12:00:00 AM**  
**0 votes on UserVoice prior to migration**  

For the sake of code succinctness, I suggest relaxing syntax rules for the else branch of an if expression in two special cases:
1) When there is no else branch in an if expression and the type of the if expression is inferred to be bool, then the F# compiler should treat the absent else branch as equal to false, type bool (like in Ada 2012 for if expressions).
2) When there is no else branch in an if expression and the type of the if expression is inferred to be option, then the compiler should treat the absent else branch as equal to None, type option.
Now, when there is no else branch written in an if expression, the type of the absent else branch is inferred to be unit, and the F# compiler emits an error: FS0001: This expression was expected to have type unit but here has type... .
New syntax. Example # 1:
[<Measure>]
type GBP
let status = false
// money = None here
let money = if status then Some(100<GBP>)
Example # 2:
let cashAvailable = false
let accountCorrect = true
// status = false here due to cashAvailable = false
let status = if cashAvailable && accountCorrect then true
elif not accountCorrect then false
These changes in the F# language syntax will not affect existing codebase. The if constructs with no else branch are allowed in Java, C#, Ada 2012, C++, VB.NET, just to name a few. I think this syntax will help remove an unnecessary burden from F# users (who have to write "else false", "else None" in their if expressions) and improve succinctness of F# code.



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/12805656)**


## Comments ##


#### Comment by Dominick Joseph on 3/4/2016 12:39:00 PM ####
I don't think is a bad idea. I do feel it makes the language less safe. The reason it defaults to unit if the if branch returns unit is because the else branch can only return unit. For everything else you need to explicitly state the else branch. This causes you to think about what the else branch needs to return. Having it just return none or false can cause you to miss something.
for example:
type person = { ShirtColor : string }
let maybePerson = Some { ShirtColor = "blue" }
let shirtIsBlue (x:person option) = if x.IsSome then x.Value.ShirtColor = "blue"
This will return false if the person is None. Is that what we want? Do we want to return bool option and return none? Do we want to wrap it in a different success/error type? But with this we will just keep processing as if the shirt is not blue. Obviously we would never write this code but imagine more complex types and expressions that don't necessarily have idiomatic ways of dealing with them.
So do we want safeness or succinctness?


#### Comment by Charles on 3/6/2016 11:41:00 AM ####
I like the existing unit default for imperative code.
I don't see the value of defaulting to false for Boolean conditionals. Can't "if a then b else false" be rewritten as "a and b"?


#### Comment by Alexei Odeychuk on 3/7/2016 1:41:00 PM ####
I tried to delete the above-mentioned suggestion shared by me, but failed due to the availability of a comment posted by Dominick Joseph. (Now a comment by Charles was appeared. I would like to thank him for another useful comment). Dominick convinced me that my suggestion is not a good fit for the F# language design due to its potential to undermine code safeness. Now the author of the suggestion is indicated as Anonymous. Dear Admin, please check in the website logs that I (Alexei Odeychuk) posted this suggestion, and delete it along with comments by Dominick Joseph and Charles or mark it as DECLINED. Thank you very much in advance for your rapid response.

