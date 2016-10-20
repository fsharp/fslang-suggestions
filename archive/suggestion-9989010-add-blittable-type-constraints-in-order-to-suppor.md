# Add blittable type constraints in order to support more robust native interop [9989010] #

**Submitted by Zoltan Podlovics on 9/30/2015 12:00:00 AM**  
**3 votes on UserVoice prior to migration**  

Proper native interop require strict type definition where the type representation is the same both on managed and unmanaged world. This represents a subset of unmanaged types.
Why this could be important?
The blittable type constraint could prevent lot's of type errors which may result errors or crashes. While it is possible to implement the check that run at runtime the static compile time check could provide more robust solution.
Unless struct with Sequential and Pack=1 or Explicit layout specified the JIT compiler free to pad the structure align the fields in order to provide better execution.
1) OpenTK project use the following checks for unmanaged (blittable type) tests:
https://github.com/mono/opentk/blob/master/Source/OpenTK/BlittableValueType.cs
2) Masterig Structs
http://www.developerfusion.com/article/84519/mastering-structs-in-c/
"What is important is that the compiler will add padding bytes to align the data within a struct. You can control the padding explicitly, but notice that some processors throw an exception if you use data that isn't aligned, and this creates a more complicated problem for .NET Compact users."
3) Ecma 355 II.10.1.2 Type layout attributes
"[Rationale: The default auto layout should provide the best layout for the platform on which the code
is executing. sequential layout is intended to instruct the CLI to match layout rules commonly
followed by languages like C and C++ on an individual platform, where this is possible while still
guaranteeing verifiable layout. explicit layout allows the CIL generator to specify the precise layout
semantics. end rationale]"
4) F# unmanaged type definition (which should remain as is)
"5.2.9 Unmanaged Constraints
An unmanaged constraint has the following form:
typar : unmanaged
During constraint solving (§14.5), the constraint type : unmanaged is met if type is unmanaged as specified below:
Types sbyte, byte, char, nativeint, unativeint, float32, float, int16, uint16, int32, uint32, int64, uint64, decimal are unmanaged.
Type nativeptr<type> is unmanaged.
A non-generic struct type whose fields are all unmanaged types is unmanaged."
Example.:
let safeCall (x : 'T when 'T: blittable and 'T: struct) = nativeCall(x)



## Response ##
** by fslang-admin on 2/5/2016 12:00:00 AM **

Merging with /archive/suggestion-6359526-add-serializable-and-blittable-constraints-fo


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/9989010)**


## Comments ##


#### Comment by Don Syme on 2/4/2016 6:12:00 PM ####
Combining with this suggestion: https://fslang.uservoice.com/admin/forums/245727-f-language/suggestions/6359526-add-serializable-constraint-for-types

