# Support C#-like Anonymous Types in F# [5673015] #

**Submitted by Howard Mansell on 3/24/2014 12:00:00 AM**  
**215 votes on UserVoice prior to migration**  

Commonly I want to return some named values, or sequence of named values, in some expression. Currently I am forced to either go through the additional effort of defining a type, or use a tuple (with its associated error-proneness if there are multiple values of the same type). Anonymous record types would be very useful and would eliminate one of the areas of additional verbosity compared to C#.



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5673015)**


## Comments ##


#### Comment by Lev Gorodinski on 3/24/2014 8:26:00 AM ####
An alternative is to use a dynamic operator https://www.nuget.org/packages/FSharp.Dynamic/ which can be useful for constructing values at application boundaries. For calls within an application, I would stick to explicit types though.


#### Comment by Joel Mueller on 4/22/2014 11:51:00 AM ####
You can't use the dynamic operator in a quotation, however. There are some C# libraries (such as Neo4jClient) that expect LINQ expression trees that create anonymous types, and extract property names and data types from the expression tree. An F# equivalent is only possible if the dynamic operator is usable in a quotation, or if F# supports anonymous types.


#### Comment by Manuel on 6/3/2014 7:43:00 AM ####
Swift just introduced that also with named member tuples


#### Comment by Maciej J. Bańkowski on 6/5/2014 9:54:00 AM ####
@Joel Mueller, I have created a pull request for Neo4jClient that includes support for tuples: https://github.com/Readify/Neo4jClient/pull/56 It is not perfect but works as a workaround for the lack of anonymous types.
BTW I totally agree F# should support something like anonymous record types. I do not know why this comes up so late in the F# dev cycle but the requirement to create one-time-use types to work with data is hard for me to understand. As @Lev Gorodinski noted, dynamic has major drawback in that it relaxes strong typing which is a very important F# feature we should keep.
Does anyone know if there is any technical issue preventing implementation of anonymous types in F#?


#### Comment by Eamon Nerbonne on 6/21/2014 3:01:00 AM ####
Swift's solution isn't very good, however, so let's not copy that. in particular, swift's names don't really matter, it's still just a positional tuple, so when you do a destructuring let binding, you bind by position, not name. If you happen to swap the names (or mistype one, or refactor and change a member's name), then swift will still let you destructure by position, ignoring the names.


#### Comment by Eamon Nerbonne on 6/21/2014 3:22:00 AM ####
I think this would go particularly well with destructuring let bindings for records - (/archive/suggestion-6081483-allow-destructuring-let-bindings-for-records-or-t).


#### Comment by Anonymous on 6/21/2014 5:58:00 PM ####
For a bit of historical perspective, structural record types were part of Standard ML decades before C#.


#### Comment by Christopher Stevenson on 7/4/2014 2:43:00 AM ####
If the issue with this idea is syntax, here's a thought: "new with { property1 = value; property2 = value }". The "new with" indicates that this is an anonymous record.


#### Comment by Michael on 11/12/2014 5:21:00 PM ####
What's the benefit here? Creating anonymous types, just to turn around and use reflection on them seems sort of hacky. C# APIs like ASP.NET MVC use this because they don't have any slick way of doing [ "prop1", "val1"; "prop2", "val2" ].


#### Comment by Jari Pennanen on 6/24/2015 12:54:00 AM ####
Anonymous Records (which is a same thing as propsed here) are really neat, they are basically like TypeScript interfaces, allowing structural typing where it makes sens.
Scala (library) implementation: http://downloads.typesafe.com/website/presentations/ScalaDaysSF2015/T4_Vogt_Compossible.pdf
Above Scala implementation has some really great benefits, potentially shortening typesafe SQL syntax a lot.
Haskell (library) implementation https://gist.github.com/nikita-volkov/6977841 not very familiar with this one, but that is where I took the name.


#### Comment by Ben Lappin on 9/18/2015 11:13:00 AM ####
One benefit is that if you're only using a type in one place, somewhere deep inside a let binding, you currently need to define the type prior to the outermost let, which can be inconvenient. Take the following example:
type Thingy = { Inty: int; Stringy: string }
let ....
let ....
let aThingy = { Inty = 5; Stringy = "F# is fun" }
It would be preferable to be able to write something like:
let....
let....
let aLocalThingy = { Inty: int = 6; Stringy: string = "Future F# is funner" }
...and in either case, you could then do what you needed with the record, as long as the flow of code allowed its (anonymous) type to be inferred.
Essentially I would see this as "syntactic sugar" over defining a type that will only be used in one place.


#### Comment by Don Syme on 2/5/2016 5:11:00 AM ####
See also this suggestion which is somewhat related /archive/suggestion-8107647-extend-with-keyword-support-to-record-definition


#### Comment by Don Syme on 2/5/2016 5:21:00 AM ####
See also this suggestion on StructTuple compatible with C# tuples: /archive/suggestion-6148669-add-support-for-structtuple


#### Comment by Yemi Bedu on 6/1/2016 5:08:00 PM ####
What is the expectation for these types to shadow each other?
Would you want the compiler to warn about a named record that matches your anonymous one in certain use cases?
Examples would be anonymous record of { Length:int ; Width:int } that could be in a lot of places.
Another example is if you describe a Point { X:int ; Y:int } and later the anonymous version gets used in a function.
Should it infer Point or just warn "a named record of type Point matches"?
Would we want the allow declaration signatures to be anonymous
let Girl = {Name: string ; Age: int }
let Boy = {Name: string; Age: int }
let greet (child: {Name;Age}) = printfn "%A" child.Name
greet {Name="you";Age=21}


#### Comment by Bruno Bozza on 8/15/2016 8:39:00 PM ####
This is badly needed for data wrangling over typed datasets. I tried to use F#, which I prefer for everything else, but when every 5 lines of query code induce a new record type, updating the records becomes tedious very quickly, so I am back to C# for this.
C#'s support is not perfect (or new), but it has really convenient record punning. And for the drastic cuts they had to make in the design (i.e.: anonymous types being non-denotable and limited to method scope), my favorite feature of this design is that it allowed the team to ship it, and now I can use it. Yes, I expect more from F#, but I would be happy to give up on structural subtyping, first class labels and even denotability, in order to get C#-style functionality.


#### Comment by Tomas Lycken on 9/5/2016 9:05:00 AM ####
I'd love this! See http://stackoverflow.com/q/39306148/38055 for a use case.

