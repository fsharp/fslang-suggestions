# Can we build a pre-processor so we don't have to use the word: let ? Makes the function name standout and saves typing similar to R ? [13308666] #

**Submitted by Musa on 4/4/2016 12:00:00 AM**  
**4 votes on UserVoice prior to migration**  

Makes the function name standout and saves typing similar to R, ofcourse if it can be done without breaking something else ?
f := 3 //or ... rather than
let f = 3



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/13308666)**


## Comments ##


#### Comment by trek42 on 4/9/2016 3:26:00 PM ####
Admittedly, after using f# for years now I feel 'let' is too noisy/repetitive and wish it's gone. The benefits I can see are:
* Make the language feel lighter-weight and the code more "direct to the point", without sacrificing readability. (subjectively, I would say it improves readability, especially so in subareas like math/science/finance).
* It's a huge win when using FSI, where virtually every line starts with a "let" which doesn't do much.
* Save 4 characters in each line, the saving is big if your coding style requires a maximum (either it's 80 or 100) line width.
Saying the above, personally I don't think it's possible to do this in F#. There probably isn't a backward-compatibility way to achieve this, and all other approaches (e.g., source code transformation) is effectively forking the language, which isn't a good thing to F# in the large.
The only way one could imagine is to start a new language with a lighter syntax (yes, even lighter than F#) and incorporate the lessons learned from F#. But a new general-purpose language is a huge endeavor, and it would better bring new ideas rather than just different syntax.
(saying that, in an imaginary world my favorite general-purpose language would change the following syntax aspects in F#:
* no let keyword. Use "=" for let-binding and "==" for equality. (I think it needs to differentiate name-binding from equality when there is no "let"). Also without "let" it will be problematic when defining a function and put its parameters in multiple lines, for example:
function_name param1
........................param2 = (* fund-body *)
would not work because the first line can also be interpreted as function application. So some special treatment is needed here, e.g., still use some keyword (e.g., "def") to mark the beginning of a function definition, or always use lambda syntax "f = \(param1, param2) -> .." for function definition.
* also replace "fun" keyword to something shorter. Probably "\".
* reverse a few default settings. For example, "CompilationRepresentation(ModuleSuffix)" should be the default, so that there isn't a need to mention it unless you really need to NOT have it.
* Have a general solution to convert between module functions and instance methods. Ideally every instance method "a.Func" could also be called like a free, curried function using "A.Func" (A is the typename), and every module function "M.func x y z" could be called as an instance function through "x.func" (or maybe z.func?), whenever it makes sense. The first is challenging in .NET/F# because .NET methods have method overloading, among other things. The second is challenging itself because it allows calling a module function without opening the module M, and it's like C++'s argument-dependent lookup, which is a big can of worm with tons of ambiguity issues.
* Make Record syntax terser. e.g., the 'with" keyword is kind of annoying in { a with x = ..}.
* Unify tuple and records. (get rid of the concept of "tuple", which is just record with special field names like _0, _1. Make record types by-default structural instead of nominal)
Arguably the last one isn't just a syntax feature. So I'll stop here :-) ).


#### Comment by Boris on 4/10/2016 1:43:00 PM ####
I think it will sacrifice readability very much.
It's just an ancient C(+ - # ) programmer's mental force overestimation.
Such a quirks make you constantly analyze complex textual patterns to understand what does
one code line exactly mean.
IMHO programming languages are much more about reading(and thinking) then about writing.


#### Comment by Gauthier Segay on 4/10/2016 8:43:00 PM ####
F# is functional first but has to support quite a bit of imperative style constructs which makes it very practical.
Without let, it would be difficult to understand the scope of definitions, difficult to catch if I mistyped a symbol name.
I think the list of ambiguity this would create is huge and I'm not in favor of this proposition.


#### Comment by Alexei Odeychuk on 4/11/2016 2:14:00 AM ####
I agree with Boris and Gauthier Segay.
It would be really difficult to understand the scope of definitions without let.
As Edsger W. Dijkstra said, programming is a human activity. It's really much more about reading and thinking then about writing code. Code maintenance takes 50% (pro-level mid-size apps) to 90% (large, long-lived apps containing several million lines of code intended to be in use for 5 to 20 years) of time professional programmers spent on software projects.
From code readability and maintenance perspective, I see no value added for dropping the let keyword. I think F# has an excellent syntax in this respect. The let keyword helps writing readable code.

