# Add NameOf operator to follow C#/VB update [5900625] #

**Submitted by amazingant on 5/8/2014 12:00:00 AM**  
**126 votes on UserVoice prior to migration**  

The Roslyn compiler currently (as of 2014-05-08) has a new NameOf operator listed as "Planned" for both C# and VB:
(https://roslyn.codeplex.com/wikipage?title=Language%20Feature%20Status&referringTitle=Documentation)
Pending its arrival there, it would be awesome to get something similar in F# as well.



## Response ##
** by fslang-admin on 6/17/2016 12:00:00 AM **

RFC is here: https://github.com/fsharp/FSharpLangDesign/blob/master/RFCs/FS-1003-nameof-operator.md


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5900625)**


## Comments ##


#### Comment by Don Syme on 11/14/2014 12:35:00 PM ####
I agree this should be added to F#.
The exact design needs nailing down. A special library intrinsic "val nameof : 'T -> string" looks appropriate, where "T" can be either an expression, a first-class use of a method or a typeof<...> expression may be simplest. The check.fs and opt.fs in the F# compiler would then treat this construct as special, doing a compile-time evaluation.
https://gist.github.com/forki/7c8ef4c3126c953630fb shows the kind of place where this is used in C#.


#### Comment by Steffen Forkmann on 11/15/2014 6:24:00 AM ####
I have a prototype implementation. Will send a first pull request for discussion soon.


#### Comment by Steffen Forkmann on 11/15/2014 1:30:00 PM ####
Pull request is at https://visualfsharp.codeplex.com/SourceControl/network/forks/forki/fsharp/contribution/7698


#### Comment by exercitus vir on 6/19/2015 6:06:00 PM ####
This is adding the name at compile-time right?


#### Comment by zjv on 12/1/2015 3:35:00 AM ####
Would really like this feature. Currently I have some ugly code with a hardcoded string in F# which I would like to improve. A nameof would make the code much safer against refactorings.
[<ReflectedDefinition(true)>]
let foo (x) = ...
let fooType = foo.GetType().DeclaringType.GetMethod("foo")
let fooExpr = Expr.TryGetReflectedDefinition(fooType)


#### Comment by ADMIN
fsharporg-lang (F# Software Foundation Language Group, F# Software Foundation) on 2/3/2016 1:55:00 PM ####
PR at https://github.com/Microsoft/visualfsharp/pull/908


#### Comment by Yemi Bedu on 5/27/2016 10:59:00 AM ####
/archive/suggestion-5674940-implement-syntactic-macros
Allowing my suggested function extension or macros would allow this implementation to be trivial. I explain this again below:
-----
So what would be nice is to extend the resolution of function parameters so that they wrap their parameters to be quotation expressions if it is a macro definition. Otherwise it would pass in the direct object value as normal. We can introduce a new keyword to make the distinction.
The definition of it could look like:
// def is a let that will pass in arguments as a Quotations.Expr
def nameof (arg:Quotations.Expr) : string = match arg with | Quotations.Patterns.Let(v, e1,e2) -> v.Name | expr -> expr.ToString()
let y = 1
printfn "%s" (nameof y)
The boxing will just find the most local definition of parameter if it is a variable or wrap the expression directly as <@ expression @>
This could allow us to use a lot of existing code and framework already in F#

