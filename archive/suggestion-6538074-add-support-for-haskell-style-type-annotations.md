# Add support for Haskell-style type annotations [6538074] #

**Submitted by amazingant on 10/8/2014 12:00:00 AM**  
**58 votes on UserVoice prior to migration**  

Although it's typically preferred to let the compiler handle types, it is often necessary to provide type annotation. Sometimes this is to help the compiler understand the types a function can take, often it is done to help other developers understand your code, and in my personal use, I frequently add type annotations to ensure the compiler will catch typos I make which change a function's return type.
Although not as verbose as other .NET languages, the F# type annotations do add verbosity to a function definition, look cluttered compared to Haskell's syntax (personal opinion), and do not match the type format provided by the compiler or interactive environment.
I propose adding syntax to allow defining a function's type with a syntax closer to Haskell's. Since the :: operator is already in use, my proposal is to create a new operator such as => for these purposes; a new keyword could suffice as well, or simply new use of the val keyword currently used in signature files.
My initial suggestion is as follows:
let f => int -> int -> int
let f x y = x * y
While the inclusion of variable names would reduce the terseness of the syntax and would provide little benefit to readability or comprehension, such a change would provide consistency with the format output by fsi.exe and seen in Visual Studio with IntelliSense. An more complex type signature with such a format:
let f => a:(int -> string -> int) -> x:string list -> y:int -> int list
let f a x y = List.map (a y) x
In these examples, neither of the code snippets would typically need type annotations, and the annotations here are much larger than the implementation itself. However, the former syntax (my preference) would greatly reduce the length of function declarations in more complex functions. The latter option, while I would prefer it over the current syntax, would introduce an additional location where variable names would have to be changed during refactoring.
It is my opinion that were such a syntax to be provided, use of both the new and current syntaxes together should provide a compiler warning to the effect of "Multiple type annotations provided for function {0}. Consider removing extra type annotations to simplify refactoring of your code."



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6538074)**


## Comments ##


#### Comment by Loic Denuziere on 10/14/2014 9:42:00 AM ####
If we implement this (which I think would be a good idea), we should definitely use the same syntax as .fsi files.
val f : int -> int -> int
let f x y = x * y


#### Comment by Sergey Yavnyi on 10/27/2014 4:47:00 AM ####
Nice idea.
Another (but somewhat clunky) alternative that you can already use is
let f : int -> int -> int = fun x y -> x * y


#### Comment by exercitus vir on 11/6/2014 4:41:00 AM ####
Sergey, thanks for pointing that out. Since this is already possible, it does not seem that this suggestion really adds much value.


#### Comment by amazingant on 1/7/2015 11:17:00 AM ####
@Sergey I agree that alternative looks a bit clunky, but it can be rearranged enough that I'm happy with it:
let f : int -> int -> int =
fun x y -> x * y
It feels a little odd not adding a full indentation level, but the second line only needs one extra space (or tab, if you're one of those) beyond the indentation for the signature line; with just one space it still feels like the fun line is still part of the function header, without requiring the body of the code to gain another indentation level.


#### Comment by exercitus vir on 6/19/2015 6:02:00 PM ####
This is related: /archive/suggestion-6237585-allow-inline-keyword-in-the-case-let-f-fun-a


#### Comment by Tobias Burger on 1/11/2016 7:55:00 AM ####
The more I code in Haskell/Elm/PureScript the more I like the way of how type are declared in this languages.
You can "emulate" this style by using an .fsi file alongside your .fs file, but the declaration and the implementation is physically separated and for scripts there is no way to declare this kind of type annotations.
I'm with Loic: the declaration should be the same as for .fsi files.
I find it easier to read/understand (and implement) the function by looking at the second declaration.
let map (mapper: 'a -> 'b) (m: M<'a>) : M<'b> = ...
val map : ('a -> 'b) -> M<'a> -> M<'b>
let map mapper m = ...


#### Comment by Anonymous on 1/16/2016 1:39:00 AM ####
Never worked with Haskell, but after I've tried Idris I've started to miss having type annotations over my functions, or at least some of them...
Declaration style should ofc be same as in fsi files...


#### Comment by Don Syme on 2/4/2016 2:06:00 PM ####
Why not just this syntax?
let f : int -> int -> int
let f x y = x * y
Also what would be the syntax for "member" declarations? This?
member M : int -> int
member this.M(x) = x + 4
Also what would be the syntax for "let rec" declarations in a mutually recursive group?


#### Comment by Anonymous on 2/10/2016 1:42:00 PM ####
What about:
f : int -> int -> int
let f x y = x * y
...and ...
M : int -> int
member this.M(x) = x + 4
same for let rec


#### Comment by exercitus vir on 7/11/2016 11:55:00 AM ####
This is possible using the following (already supported) syntax:
let add : int -> int -> int =
fun x y -> x * y
The only restriction is that you currently cannot add "inline" to the function value:
let add : int -> int -> int =
inline fun x y -> x + y
Lifting this restriction has been requested and approved by Don Syme here, so someone just needs to propose a tested PR: /archive/suggestion-6237585-allow-inline-keyword-in-the-case-let-f-fun-a

