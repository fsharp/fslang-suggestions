# Allow single case unions to be compiled as structs [6147144] #

**Submitted by exercitus vir on 7/8/2014 12:00:00 AM**  
**37 votes on UserVoice prior to migration**  

Single case unions are often used to define domain types that just wrap another primitive type. See http://fsharpforfunandprofit.com/posts/designing-with-types-single-case-dus/ for examples.
It would be great if we could mark these single case unions "inline" for optimized code generation. An "inline" single case union would not be converted to a class with a single "Item" property like an ordinary single case union, but instead the wrapped "Item" of the single case union would be passed directly (as is).
This would be similar to units of measure that are checked by the F# compiler, but are no longer visible in the generated code.
This would avoid the overhead of instantiating a class with the sole purpose of wrapping another type.



## Response ##
** by fslang-admin on 8/2/2016 12:00:00 AM **

Completed
RFC here with links to implementation https://github.com/fsharp/FSharpLangDesign/blob/master/RFCs/FS-1014-struct-unions-single-case.md
Don Syme
F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6147144)**


## Comments ##


#### Comment by Expandable on 7/8/2014 8:52:00 AM ####
But that would break type safety when the code is used from outside F#. True, that's also the case with units of measure and the inline annotation is purely optional.
But what about generating a struct instead? That would also avoid the heap allocation, instances of the type would not consume any additional memory compared to raw instances of the wrapped type and the just in time compiler should be able to inline pretty much all function calls (of course, the Equals methods, etc. should be overridden and point to the equivalent methods of the wrapped type).


#### Comment by Fraser Waters on 7/11/2014 9:11:00 AM ####
Wrapping with a struct sounds sensible. It would be lighter weight than currently and keeps it type safe when used from C#/VB/etc.


#### Comment by exercitus vir on 7/11/2014 2:15:00 PM ####
I also like Expandable's idea of generating a struct instead of a reference type. But I think structs would also break type safety because they are automatically initialized and the default of the struct could be passed into a function that expects a non-default single case union.


#### Comment by Expandable on 7/20/2014 9:48:00 AM ####
@exercitus vir: These benchmarks do not take garbage collection into account, as far as I can see.


#### Comment by ADMIN
fsharporg-lang (F# Software Foundation Language Group, F# Software Foundation) on 9/16/2014 5:08:00 AM ####
Title updated to "Allow single case unions to be compiled as structs"


#### Comment by exercitus vir on 10/21/2014 7:30:00 AM ####
I don't think that the new title is appropriate. I was not asking for single case unions to be compiled as structs, but "inlined". For example:
type inline SingleCaseUnion = SingleCaseUnion of int
let f (SingleCaseUnion item) = ...
should not compile to "SingleCaseUnion.Item" when passing the single value of "SingleCaseUnion" to function "f", but instead inline the int value in place of the "SingleCaseUnion.Item" property, so that "f" would look like this:
let f (item : int) = ...


#### Comment by Will Smith on 9/7/2015 6:45:00 PM ####
Obviously, we like wrapping types, but we also do not like heap allocation. Making them structs I think is what we want.
If you are worried about performance, allowing single case unions to be structs is very sufficient and close enough to the performance as if the type was erased. It might be slower, but not by much, where as reference types might be on an order of magnitude slower if you are creating a lot of them. You also have access to inline functions, so you can avoid the copying of structs if you need to.


#### Comment by Gauthier Segay on 1/22/2016 3:32:00 AM ####
This feature (description, not the title) looks like newtype in haskell.
https://wiki.haskell.org/Newtype


#### Comment by exercitus vir on 7/7/2016 8:15:00 AM ####
While I was initially asking for something different (inline vs. struct), single case unions compiled to structs solve the same problem. While structs are more type-safe than inlined when used from other languages, it would not be completely safe either when used from other languages that can call the default non-overridable parameterless constructor of structs, which wrap reference types. But it's great that you prevent calling that constructor from within F#!
To be completely safe, the author of the single case union compiled to struct must remember to wrap value types only, because wrapping reference types that default to `null` would be dangerous. This feature would still make a great addition to F# vNext.


#### Comment by exercitus vir on 7/7/2016 8:17:00 AM ####
The related records compiled to structs feature suggestion has already been implemented and merged:
- uservoice: /archive/suggestion-6547517-record-types-can-be-marked-with-the-struct-attribu
- github: https://github.com/Microsoft/visualfsharp/pull/620

