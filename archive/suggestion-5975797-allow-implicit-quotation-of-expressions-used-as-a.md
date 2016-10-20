# Allow implicit quotation of expressions used as a method arguments [5975797] #

**Submitted by Tomas Petricek on 5/27/2014 12:00:00 AM**  
**27 votes on UserVoice prior to migration**  

In many data science scenarios, if a method can "see" what expression the caller passed as an argument. For example in R, you can write:
prices = c(10.0, 11.0, 9.0)
days = (1, 2, 3)
plot(days, prices)
This shows a chart where the X and Y axes are labelled as "days" and "prices", because the plot function can look at the expression passed as an argument. Similarly, we could automatically name newly added series to a data frame, etc.
One way to implement this would be to allow the `ReflectedDefinition` attribute on parameters and pass a hidden quotation as a next argument. For example, we could write the declaration as:
type Chart =
static member Plot([<ReflectedDefinition>] values:seq<float>, expr:Expr<seq<float>>) = (...)
And call it by writing:
let prices = [1.0; 2.0; 3.0]
Chart.Plot(prices)
The call would be translated to something like:
Chart.Plot(prices, <@@ prices @@>)
This also requires extending the quotations to actually capture names of local let-bound values (so that the quotation contains the name in some form).



## Response ##
** by fslang-admin on 7/18/2015 12:00:00 AM **

Completed in F# 4.0


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5975797)**


## Comments ##


#### Comment by Howard Mansell on 5/28/2014 7:16:00 AM ####
It should also be possible to do this with the param-array argument, so one can pass some arbitrary number of arguments. This would allow (for example) the construction of Deedle Frames with columns named according to the expression passed in.
Also, note that if I call something like plot(xs, ys ^ 2) this allows the axes of the plot to be labelled with the textual form of the expression, just as they do in R. So this is strictly more powerful that the Python kwargs feature.
In terms of implementation/syntax, I think having two separate formal parameters for each argument is strange. It would be better to pass some type that wraps up the whole thing.
BTW a string version of the expression covers all the use cases I think of, though some AST-based approach would presumably be generally more powerful.


#### Comment by Don Syme on 6/24/2014 10:37:00 AM ####
I am strongly sympathetic to this design proposal consider it basically "approved" though a prototype is needed.
As Tomas mentions one main problem is a limitation in F# quotations w.r.t. local values. When given this code:
let f() =
let prices = [1.0; 2.0]
Chart.Plot(prices, <@@ prices @@>)
then the quotation <@@ prices @@> becomes an Expr.Value quotation node containing the value [1.0;2.0] value but no trace of the name "prices". This means that the feature would require some kind of extension to F# quotations to properly propagate metadata
One such extension may be to have a new node Expr.NamedValue("prices", <value>, <type>) which is also successfully matched by the existing Quotations.Patterns.Value active pattern (to avoid breaking backwards compatibility). This would be the first time that extensions like this to the set of quotation nodes have been used, but I believe it is sound and compatible.
Libraries which used this feature would pick up a dependency on the corresponding FSharp.Core 4.x
Cheers
Don


#### Comment by Don Syme on 6/24/2014 11:10:00 AM ####
Here's an alternative design (in addition to the need for NamedLocalValue):
At the declaration site we just have one argument with the following very natural form:
type Chart =
static member Plot([<ReflectedDefinition>] values:Expr<X>) = (...)
With an implicit conversion from X --> Expr<X> at the callsite. In this second design, the quotation node generated would be of a new kind that would match both Expr.Value plus other expression tree nodes. Let's say this new kind of node is created by Expr.ReflectedValue(T, Expr).
So for
Chart.Plot(f x + f y)
the caller becomes:
Chart.Plot(Expr.ReflectedValue(f x + f y, <@ f x + f y @>))
and the quotation value Q received by Chart.Plot matches both:
match Q with
| Expr.Value(v, ty) --> // v = f x + f y
and
match Q with
| Expr.Call(...) // the addition call
The point is, the quotation node contains the value "v".
There are a lot of advantages to design (2) - there is no insertion of an additional implicit argument (which might confuse IDE tools I suppose), there are no new public types in the F# library design, and the rules for the implicit coercion can be made the same as other implicit conversions to delegates or Expression<T>.
The minimal overall library additions for option (2) would be:
/// Create a new quotation expression that matches the same set of active patterns as
/// 'expr' except it also matches the Expr.Value active pattern, returning value 'value'
/// and type typeof<T>
static method Expr.ReflectedValue : value: T * expr: Expr<T> --> Expr<T>
/// Create a new node that matches both the NamedLocalValue and Value active patterns
static method Expr.NamedLocalValue : T * Expr --> Expr
/// Match a NamedLocalValue node
active pattern (|NamedLocalValue|_|) : Expr<T> --> (string * T * Type) option


#### Comment by Don Syme on 10/30/2014 12:27:00 PM ####
I have submitted a design here:https://visualfsharp.codeplex.com/SourceControl/network/forks/dsyme/cleanup/contribution/7638
The refined design is similar to the one below. At the declaration site we have:
static member Plot([<ReflectedDefinition>] values:Expr<X>) = (...)
With an implicit conversion from X --> <@ X @> at the callsite. So for
Chart.Plot(f x + f y)
the caller becomes:
Chart.Plot(<@ f x + f y @>)
Additionally, the method can declare that it wants both the quotation AND the evaluation of the expression, by giving "true" as the "withValue" argument of the ReflectedDefinitionAttribute.
static member Plot([<ReflectedDefinition(true)>] values:Expr<X>) = (...)
Quotations that capture named local values can now look at the captured name by matching ValueWithName, so
let f x = <@ x @>
This means that
match (f 3) with
| ValueWithName(obj,ty,"x") -> true
| _ -> false
returns 'true'
The named local values embedded in the quotation are irrelevant for the purposes of quotation equality.


#### Comment by Don Syme on 1/16/2015 9:18:00 AM ####
A speclet for this feature has been added here: https://github.com/fsharp/FSharpLangDesign/blob/master/FSharp-4.0/AutoQuotation.md


#### Comment by Yemi Bedu on 5/29/2016 3:45:00 AM ####
Hello,
So I have the following and can not pass in a quotation as the parameter:
type NameOf =
static member NameOf([<ReflectedDefinition>] q:Quotations.Expr<'T>) =
match q with
| Quotations.Patterns.Call(a, b, c) -> sprintf "%s %A" b.Name c
| Quotations.Patterns.Let(a, b, c) -> a.Name
| Quotations.Patterns.ValueWithName(a, b, c) -> c
| expr -> expr.ToString()
// ----- later on -----
let v = 1 + 1
let w = "2"
let x = <@ 1 + 1@>
printfn "%s" (NameOf.NameOf (1 + 1) )
printfn "%s" (NameOf.NameOf v)
printfn "%s" (NameOf.NameOf w)
printfn "%s" (NameOf.NameOf x) // will not compile. it will accept %x but does not give ValueWithName
Error FS0193: Type constraint mismatch. The type
Quotations.Expr<int>
is not compatible with type
Quotations.Expr<Quotations.Expr<int>>
The type 'Quotations.Expr<int>' does not match the type 'int' (FS0193)
Can you extend this feature to include Quotations? Thank you. Good day.

