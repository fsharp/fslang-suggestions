# Interfaces as simple, reusable and named sets of member constraints on statically resolved type parameters [8393964] #

**Submitted by exercitus vir on 6/12/2015 12:00:00 AM**  
**16 votes on UserVoice prior to migration**  

The suggestion is that any interface can be used as a named set of member constraints on statically resolved type parameters (just like generic type parameters) .
This suggestion achieves 4 desirable properties of member constraints on statically resolved type parameters with new kind of constraint that is non-invasive and simple to use:
1) simplified syntax improves writability
2) grouping constraints improve readability and makes declaration explicit
3) naming a set of constraints allow reuse of those constraints
4) ability to reuse existing interfaces as a named set of member constraints allows retroactively implementing interfaces on existing types (solves many reasons why people want type classes)
It's syntax and semantics are similar to the type constraint specified with `:>`. The suggested syntax for the new kind of constraint is `:^`.
It works with any (existing) interface. For example,
type IDuckish = //an interface for duck-like types
abstract member Quack: unit -> string
let inline quackLikeADuck (d : ^d when ^d :^ IDuckish) = //note the `:^` instead of `:>`
d.Quack(); //syntax for invokation also much simpler*
*The simpflied syntax for member invokations is inspired by this suggestion: /archive/suggestion-8014059-improve-constraints-and-make-call-syntax-easier-fo
This suggestion subsumes this suggestion: /archive/suggestion-6343928-allow-naming-of-member-constraints



## Response ##
** by fslang-admin on 2/4/2016 12:00:00 AM **

Per my comment, closing this as a duplicate of /archive/suggestion-6343928-allow-naming-of-member-constraints.
This isn’t an exact duplicate, I know, e.g. it also incorporates /archive/suggestion-8014059-improve-constraints-and-make-call-syntax-easier-fo, but they are close enough together that we don’t need to track them separately


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/8393964)**


## Comments ##


#### Comment by exercitus vir on 6/12/2015 10:12:00 PM ####
Note: This effectively allows simple to use structural subtyping as opposed to nominal subtyping currently provided by interfaces, so you could call this kind of constraint a "structural interface constraint".
This could also allow efficient extension interfaces* even on sealed types and value-types where if the function is expecting a statically resolved type parameter with a structural interface constraint, then it could just inline the functions of the extension interface.
*extensions interfaces suggested here: /archive/suggestion-5665042-allow-extension-interfaces


#### Comment by exercitus vir on 6/12/2015 10:29:00 PM ####
Regarding my last comment, the advantage of extension interfaces is that it makes the supported functions explicit even if the extension interface is only used as a structural interface constraint.
I suggest the following syntax for extension interfaces, which is consistent with extension members:
type TypePretendingToBeADuck with
interface IDuckish with
member this.quackLikeADuck() = "Quack"


#### Comment by exercitus vir on 6/13/2015 10:09:00 AM ####
One more advantage of this suggestion: All usage of member constraints defined by an interface could finally be renamed via the Refactor->Rename command in Visual Studio since they would identified by the interface they belong to. This is currently not possible since member constraints do not have a global name.


#### Comment by exercitus vir on 6/13/2015 10:20:00 AM ####
Here is a suggestion for an event shorter syntax if the interface is the only constraint on `d`(just like with generic type parameters):
let inline quackLikeADuck (d :^ IDuckish) = //again, just `:^` instead of `:>`
d.Quack() //exactly like invokation of dynamically resolved members as before


#### Comment by exercitus vir on 6/13/2015 11:58:00 AM ####
This idea could even be extended to static member constraints where instead of using an interface as a named set of member constraints, we could use a *module* signature as a named set of *static* member constraints. This is similar to how a type class is defined as a set of functions, but being static members in F# enforces a single instance of a type class for a type.
module Duckish = //module as structural interface for static members
val quack : unit -> string //just like a function signature in signature files
type TypePretendingToBeADuck =
module Duckish with //syntax just like interface implementation
let quack() = "quack" //will be translated to a static member of the same name
let inline quackLikeADuck (d : ^d when ^d :^ Duckish) = //module as named set of static member constraints
^d.quack() //syntax consistent with invokation of static member


#### Comment by exercitus vir on 6/13/2015 12:12:00 PM ####
Here is an example where a module signature as named set of static member constraints would be useful. Tomas Petricek shows you can implement custom numeric types like this: http://tomasp.net/blog/fsharp-custom-numeric.aspx/. The module signature would look like this:
module Numeric<'n> =
val FromZero : unit -> 'n
val FromOne : unit -> 'n
val FromInt32 : int -> 'n
val FromInt64 : int64 -> 'n
And can be used as a static member constraint in an inline function like this:
let inline zero (n : ^n when ^n :^ Numeric) =
^n.FromZero()


#### Comment by exercitus vir on 6/13/2015 12:19:00 PM ####
Please ignore this and my last two comments if you don't care about modules as named sets of *static* member constraints. The original suggestion was only about interfaces as named set of member constraints.
If using a module signature as a named set of static member constraints does interest you, I suggest to call this kind of constraint "module signature constraint".


