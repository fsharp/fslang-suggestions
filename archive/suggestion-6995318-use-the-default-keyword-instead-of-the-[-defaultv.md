# Use the default keyword instead of the [<DefaultValue>] attribute [6995318] #

**Submitted by Alexei Odeychuk on 1/22/2015 12:00:00 AM**  
**1 votes on UserVoice prior to migration**  

Use the default keyword instead of the [<DefaultValue>] attribute
Programming is a human activity. I think F# code has to be more elegant and readable for human programmers.
So, instead of coding:
type MyType() =
let mutable myInt1 = 10
[<DefaultValue>] val mutable myInt2 : int
[<DefaultValue>] val mutable myString : string
member this.SetValsAndPrint( i: int, str: string) =
... member body ...
it would be better and more elegant to write:
type MyType() =
let mutable myInt1 = 10
val mutable default myInt2 : int
val mutable default myString : string
member this.SetValsAndPrint( i: int, str: string) =
... member body ...
Please declare the [<DefaultValue>] attribute as an obsolete (unrecommeded to use in new code) feature in the F# language specification, but remain it in the language for compatibility with the existing codebase.



## Response ##
** by fslang-admin on 7/17/2015 12:00:00 AM **

Many thanks for this suggestion. It is being marked as declined – for discussion see the comments above.
Further comments, use cases, information and discussion welcome
Don Syme, F# Language and Core Library Evolution.


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6995318)**


## Comments ##


#### Comment by Vasily Kirichenko on 2/8/2015 1:38:00 AM ####
Attributes like [<DefaultValue>], [<Sealed>], [<AbstractClass>] and [<VolatileField>] were deliberately not made keywords in order to keep language simple AND to embrace FP where all these stuff are not used at all.


#### Comment by ADMIN
fsharporg-lang (F# Software Foundation Language Group, F# Software Foundation) on 2/14/2015 11:40:00 AM ####
Vasily is right - default values for mutable fields are not really "normal" in F# and functional programming - it would be more normal in F# to initialize the values of the fields.

