# Generic `TypeWithMeasure` and `TypeWithoutMeasure` functions for adding units of measure on any type [8401578] #

**Submitted by exercitus vir on 6/13/2015 12:00:00 AM**  
**2 votes on UserVoice prior to migration**  

Currently, the Core.LanguagePrimitives module only provides the following functions to add units of measure to decimal, double (= float) and single (=float32), respectively:
DecimalWithMeasure : decimal -> decimal<'u>
Float32WithMeasure : float -> float<'u>
FloatWithMeasure : float32 -> float32<'u>
and the Core.Operators module overloaded functions for removing units of measure on decimal, double (= float) and single (=float32):
decimal : ^T -> decimal
float : ^T -> float
float32 : ^T -> float32
Even though all the other primitive numeric types are also annotated with [<MeasureAnnotatedAbbreviation>], you cannot use them to carry a unit of measure, because the needed conversion functions are missing. And since `MeasureAnnotatedAbbreviation` is a public attribute, we would should be able to add units of measure on *any* type.
So, I propose to add the following generic functions to the Core.LanguagePrimitives module as follows:
TypeWithMeasure<'T, 'U> : 'T -> 'U
TypeWithoutMeasure<'T, 'U>: 'U -> 'T
where 'U is 'T with the measure.
Currently, DecimalWithMeasure, Float32WithMeasure, FloatWithMeasure are all implemented using the same generic function:
let inline retype<'T,'U> (x:'T) : 'U = (# "" x : 'U #)
So `TypeWithMeasure` and `TypeWithoutMeasure` could simply reuse this function. I realize that retype might not be entirely safe, but implementors of custom types that can carry units of measure can then implement two type-safe functions:
//custom type
type SomeType = ...
//custom type that can carry measure
[<MeasureAnnotatedAbbreviation>]
type SomeType <[<Measure>] 'm> = SomeType
//module with conversion functions for custom type
module SomeType =
let inline SomeTypeWithMeasure (withoutMeasure : SomeType) : SomeType<'m> = TypeWithMeasure withoutMeasure
let inline SomeWithoutMeasure (withMeasure : SomeType<'m>) : SomeType = TypeWithMeasure withMeasure



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/8401578)**


## Comments ##


#### Comment by exercitus vir on 6/14/2015 11:31:00 AM ####
I just noticed that the following functions also exist, but I still think that we need a generic version:
Int16WithMeasure : int16 -> int16<'u>
Int32WithMeasure : int32 -> int32<'u>
Int64WithMeasure : int64 -> int64<'u>
SByteWithMeasure : sbyte -> sbyte<'u>


#### Comment by exercitus vir on 6/14/2015 12:08:00 PM ####
You could solve the safety issue by introducing a new attribute similar to `GeneralizableValueAttribute` for value restriction. For example, `TypeWithMeasure` and `TypeWithoutMeasure` should only be callable from functions with an Attribute that might be called `ValueReturnedWithMeasureAttribute` and `ValueReturnedWithoutMeasureAttribute` to prevent accidental usage of `TypeWithMeasure` and `TypeWithoutMeasure`.


#### Comment by exercitus vir on 6/18/2015 11:49:00 AM ####
I also noticed that removing units of measure using functions such as `float` or `double` compiles to (in release mode) for example `(Double) doubleValue` in CIL. Unless this cast is ignored by the CLR if the value is of the same type as the desired cast, this explicit cast should not appear in the CIL produced by F#.
I would be interested to know if currently `(Double) doubleValue` is optimized to simply `double` by the CLR to avoid unnecessary casts.


#### Comment by Don Syme on 7/18/2015 4:43:00 AM ####
Take a look at this gist.
https://gist.github.com/dsyme/b80086ce5c5a0dc1a9f7
Although there is a change of representation in the conversion for units <-> no units, the effect is still basically as you want it. (if you want to minimize the cost of the representation conversion you could use a struct type)