#### Comment by Jared Hester on 6/22/2015 8:06:00 AM ####
I'm confused about the proposed implementation for this suggestion. It seems like Interfaces already do a lot of what you'd like them to :
-----------------------------------------------------------------------------------------------------
| type Gunslinger = abstract shoots : int -> int
| type Incinerator = abstract incinerate : int -> int
| type Elite = abstract harbinger : int -> int -> int
|
| let maelstrom (derringer:'a when 'a :> Gunslinger
| and 'a :> Incinerator
| and 'a :> Elite ) shot =
| shot |> (derringer.incinerate >> derringer.shoots >> derringer.harbinger 22)
-----------------------------------------------------------------------------------------------------
` :> ` is the upcast operator, is ` :^ ` supposed to be static type resolution operator or something like that?
I think this is a better way to get the properties you're looking for
/archive/suggestion-8509687-add-constraints-as-a-language-construct


#### Comment by exercitus vir on 6/22/2015 3:27:00 PM ####
Hello Jared, thanks for pointing out that my suggestion might not have
been clearly articulated.
Yes, ` :> ` is the upcast operator and also used to specify type constraints of (dynamically resolved) type parameters as in your example. I have not seen members being defined as function types, so thanks for making me learn something, but that does not solve the problem I am trying to solve.
`:>` can only be used for (nominal) interfaces as type constraints on dynamically resolved type parameters. I am asking for structural interfaces that can be used as type constraints on statically resolved type parameters. To make it explicit syntactically and reduce ambiguity for the compiler, we could use ":^" inspired by "^" for statically resolved type parameters and inspired by ` :> ` for dynamically resolved type constraints.
The goal of my suggestion is simply to ease the pain of declaring groups of explicit member constraints. They get really ugly really fast and they are not reusable. Being able to reuse existing interfaces to group several explicit member constraints into a structural interfaces is what my suggestion is about. I also haven't figured out how to indent several explicit member constraints without getting an indentation warning, but that is another problem.
Regarding the implementation, the compiler would basically just inject the explicit member constraints derived from the specified interface for you. If the argument actually explicitly implements a (nominal) interface, then it could replace the structural interface constraint with the nominal interface constraint, or not - it would work either way because implementations of nominal interfaces already have the required structure of asked for by structural interfaces.
I hope that makes it clear. If not, just let me know.


#### Comment by Jared Hester on 6/22/2015 10:47:00 PM ####
I think it would be confusing to change interfaces in the manner that you're suggesting
as it would break one of the rules of interfaces -
"Interface methods can be called only through the interface, not through any object of the type that implements the interface."
These "statically resolved interfaces" would also be fairly limited in their functionality. They couldn't support constructor constraints like ` 'T when 'T : (new : unit -> 'T) ` (interfaces can't define constructors); or static member and operator constraints (interfaces cannot define static members); and I can't see a way for them to support the - base type, null, value type, reference type, or unmanaged constraints either.
"statically resolved interfaces" also fall short for constraints on functions ::
---------------------------------------------------------------------------------------
let inline constraint_func (argA:^a) (argB:^b)
(**) (func: ^a-> ^b-> ^c when ^a:( static member (+) : ^a * ^b -> ^b )
(*.............................*) and ^b : ( static member (+) : ^b * ^a -> ^b )
(*.............................*) and ^c : ( static member (*) : ^c-> ^c -> ^c )
(*.............................*) and ^c : ( member toA: unit-> ^a )) : ^c =
(**) let arg1 = (^c:(member toA:unit-> ^a)(func argA argB))
(**) let arg2 = argA + argB
(**) func arg1 arg2
// ^ this is working ( albeit useless =P )code
---------------------------------------------------------------------------------------
When multiple types need constraints, using interfaces necessitates an interface per distinct type. However, following the syntax of my constraint suggestion, it could easily be defined as one cohesive unit
( /archive/suggestion-8509687-add-constraints-as-a-language-construct )
---------------------------------------------------------------------------------------
constraint ( ^a-> ^b -> ^c : abc_multplus ) =
(*.*) when ^a : ( static member (+) : ^a * ^b -> ^b )
(*.*) and ^b : ( static member (+) : ^b * ^a -> ^b )
(*.*) and ^c : ( static member (*) : ^c -> ^c -> ^c )
(*.*) and ^c : ( member toA : unit -> ^a ))
let inline higherFn ( funk : ^f when ^f : abc_multplus ) ( arg1 : ^g ) = ....
---------------------------------------------------------------------------------------
Adding a distinct language construct for constraints really seems like the best way to collect a
heterogeneous mix of constraints into a modular, composable, and extendable expression


#### Comment by exercitus vir on 7/14/2015 9:47:00 AM ####
Jared, thanks for your feedback. I agree that "statically resolved" or "structural" interfaces would be fairly limited. But they would still be very usefu for the simple problem they are solving. The fact is, declaring simple explicit member constraints is ugly. And the complex explicit member constraints are of course much more powerful than the simple structural interfaces. But in 90% of cases you don't need the other constraints like null, etc.
Static member constraints could be expressed as member signatures since this is what they basically are as I described in my comments below.
I disagree with the rule you quoted though. This rule applies to nominal interfaces, because this is the only kind available in .NET. Structural interfaces are a different kind of interface. I am just suggesting to be able to reuse the syntax and existing nominal interfaces. I don't think that it would cause any confusion as it's rather seamless and unobtrusive.


#### Comment by Don Syme on 2/4/2016 11:31:00 AM ####
Note that type aliases can be used to name groups of constraints, see https://gist.github.com/dsyme/bfed2eed788c7ba58ccc
Also, I will close this as a duplicate of /archive/suggestion-6343928-allow-naming-of-member-constraints. This isn't an exact duplicate, and also incorporates /archive/suggestion-8014059-improve-constraints-and-make-call-syntax-easier-fo, but they are close enough together that we don't need to track them separately

