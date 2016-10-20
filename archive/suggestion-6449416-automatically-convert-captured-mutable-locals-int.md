# Automatically convert captured mutable locals into refs. [6449416] #

**Submitted by Matthew Parkinson on 9/17/2014 12:00:00 AM**  
**18 votes on UserVoice prior to migration**  

There are several places where refactoring code can cause it not to compile due to captured mutable locals. For instance,
let mutable worklist = ...
for c in collection do worklist <- c::worklist
If this gets converted, to a data structure that doesn't work with "for" but does expose some form of iter method:
let mutable worklist = ...
collection.iter (fun c -> worklist <- c::worklist)
This doesn't compile, and you need to write
let worklist = ref ...
collection.iter (fun c -> worklist := c::!worklist)
Also, if you wanted to factor out the worklist adding code
let mutable worklist = ...
let add c = worklist <- c :: worklist
for c in collection do add c
The compiler could automatically insert the refs where necessary using a pretty simple analysis, and this awkward corner of when you can write mutable and when you can't would disappear.



## Response ##
** by fslang-admin on 11/12/2014 12:00:00 AM **

This is now completed and available in preview releases of F# 4.0.
For an early Visual Studio preview release see here (cross platform releases will follow) – http://blogs.msdn.com/b/fsharpteam/archive/2014/11/12/announcing-a-preview-of-f-4-0-and-the-visual-f-tools-in-vs-2015.aspx
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6449416)**


## Comments ##


#### Comment by Mårten Rånge on 9/17/2014 1:42:00 PM ####
While I think the idea is nice and better than the implicit capture by value in C# I have some concerns
let c = x
let mutable c = x
The big difference here is that the compiler allows writes to c. AFAIK the generated IL is very similar.
If I understand your proposal *if* c was captured by a lambda it would then convert this into ref x.
Refs in F# requires AFAIK an object allocation. The cost is small but not zero. In addition it generates more objects for the GC to collect.
Some F# users are already concerned about certain idioms in F# requires object allocations when running on platforms with a weak GC (like XBOX).
So I would be somewhat reluctant to have non-zero cost changes to the generated code based on the subtle condition if a mutable variable was captured or not.
But chances are it's just me that thinks this way.


#### Comment by Matthew Parkinson on 9/18/2014 4:31:00 AM ####
@Mårten, thanks for your comment. It is very valid concern.
The compiler will throw out code based on "subtle condition"s, I think this may be a barrier to adoption for some users. We have to balance that against, the later problems of silent allocation for more constrained situations.
I would propose we have a compiler option to give warning for this allocation. All existing compiling code would compile identically.
There are also many cases where the compiler would be able to optimise away the allocation due to inlining. If the closures gets inlined, then the code doesn't need to do allocation. At the moment, this is not possible, as the check occurs before the optimiser.


#### Comment by Don Syme on 10/10/2014 11:03:00 AM ####
I've worked on this with Matt today and am happy with the design proposal. I've noticed a lot of beginners getting tripped up by the sudden switch between "mutable" and "ref" and over time I've come to believe that the regularity Matt proposes is a better place to be.
The design is
(a) Implicitly promote local "let mutable" to a ref allocation when captured by closures, including object expressions, sequence expressions etc.
(b) Give an optional (off-by-default warning) when this happens, similar to warning "1182" for unused variables

