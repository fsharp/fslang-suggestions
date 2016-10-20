# Structural, extensible records like Elm (concrete proposal) [9633858] #

**Submitted by trek42 on 9/5/2015 12:00:00 AM**  
**6 votes on UserVoice prior to migration**  

(this is similar to /archive/suggestion-8592088-make-records-extensible-a-la-elm, but more concrete).
== Motivations ==
F#'s record type is good at representing a group of fields, but is also limited and inflexible:
* Not Extensible -- it's hard to extend an existing record type with new fields. To extend type A without elaborating all its fields, the only choice is to create a nested structure that holds A as one field. However, many times a flat structure is more desirable (e.g. it is a better way to model the data, simpler, more readable, etc), and this is hard to do.
* Inflexible -- F#'s record type is nominal and doesn't support inheritance, which makes sharing common logic that works on structurally similar records very difficult. (Using inline functions with SRTP could achieve this, but the ugly/heavy syntax and other constraints of SRTP often create more problems than benefits).
I believe what's missed is a structural typing for record (a la Elm), and it's possible to add this to F# with great benefits.
== Proposal: Flexible Record Type ==
The core idea is to use '#' (currently for flexible type) to decorate records, so as to distinguish these “flexible records” from nominal record types.
Examples:
==== Defining Ad-hoc Flexible Records ====
// for normal records. the type must be predefined.
type A = { x: int; y: int }
let a = { x = 10; y = 10 }
// the type of ‘b’ is #{x: int; y: int}.
// the type doesn’t need to be predefined.
let b = #{ x = 10; y = 10 }
// type annotation and mutable are also possible.
let c = #{ x: int = 10; y = 20 }
let d = #{ mutable x = 10; y = 10 }
// flexible records are extensible.
// e0 doesn’t change the type.
// e1, e2, e3 adds, removes, updates fields respectively.
let e0 = #{ b with y = 100 }
let e1 = #{ b with z = 100 }
let e2 = #{ b - y }
let e2 = #{ b with y = “new field type” }
// We can definitely combine two flexible records
// as long as their fields are disjoint.
// below ‘Z’ is #{ x = 10; y = 10 }
// ‘U’ is #{x = 10; y = 10; u = 100 }
let X = #{ x = 10 }
let Y = #{ y = 10 }
let Z = #{ X; Y }
let U = #{ X; Y with u = 100 }
// Flexible records make defining default field values
// tremendously easier, because we can define default values
// per field, independently of the enclosing type.
//
// Below gives default value for ‘z’ but leaves ‘x’ and ‘y’ open.
// This is hard to simulate with current F# record, where the
// { default_instance with fields } syntax requires ‘default_instance’
// to be fully defined.
//
let DefaultZ = #{ z = 100 }
let xyz = #{ DefaultZ with x = 10; y = 20 }
==== Defining Flexible Record Types ====
// We can give names to flexible record types,
// and they are just type alias.
//
// B is a type alias of #{x: int; y: int}.
type B = #{x: int; y: int}
// Both nominal and flexible records can hold flexible
// record fields.
type Nominal = { b: B }
type Flexible = #{ b: B }
// Instance of ’Nominal’
let nominal = { #{ x = 10; y = 10 } }
// Instance of ‘Flexible’
let flexible = #{ #{ x = 10; y = 10 } }
==== Functions With Flexible Records ====
// Functions can take flexible record parameters.
let f (r: B) = …
let g (r: #{x: int; y: int}) = …
// We can call f and g with ‘a’, ‘b’, ‘e1’ defined above.
// Note that ‘a’ (of type A) and ‘e1’ have structurally
// compatible types, so they can be called directly
// without any conversion.
//
// For implementation, the compiler could add desugar code
// at call sites to make this work (e.g.., adding virtual dispatches
// to access fields of ’a’ and ‘e1’ through flexible type B).
let _ = f a, f b, f e1
let _ = g a, g b, g e1
// Flexible record type can be inferred and hold generic fields.
// The signature of ‘h1’ is #{ x: ’T; y: int } -> ’T * int
// The signature of ‘h2’ is #{ x: ’T } -> ’T
let h1 (r: #{_}) = r.x, (r.y + 1)
let h2 (r: #{x: _}) = r.x
// It’s also very useful to return flexible record type.
// This is usually more readable than returning a tuple.
// Below we can use result.x, etc.
let h3 … = … in #{ x = x; y = y; z = z }
let result = h3 …
(note: this implements this suggestion: /archive/suggestion-5673015-support-c-like-anonymous-types-in-f)
==== Extra Feature: Partially Apply Records to Functions ====
There are already suggestions for supporting named and optional parameters on let-binding functions (/archive/suggestion-5663215-optional-and-named-parameters-on-let-bindings-on-m).
A way to achieve this is to allow partially applying the fields of a record
(nominal or flexible) to a function based on parameter names. But we need a new syntax to distinguish this to normal function application. I think a reasonable choice is to use “##{}”, which means “flexible application”. I don’t really enjoy the particular operator, but I think it’s quite acceptable.
// syntax: “Function ##record”.
// g is (fun x -> x + 10 + 20).
let f x y z = x + y + z
let g = f ##{ y = 10; z = 20 }
// c = 130.
// d is (fun x y -> x + y + 30)
// e is 60.
let a = { x = 10; y = 20 }
let b = #{ z = 30; extra_field = “ignored” }
let c = f ##a 100
let d = f ##b
let e = f ##b ##a
// Below is a compiler error
// because the field isn’t compatible.
let _ = f ##{x = “string” }
== Notes on Implementation of Runtime ==
I think there are multiple ways to implement this, for example to make flexible record an interface
whose fields are virtual properties, and compiler automatically injects adapter objects to when calling a function with compatible but not identical records.
There might be clever ways to avoid the virtual dispatch for common cases, e.g., if there is no mutable field involved, we can make the flexible record type concrete, and do a field-wise copy at callsites when calling a function with compatible but not identical records.
== Summary ==
I think this opens lots of opportunities, and the fact that it can achieve the goal of some other suggestions (“C#-like anonymous type; named parameters for let-binding) suggests it may be an appropriate language construct and bring synergy and consistency to the language.
Related Suggestions:
* /archive/suggestion-8592088-make-records-extensible-a-la-elm
* /archive/suggestion-5673015-support-c-like-anonymous-types-in-f
* /archive/suggestion-5663215-optional-and-named-parameters-on-let-bindings-on-m
PS: IMHO, ideally structural record should be the default, and nominal record type should require annotation. However this doesn’t seem to be feasible now.



## Response ##
** by fslang-admin on 2/5/2016 12:00:00 AM **

Thanks for the suggestion, I think it’s a great feature
Unfortunately I have to decline it since I don’t think it’s possible to implement it within the constraints of the .NET nominal/generics type system, while maintaining cross-assembly type identity
The issue /archive/suggestion-5673015-support-c-like-anonymous-types-in-f is also highly relevant, as is /archive/suggestion-6148669-add-support-for-structtuple


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/9633858)**


## Comments ##


#### Comment by Don Syme on 9/7/2015 5:15:00 AM ####
Thanks for the well described proposal. For example I'd not seen the use of this kind of declaration:
let h1 (r: #{_}) = r.x, (r.y + 1)
to introduce the ability to use r.x and r.y without pre-naming x and y (and without allowing r.mistake in other situations) before.
There are a couple of things you need to consider. One is the interaction with generics: what is the type of
let f1 x = #{ a=x; b=x }
and is the return type compatible with
let f2 x y = #{ a=x; b=y }
Also, how is this compiled? How many generic type parameters does the underlying class/interface have?
The other huge issue is about type identity and how to compile such a feature in a cross-assembly compatible way. If an abstract class or interface type is used as the representation, which assembly is that class or interface defined in? Or, to put it another way, is #{x=4} from one assembly compatible with #{x=4} from another assembly? Of course we would like that they are, but how do you implement that?
This is central to the design space for structural types for F# - it's not that there are multiple ways to implement structural record types (efficiently) - the problem is that there are _no_ ways to implement them on top of .NET (or at least no ways that don't lead to some other kind of limitation).
For example, you could unify all the similar record types within an assembly (C# does this for its anonymous object representation types), but give the types different identities across different assemblies. This would mean #{ x = 10; y = 10 } from one assembly would not be type-compatible with #{ x = 10; y = 10 } from a different assembly.
Likewise you could choose to tie the identity of a type to a containing module or containing function, so #{ x = 10; y = 10 } in one module was not type-compatible with #{ x = 10; y = 10 } in another module unless they were explicitly type-annotated to refer to a common module.
But what you can't get for free from .NET is structural types that somehow compile to nominal types in the natural way _and_ with seamless compatibility between objects and types across assembly boundaries.


#### Comment by trek42 on 9/7/2015 9:43:00 AM ####
Hi Don — thanks for the thoughtful reply!
I think we want to make all “#{x=4}” objects instantiated
in different assemblies work together seamlessly, otherwise
it is quite unsatisfactory.
I guess one way that might work is to use erased types.
Here’s a layman’s proposal for discussion, please
bear with me if it falls apart completely :-). The idea is that
the field names are ordered lexicographically and then erased
completely in the compiled form, e.g., #{ y: ’U, x: ’T } becomes
FSharp.Core.ErasedRecord<’T, ‘U>, and List<#{x: int}> is just
List<ErasedRecord<int>>, and so on. So all such records
will be compatible with each other at IL level as long as the
shape is the same.
We keep F#-accessible metadata for the non-erased record types,
derived types and functions signatures in the assembly, in order to enforce
stronger type safety by F# compiler, which will check that not only the
shape but also field names must be compatible. I don’t know how
powerful the F#-only decorations can be; I wish this could be achieved
in a similar way that we define types with unit-of-measure, erased them
in compiled form, yet still have stronger type safety when consuming them
in F# code.
(With the F#-only decorations the compiler can automatically inject
conversion code between different but structurally compatible record types
e.g., when we call a function taking #{x: int} with an object of type #{x: int, y: int},
a new ErasedType<int> is automatically constructed).
For the first question about generics:
// Signature:
// f1: ’T -> # { a = ’T; b = ’T }
// f2: ’T -> ‘U -> # { a = ’T; b = ‘U }
//
// they are erased to return
// ErasedRecord<’T, ’T> and ErasedRecord<’T, ‘U> respectively.
let f1 x = #{ a = x; b = x }
let f2 x y = #{ a = x; b = y }
So naively I guess their signatures shouldn’t be compatible,
similar to that “let f1 x = x, x” and “let f2 x y = x, y” aren’t compatible.
I haven’t spotted a particularly big issue here, but I could well have
misunderstood the situation here. (let me know!).
===
PS: after I posted the original proposal, I’m leaning towards making structural record types
concrete instead of interface, for better performance and simplicity. This may mean that
mutable fields can’t be supported (I’m not sure), but I think it’s an acceptable situation
if other parts of the solution can be worked out nicely.


#### Comment by Nathan Schultz on 11/17/2015 9:00:00 PM ####
It might be worth noting that Elm is removing Extensible Record support as of version 0.16.
https://github.com/elm-lang/elm-compiler/issues/985


#### Comment by Don Syme on 2/5/2016 5:17:00 AM ####
trek42 - I think it is not possible to get both cross-assembly structural typing and subtype-compatible extensibility.
There is also a lot of overlap between this and /archive/suggestion-5673015-support-c-like-anonymous-types-in-f and /archive/suggestion-6148669-add-support-for-structtuple. From the notes below, this is beginning to look a lot like the StructTuple proposal in its compiled form. But I think you _really_ want to be able to add and remove fields and maintain structural compatibility. I don't think that's possible if compiling to tuple types.
Don't get me wrong - I think this is a great feature - I just think it would have to be completely erased to property bags to actually work in practice. But that would not satisfy typical performance needs.


#### Comment by Don Syme on 2/5/2016 5:18:00 AM ####
I'm going to decline this feature because I don't believe it's possible to implement it satisfactorily within the constraints of the .NET nominal/generics type system, without using complete erasure of the types (or interfaces, which also would bring cross-assembly type identity problems)


#### Comment by trek42 on 2/6/2016 2:05:00 AM ####
Don -- It's a great news that there will be StructTuple in F# !! really looking forward to the open rfc. I think it will be a great enhancement to F#.
====
Some further discussion:
Re: "But I think you _really_ want to be able to add and remove fields and maintain structural compatibility. I don't think that's possible if compiling to tuple types."
to clarify, what I was thinking about is after type-erasure, the tuple types won't be structurally compatible. In other words, mapping two erased tuples based on field order will be wrong. However, all type conversions are statically generated and injected by compiler at compile time, so the field order in erased tuples don't matter.
====
I've been thinking about this proposal since last time, just document them here (not indicating they are useful, but anyway :-) )
I think what I really want is "anonymous types with subtyping based on field identifiers". -- Other things are icing on the cake.
Namely (using tuple notation):
#0. Anonymous type -- don't have to typedef it. (tuple satisfies this).
#1. (A:int, B:string) is identical to (B:string, A:int) -- unlike vanilla tuples, field order never matters.
#2. Subtyping -- we can have a function that accepts (A:int, B:string), and any compatible superset (e.g., (A:int, B:string, C:int) ) can be applied without manual conversion (compiler generates conversions at call-sites).
(How to make #1 and #2 work on .NET and across assembly is the hardest part. I really hope there is someway to hack this...)
Beyond that, producing new types by adding/removing fields from existing, *concrete* type is mostly syntax sugar -- they are very useful but not as critical as subtyping (#2), which enables sharing code.
I'm eager to find out whether the StructTuple is completely agnostic to field order (I think order-based mapping is too confusing), and to what extend type conversion among different StructTuple can be introduced.

