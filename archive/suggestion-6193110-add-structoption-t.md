# Add StructOption<T> [6193110] #

**Submitted by Demetrios Obenour on 7/19/2014 12:00:00 AM**  
**59 votes on UserVoice prior to migration**  

Currently, whenever a new Option is created, a heap allocation is required. This comes at a performance penalty.
I suggest that a new type StructOption<T> be made available for performance.



## Response ##
** by fslang-admin on 2/4/2016 12:00:00 AM **

Approved in principle, per my comment below.
Link to RFC to follow
Don Syme, F# Language and Core Library Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6193110)**


## Comments ##


#### Comment by Arbil on 7/20/2014 2:53:00 AM ####
This is much needed. For maximum performance, is there a reason why options on reference types cannot be just syntactic sugar on `null`? By that I mean that for both `T` and `T option` the underlying type is just `T`, and matching on option is compiled to `if opt = null then..;else..`.


#### Comment by Demetrios Obenour on 7/20/2014 12:14:00 PM ####
I agree with Arbil. This would have the further advantage that Option<T> could be restricted (as a .NET type in the CIL) to where T is a struct -- so Option<T> would not box the struct.
If this is not possible, use two types: one where T is a reference type, and one where T is a value type -- it is not acceptable for Option<T> where T is a struct to box the struct.


#### Comment by Fraser Waters on 7/21/2014 6:03:00 AM ####
"Also, it would be nice if there was a way to create an Option<T> type (where T is a struct) without boxing the struct." This is already the case. Option is a proper generic type, when T is a value type the jit will create new instances of Option so that the value stored does not need to be boxed (Same way List<T> doesn't box value types).
"For maximum performance, is there a reason why options on reference types cannot be just syntactic sugar on `null`?" I figure generics throw a spanner in the works here, if you have a generic method that takes a generic option that has to be done with the proper option class to support being able to pass both structs and classes in (structs couldn't be passed in as null, and nullable<T> is a totally different type).
It's probably possible to have an optimization pass that erases instances of Option<class> to just class and replaces matches/instance methods (e.g. opt.IsNone becomes (opt == null)). There's probably some corner cases where you can't erase every instance, and of course if changes your public API which you may or may not be wanted, but it sounds possible.
You could probably do a similar pass with Option<struct> to Nullable<T>. Nullable is a value type so it could help with performance and GC pressure, but that probably has even more corner cases.


#### Comment by Alfonso Garcia-Caro on 9/7/2014 10:41:00 AM ####
Having a compiler flag to desugar options on reference types as null would increase performance when writing F# to be compiled into other languages like JavaScript.


#### Comment by Loic Denuziere on 9/21/2014 5:01:00 AM ####
This is not purely an optimization though, it changes the semantics of the language. Currently, None and Some null are different, whereas with this proposal they would be equal.


#### Comment by Vasily Kirichenko on 10/5/2014 9:07:00 AM ####
None is represented as null in compiled code due to [<CompilationRepresentation(CompilationRepresentationFlags.UseNullAsTrueValue)>] applied on Option<'T>. So, only Some<'T> values are heap allocated.


#### Comment by Will Smith on 5/14/2015 7:12:00 PM ####
This is tricky. If Option<'T> can be made into a struct, then discriminated unions should be made into structs.


#### Comment by Don Syme on 2/4/2016 12:50:00 PM ####
I will mark this as approved in principle and we will open an RFC for it. We should add a StructOption<T> type to FSharp.Core.
More details are needed, but the intent is to augment FSharp.Core with a StructOption<'T> type that can be used as a substitute for the current option type in pattern matching etc. That will require ironing out many details.
The library functions using Option (e.g. choose) would not initially be redefined, that could be discussed in the RFC
The type would be opt-in, e.g. by opening a namespace or using a specific type name or StructSome/StructNone etc. Details will be discussed in the RFC

