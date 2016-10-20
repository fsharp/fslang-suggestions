# Pure Functions - "pure" keyword [5670335] #

**Submitted by Will Smith on 3/23/2014 12:00:00 AM**  
**116 votes on UserVoice prior to migration**  

I've been thinking about this one for a while.
At the moment, it's pretty easy to make a pure function and as a long as you follow a few rules, you should be fine. There is just no guarantee. A way for the F# compiler to enforce a function to be "pure" and not allow any side effects/mutations ever would ensure that guarantee. A "pure" function will have more constraints. This may also allow for more aggressive optimizations.
A challenge with this is how do we handle existing functions that are referentially transparent and types that we know are immutable. My best shot at this is only allow the F# compiler to make exceptions to functions/types to be allowed in "pure" functions. An example would be the "string" type and its functions.



## Response ##
** by fslang-admin on 2/3/2016 12:00:00 AM **

Declining per my comment of July 18, 2015 12:16
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5670335)**


## Comments ##


#### Comment by Richard Gibson on 3/25/2014 6:19:00 AM ####
I like this idea. You could say that a pure function does not close over any variables in outer scope, and can only call methods & access properties that are themselves marked as pure. E.g.
let x = 5
let printx() = printfn "%i" x // This function is NOT pure
let pure add x y = x + y // This function is pure because it only acts on variables explicitly passed in, and because the "+" operator is pure.
type Customer = { Id: Guid; mutable Name: string }
let pure formatId c = sprintf "The id is %A" c.Id // Immutable properties can be accessed in pure methods
let formatName c = sprintf "The name is %s" c.Name // Mutable properties make the method non-pure
This seems more "correct" somehow, but I'm not 100% sure what pure methods would actually give you...


#### Comment by Will Smith on 3/26/2014 10:26:00 AM ####
Richard,
Pure functions give you an absolute guarantee that a function does not have any side effects. Can be very useful if you need to run computations in parallel. We can still do this, but there is no guarantee.
I'm not sure how I feel with using immutable properties, I think I would only want to use immutable records/structs with no fields marked as mutable. But, maybe it does make sense to use only immutable properties. I think it's definitely worth exploring this idea. :D


#### Comment by Jack Pappas on 3/29/2014 10:54:00 AM ####
If this were implemented, why not use the existing [<Pure>] attribute instead of adding a keyword? http://msdn.microsoft.com/en-us/library/system.diagnostics.contracts.pureattribute%28v=vs.110%29.aspx
If the keyword is implemented instead, the compiler should decorate the method with [<Pure>] in the compiled assembly for interoperability with Code Contracts.


#### Comment by Will Smith on 3/31/2014 1:43:00 PM ####
Not fully against using the [<Pure>] attribute; however, when writing pure functions, I would hate to have to type out "[<Pure>]" over every method on top of "let".
Imagine this everytime:
[<Pure>]
let addOne x = x + 1
[<Pure>]
let addTwo x = x + 2
vs.
let pure addOne x = x + 1
let pure addTwo x = x + 2
Using the keyword makes creating the pure functions a natural part of the language. Using the attribute just feels like a fix to get the desired behavior.
Now, it's ok to decorate the compiled pure function with the [<Pure>] attribute.


#### Comment by knocte on 4/13/2014 12:05:00 PM ####
IMHO, in the same way we have a 'mutable' keyword, we shouldn't have a 'pure' keyword, but an 'impure' one! Always default to the best outcome...
This way, all functions should be assumed pure, and when one is not, the compiler should generate a warning if it doesn't contain the "impure" keyword.


