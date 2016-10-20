# Add support for StructTuple [6148669] #

**Submitted by Arbil on 7/8/2014 12:00:00 AM**  
**136 votes on UserVoice prior to migration**  

According to my tests short struct tuples perform up to 25x faster than default ones if the cost of garbage collecting is taken into account. The code below allocates an array of default tuples/struct tuples respectively and collects it. The results are:
1249 ms for default tuples
44 ms for struct tuples
I remember reading that the Microsoft team had considered implementing tuples as structs but didn't see their advantage in the internal tests. I suspect the tests failed to take the garbage collection into account. If this is done the difference is huge.
Currently, even such a basic operation for high-performance code as a Dictionary.TryGetValue allocates memory! (Unless it is JITed away; the System.Tuple constructor is in the IL code).
I feel this is a real impediment for F# as a language for scientific, financial or game development.
Code:
type Pair<'a, 'b> =
struct
val Item1 : 'a
val Item2 : 'b
new(item1, item2) = {
Item1 = item1
Item2 = item2
}
end
let run() =
let size = 10000000
GC.Collect()
let watch = Diagnostics.Stopwatch.StartNew()
let mutable arrTuple = Array.init size (fun i -> (i,i))
arrTuple <- [|(0,0)|]
GC.Collect()
watch.Stop()
printfn "Took %A ms" watch.Elapsed.TotalMilliseconds
watch.Restart()
let mutable arrStruct = Array.init size (fun i -> Pair(i,i))
arrStruct <- [|Pair(0,0)|]
GC.Collect()
watch.Stop()
printfn "Took %A ms" watch.Elapsed.TotalMilliseconds



## Response ##
** by fslang-admin on 8/2/2016 12:00:00 AM **

Completed, see https://github.com/fsharp/FSharpLangDesign/blob/master/RFCs/FS-1006-struct-tuples.md
Don Syme, F# Language and Core Library Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6148669)**


## Comments ##


