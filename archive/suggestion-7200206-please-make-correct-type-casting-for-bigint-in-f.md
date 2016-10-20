# Please make correct type casting for bigint in F# [7200206] #

**Submitted by Alexei Odeychuk on 3/12/2015 12:00:00 AM**  
**8 votes on UserVoice prior to migration**  

I have been using the forward pipe to convert values and came up against the problem where the following code would work
let IntToFloat = 10 |> float
let FloatToInt = 10.0 |> int
But the equivalent bigint code would not work:
let FloatToBigint = 10.0 |> bigint
The reason why FloatToBignint does not compile is because the F# compiler is looking for a function called bigint that has an input of type float!
So, as soon as I had the following function declared:
let bigint(x:float) = bigint(x)
the code:
let FloatToBigint = 10.0 |> bigint
works perfectly.
Please make correct type casting for bigint in F# in order to eliminate the need to declare a helper function.



## Response ##
** by fslang-admin on 9/7/2015 12:00:00 AM **

See Lincoln’s comment – this will work the way you want in F# 4.0
Don Syme
F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/7200206)**


## Comments ##


#### Comment by Lincoln Atkinson on 3/16/2015 12:37:00 PM ####
This will actually work the way you want in F# 4.0, due to the "constructors as first-class functions" feature.
`float` and `int` in your example are generic inline *functions* which are defined to facilitate casts. Here's an example of their implementation https://github.com/Microsoft/visualfsharp/blob/fsharp4/src/fsharp/FSharp.Core/prim-types.fs#L4356
`bigint`, on the other hand, is simply a *type alias* for `System.Numerics.BigInteger` https://github.com/Microsoft/visualfsharp/blob/fsharp4/src/fsharp/FSharp.Core/math/z.fs#L336
Before F# 4.0, you could construct an instance by calling the ctor like `bigint(10.0)`, but it was not supported to use the type name like a function, e.g. `10.0 |> bigint`. With F# 4.0 this is now supported, and your example code works fine.