#### Comment by Will Smith on 4/13/2014 12:12:00 PM ####
This means that all existing code would not compile and/or have warnings all over of the place. :(
Maybe, "pure" can be on functions like this:
let pure f x = x + 1
--
but we could also have it on modules:
module pure internal BestModule
--
That way, anything inside the module would only allow pure functions. Though, it gets more complicated as modules can contain classes, records, structs, etc.


#### Comment by knocte on 4/13/2014 12:19:00 PM ####
> This means that all existing code would not compile and/or have warnings all over of the place
You would only pay this price if you upgrade to F# v.Next


#### Comment by Will Smith on 4/13/2014 12:36:00 PM ####
Maybe a better way to handle this would be to have a compiler directive:
#pure
This will make the file you are in only able to use pure functions and immutable types. This would get rid of having to have "pure" being used with functions or modules as well as using the [<Pure>] attribute. Should be a fair compromise. Thinking about it, I think a compiler directive is the cleanest way.


#### Comment by Suminda Sirinath Salpitikorala Dharmasena on 5/8/2014 11:01:00 PM ####
May be an attribute would do


#### Comment by Anonymous on 6/9/2014 8:57:00 AM ####
Microsoft Research's Koka programming language infers this quality as part of the type. They take it further with Total functions (pure functions that do not diverge or throw). It seems like a logical next step to have the 'effectfulness' be a part of the type, and for it to naturally be inferred, although as the paper on it mentions this adds some complexity when composing.
If you can infer 'purity' or 'totalness' 'pure' or 'impure' could be an optional keyword on the type.


#### Comment by amazingant on 6/25/2014 2:58:00 PM ####
I'd definitely prefer the compiler directive as Will put it. Coming from VB development, it's nice to be able to turn off Option Strict for the few files in a project that haven't been cleaned up yet.
Following that train of thought, for libraries and so forth, perhaps being able to set this value for the project as a whole? This would mean taking the opposite approach to the OP and more towards what I have to do with VB's Option Strict, namely telling the compiler "please consider this entire project to be made of pure functions...except this file"


#### Comment by Alfonso Garcia-Caro on 9/7/2014 10:27:00 AM ####
I like the idea, but I also think it would be more useful to mark whole modules or libraries as pure rather than single functions.


#### Comment by Ovidiu Deac on 10/25/2014 7:35:00 PM ####
As knocte suggested I think it's better to have impure, in the same way we have mutable. Then you should be able to disable the warning for backwards compatibility.


#### Comment by Jannick B on 1/25/2015 2:05:00 AM ####
I'd rather have an impure keyword added to anything that and let pure be the default


#### Comment by amazingant on 2/26/2015 8:03:00 AM ####
While I agree it would have been nice when F# was originally being developed, Microsoft doesn't really do breaking changes like that. Even as just a compiler warning, if it's an opt-out I'll end up telling management that "Microsoft changed this behavior in the last release, so I need to rewrite some code." Nobody will care that it improves the code quality or that it can be turned off, they'll just care that Microsoft "broke" something.
If this is added as a "pure" keyword, or some other opt-in, I can tell management that "I'm turning on this new feature so that I write better code; it will probably tell me some old code isn't as good as it could be." While it means it's something they can tell me not to do because time constraints, I could still start sprinkling the pure keyword into code as things get added or rewritten.


#### Comment by Don Syme on 7/18/2015 6:16:00 AM ####
The ramifications on a type system to track effects and/or purity are substantial, and considerably more is needed than declaring and checking named functions as pure. For example:
- The integration with higher-order features is very difficult. "List.map pureFunction" is also pure, but the type system won't know this. "Seq.map pureFunction" is pure if the input enumerable is pure when enumeration is performed, but the type system won't know this
- Other effects besides purity (the "zero effect" quickly become of interest, including termination, exceptions, read/write effects, IO effects etc.
- The space of possible inferred types for code becomes large (with no "best type" guaranteed) and the inferred types themselves are large and subtle
There are human-factor considerations to take into account as well - "can a beginner understand the type of List.map" and "when and where do we show effect annotations in error messages?" and "can a team mixing beginners and advanced experts make good use of this feature?"
For F# the stable approach is has so far been to push this off to FSharpLint-style tooling. The F# compiler service exposure of typed expression trees is relevant here.


#### Comment by Schalk Dormehl on 10/16/2015 8:59:00 AM ####
The true value of the fuctional revolution has been to seperate commands and queries from one another. The problem is that the idea has been extrapolated beyond it's real usefulness, IE things like Haskell, where there are no commands, only functions but now commands need to be simulated.
Ironically good command / query seperation has existing in SQL for a long, long time. T-SQL functions do not have side effects, you can't even call Random or Print.
The introduction of a Command keyword and a "pure" keyword would be epic. I think that the best method for implementing the pure keyword is to have it as an extension to the language initially. It would simply not be allowed to do any re-assignements to mutables and it will not be allowed to call a command. It may be necessary to go one step further than that and not allow it to refer to any mutable variables either to ensure memiozation.
PS Typescrypt has added the let keyword. I think the chances are best to introduce a pure fuction syntax into that.


#### Comment by knocte on 1/6/2016 9:04:00 PM ####
I've realized that there could be a simpler way to achieve this: in the same way C# requires you to use an -unsafe flag to call the compiler when you use the unsafe keyword in your project, F# could require a -mutable flag when you use the mutable keyword in any shared member (mutable keywords for variables inside a method, for example, would be allowed, as they are not shared).
This is maybe not a full solution w.r.t. purity/impurity handling (because you could still have impurity via IO without mutable members), but it would be a first step towards it.


#### Comment by Don Syme on 2/3/2016 12:59:00 PM ####
The proposal doesn't mention what happens in higher order cases. For example, can you constrain an input function to be pure?
Also it's not actually clear what additional optimizations we would actually implement (rather than think about implementing) if "pure" were added.....