#### Comment by Expandable on 7/9/2014 11:52:00 AM ####
Are you sure that you're not measuring the difference between writing objects of a value type into an array vs writing objects of a reference type into an array? The latter might have to perform type checks on every write.
But still, it also worries me that tuples are implemented as classes. But I guess that's because you'd have to pass the tuples by ref (in C# terminology) for optimal performance when passing tuples to functions and that is somewhat frowned upon in the C# world. For F#, of course, the compiler could generate the appropriate function signatures.


#### Comment by Braden Evans on 7/9/2014 12:43:00 PM ####
This has been my experience as well, it is hard to write idiomatic f# code when avoiding allocations (option is another big offender)
In a batch workload (like the f# compiler) this isn't such a big deal (I remember reading the BCL team's test was actually with the f# compiler) but it is an annoying show-stopper for realtime stuff.
I wonder if it is possible to make major breaking changes like this to major f# versions?


#### Comment by Arbil on 7/9/2014 1:52:00 PM ####
@Expandable The difference is not due to using an array. I repeated the test with
let mutable tup = (0,0)
for i = 1 to 10000000 do tup <- (i,i)
and analogous code for Pair. The results are 47 ms and 3.3 ms, and the ratio is 15x. Short struct tuples will remain much faster even if you don't pass them as ref. I recall Jon Harrop claiming the cut-off when class tuples become faster even if passed to a function is length of 7.
@Braden I've been intending to make an analogous proposal for option but first things first! As you say, the difference between struct and class implementations is not visible in most synthetic benchmarks and one-time workloads, which is I believe why it has been overlooked. And it is indeed a show stopper particularly when guaranteed low latency is required (financial applications and games).
I wouldn't call the change breaking, it wouldn't break any existing functionality. It would degrade performance only in a pathological situation when a tuple is passed around ad infinitum, and dramatically improve performance in the remaining 99.99% cases.


#### Comment by Expandable on 7/10/2014 2:15:00 AM ####
@Arbit: The problem is: It wouldn't break anything for F# code, but it would certainly break some F#/C# interop scenarios. From F#'s point of view, implementing tuples and option as classes or structs is just an internal optimization, but C# facing code might break, as structs vs classes have significantly different semantics in C# and there is no way the C# compiler can hide that. On the other hand, I'd say this breaking change is worth it, especially since you normally don't expose F#-specific data structures to C# as they're ugly to use from C# anyway. Now for tuples it might be a bit different, but I personally hate to use tuples in C# anyway.


#### Comment by trek42 on 7/10/2014 9:06:00 AM ####
I'd like to +1000 on this (and also making option types structs) if I could :-) That will make idiomatic F# a fantastic choice for games.
I wonder if this could be enabled with a compiler flag, which will be good enough for those of us who don't need/care C# interop. Compiler could also generate function wrappers that convert from System.Tuple to/from the struct tuples for public functions to facilitate C# interop.


#### Comment by Braden Evans on 7/10/2014 11:01:00 AM ####
I like the idea of a compiler flag if a breaking change is out of the question.
Should note the compiler actually has a struct implementation for tuple2 already: https://github.com/fsharp/fsharp/blob/master/src/fsharp/FSharp.Core/prim-types.fs#L520 (Haven't tried to compile with it yet though)


#### Comment by Arbil on 7/15/2014 6:33:00 AM ####
I see what you mean with breaking C# interop. I do however think that impeding the development of a language by considering what might become broken by changes within that same language is quite enough. Binding development of F# to C# would be bad -- especially considering C# is at a point where they are hesitant to fix bugs because there are application that depend on them! I believe many who moved to F# to C# highly appreciate that F# is actively developing.
But this is of course something for the head honchos of F# and not me to decide.


#### Comment by Arbil on 7/28/2014 3:53:00 AM ####
I compiled the source with the struct tuple flag (https://github.com/fsharp/fsharp/blob/master/src/fsharp/FSharp.Core/prim-types.fs#L520) but 2-tuples are still compiled as classes. I might have overlooked something though. Still, it seems this is an irrevelevant/dead code branch because in reality the tuples are compiled as System.Tuple, while this branch defines its own Tuple type whether the struct flag is set or not. It is not used.


#### Comment by Anonymous on 7/31/2014 5:11:00 AM ####
I think this is a difficult issue in many ways.
First of all there is the value of interoperability. It is difficult to say how important this is. Personally I'd like the F# compiler to do much more aggressive optimization and could even accept having to do more work to interop with other .Net languages, but I believe I'm in a very small minority and the interop is vital to the success of F#. Without the interop, I believe F# would be doomed to be a niche language, because it would make it harder for developers from other .Net languages to use F# in their projects. Compare with the success of C++, for example.
Then there is the fact that currently .Net does not seem to generate very efficient code when dealing with structs. This is reported in many places. The current JIT generates many redundant copies when you are initializing structs, passing them as arguments to or returning the as results from functions. My experience is that with the current JIT, structs are only a win in few specific scenarios, such as when you basically make sure that a struct is allocated once (on stack or as part of some other object), is processed via a reference and structs are not arbitrarily passed around. When you do pass structs around arbitrarily, as a rule of thumb, a stack allocated struct with two pointer sized elements seems to be roughly as efficient as the equivalent two element heap allocated object. A pointer sized struct will generally be a win, while a struct larger than two pointers is likely to be a lose.
Then there is the fact that the internals of the F# compiler do not seem to be particularly designed for making sophisticated optimizations. In order to really make an effective optimizing compiler, you need to transform the surface language to a suitable intermediate language (e.g. SSA / CPS) that makes it relatively easy to write effective analysis and transformation passes for that intermediate language and also allows the desired optimizations to be expressed in the first place. Currently there is no such intermediate language in the F# compiler. The current intermediate languages within the F# compiler will not allow you to express control flow optimizations such as contification, which could be effective for optimizing non-trivial sets of local tail recursive functions into efficient loops.


#### Comment by Arbil on 8/4/2014 5:01:00 AM ####
@Anonymous That's helpful. Prompted by you I looked at some of the IL generated by struct usage and it often is indeed bizarro code. However, I think you are wrong when you say that 3 pointer sized structs are usually slower than 3 pointer sized classes. I tested it with passing to a function once and the 3-structs came over two times faster. And this is a test unfavourable to structs. Tuples are primarily made to be returned from functions and immediately deconstructed.
Code:
let checkT tup =
let (fst,_,_) = tup
if fst = -1 then printf "bad"
let checkS (str:Triple<_,_,_>) = if str.Item1 = -1 then printf "bad"
let run() =
let size = 100000000
GC.Collect()
let watch = Diagnostics.Stopwatch.StartNew()
let mutable tup = (0,0,0)
for i = 1 to size do
tup <- (i,i,i)
checkT tup
GC.Collect()
watch.Stop()
printfn "Took %A ms" watch.Elapsed.TotalMilliseconds
watch.Restart()
let mutable trip = Triple(0,0,0)
for i = 1 to size do
trip <- Triple(i,i,i)
checkS trip
GC.Collect()
watch.Stop()
printfn "Took %A ms" watch.Elapsed.TotalMilliseconds


#### Comment by trek42 on 8/7/2014 4:20:00 PM ####
@Anonymous -- I agree with your comments on .net optimizer, but I think they missed the big point which is garbage collection issues. For real-time applications, especially the now popular mobile and game development (where F# should really shine IMO), people often need to avoid garbage collection pause at all cost --- often, it's totally fine to pay a small extra cost each time a struct passed around, while avoiding piling up garbage quickly and cause observable lags.
Also note that we are specifically discussing about *Tuple*, not the general "struct vs class" tradeoff. Tuples are usually short-lived, local variables (mostly for multiple return values), and avoiding GC could lead to a larger win.


#### Comment by Anonymous on 8/25/2014 8:02:00 PM ####
@Arbil Just for the record, below are timings I get with your test code on my laptop.
fsianycpu.exe --optimize with server GC:
> run () ;;
Took 923.3096 ms
Took 1215.1609 ms
val it : unit = ()
> run () ;;
Took 913.3422 ms
Took 1217.4542 ms
val it : unit = ()
Struct version run slower.
fsi.exe --optimize with server GC:
> run () ;;
Took 750.8876 ms
Took 462.6067 ms
val it : unit = ()
> run () ;;
Took 758.2908 ms
Took 459.7404 ms
val it : unit = ()
Struct version runs faster.
RyuJIT CTP4 gives roughly similar timings.


#### Comment by Anonymous on 8/25/2014 8:40:00 PM ####
@Arbil Regarding your benchmark. I took a look at the JITted code (I made sure JIT optimizes even when running under debugger, placed breakpoints on the loops, and viewed the assembly in debugger) and it seems that, in your benchmark, some undesired optimizations do kick in depending on whether it is 64-bit or 32-bit and whether tuples or structs are being used. By "undesired optimizations" I mean that either the F# compiler (by inlining and then optimizing the functions called in the loops) or the JIT is able to eliminate some parts out of the code so you are not really measuring what you wrote. On the 64-bit JIT, the struct version generates an insane amount of instructions that clear and copy temporary copies of the struct.
What my earlier rules of thumb are based upon are my many attempts to use structs to gain performance in much more realistic settings where things can't get reduced to nothing. Even with two element structs it can take careful tweaks to get things moving really efficiently (e.g. if you pass byref and the target function can be inlined by the JIT, then copying can be avoided).
What I'd really like to see would be good enough escape analysis and elimination of object allocations (in RyuJIT) that would basically make it unnecessary to use structs for performance reasons.


#### Comment by Don Syme on 10/15/2014 8:01:00 AM ####
Given the binary-compat issues of changing the representation of Option and Tuple, One approach to this problem is to add struct-tuples as a language feature. For example, we could do this today simply by adding a set of "StructTuple<A,B,C>" types to FSharp.Core. Of course that would only work up to a fixed size of tuple - say 7 for symmetry.
People would then use StructOption and StructTuple when they needed. The FSharp.Core library wouldn't use these otherwise - e.g. they would not be used in the return type of List.* operations - but upstack libraries would be free to use them internally.
If we went in this direction, it would be even better to add StructOption and StructTuple in a way that was very close to the existing Option and Tuple support - allowing Some/None pattern matching for options, and arbitrary size of tuples, and pattern matching on tuples (without allocation).
Overall it becomes a more sizable feature - but if done well it would at least allow smoother transitions to allocation-free code.


#### Comment by Don Syme on 2/4/2016 1:47:00 PM ####
I believe we will have to add unboxed struct tuples to F# in some form or another.
The C# design for tuples is progressing and it will almost certainly involve using structs for at least smaller tuples. That's reasonable.
It is undecided as yet where the StructTuple<...> types will live and whether they will have identical semantics to the existing System.Tuple<...> types. F# will likely be quite exposed to C# design decisions here.
C# tuple types will also likely carry erased metadata (the metadata won't be in object instances)
My preferred sketch design is to add a struct annotation to the syntax of types like this:
type = struct (idopt: type * idopt: type)
| ...
and to expressions:
expr = struct (idopt: expr * idopt: expr)
| ...
and to patterns:
pat = struct (idopt: pat * idopt: pat)
| ...
The "structness" and optional identifiers would be propagated through the F# type inference process through standard unification. Otherwise, wherever possible, the existing design of F# tuples would apply.
The idea is that no code would break with this design. Unless otherwise unified, F# tuple syntax would default to the existing reference types with no identifiers.
The FSharp.Reflection facilities on tuples would be extended for struct tuples, as would the FSharp.Quotation facilities.
This is a sketch and there would no doubt be many details to add, and we must also be careful to interoperate with C# (we are in discussion with the C# team about this).
We will go ahead and marked this as "approved in principle" and we will open an RFC sooner or later.


#### Comment by Paul Westcott on 2/17/2016 2:51:00 PM ####
Just a reminder: on the 64-bit JIT, for value types > 64-bit in size there is a potential performance minefield when interacting with the "tail" IL instruction.


#### Comment by ADMIN
fsharporg-lang (F# Software Foundation Language Group, F# Software Foundation) on 3/1/2016 5:42:00 AM ####
RFC created! https://github.com/fsharp/FSharpLangDesign/blob/master/RFCs/FS-1006-struct-tuples.md


#### Comment by exercitus vir on 7/9/2016 9:36:00 AM ####
Great idea! But I am not a big fan of the syntax. Other than the possible syntax ambiguities mentioned in the RFC, it would be inconsistent with the records and unions compiled to struct, which are going to use the "Struct"-attribute. The "Struct"-attribute is also more flexible as it can be placed on top of the type, which looks much cleaner. I also don't like seeing even more parenthesis in my code, which are currently part of the RFC. An alternative to the "Struct"-attribute, e.g. [<Struct>] int * int, would be to use syntax similar to how `byref is specified`, which is actually a type. E.g. Struct<int * int>.
Structness inference seems to be an essential feature (rather than an optional feature). Otherwise, it would be no fun working with struct tuples.
I don't really understand the value-add of tuple field metadata.I think that if you want to name the components and have them be part of the type, then you should simply use a (struct) record since that what it's for.

