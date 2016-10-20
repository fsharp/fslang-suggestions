# Add support for "fixed" [5663721] #

**Submitted by Don Syme on 3/21/2014 12:00:00 AM**  
**45 votes on UserVoice prior to migration**  

F# 3.x doesn’t support “fixed” local variables in the style of C#. This is a missing hole in our native interop story and has been a user request. It is reasonable to lift this limitation if a quality implementation is provided.



## Response ##
** by fslang-admin on 8/2/2016 12:00:00 AM **

Completed. The RFC is at https://github.com/fsharp/FSharpLangDesign/blob/master/RFCs/FS-1015-support-for-fixed.md
Don Syme, F# Language and Core Library Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5663721)**


## Comments ##


#### Comment by Will Smith on 3/23/2014 9:30:00 AM ####
Would "fixed" be similar to how "use" works today? If you have a fixed local variable, at the end of its scope, it will get freed?


#### Comment by Jack Pappas on 3/23/2014 11:12:00 AM ####
Will -- there's two parts to 'fixed': the variable whose value is bound by the 'fixed', and the value which is bound to the variable. In C#, when you use a 'fixed' block, the object being fixed (e.g., an array) is pinned by the GC so it can't be relocated, and you're given a pointer to that object so it can be passed into native code. Both 'using' and 'fixed' blocks in C# are compiled into a try/finally; a 'using' block calls '.Dispose()' on the object bound by the block within the 'finally' clause, whereas a 'fixed' block simply zeros-out (assigns null) to the local variable holding the pinned reference.
To answer your question -- yes, 'fixed' would be very similar to how 'use' works today. When the variable goes out of scope, the finally block would be executed and assign null to the local variable (within the IL) holding the pinned reference, which triggers the GC to unpin the object.


#### Comment by Don Syme on 6/20/2014 12:25:00 PM ####
Jack - the code gen should work the same as for C#


#### Comment by Don Syme on 6/20/2014 12:31:00 PM ####
I consider this approved in principle for F# 4.0, though some details may need to be sorted out.
If you think this should not be done, please chime in with details below.
If you have specific questions on the design, please chime in below.
An implementation and testing would need to be provided by someone in the F# community (possibly including Microsoft or Microsoft Research, though not limited to them).Currently, initial implementations of approved language design can be submitted as pull requests to the "fsharp4" branch of https://visualfsharp.codeplex.com/SourceControl/latest. F# 4.0 is open for business.
I encourage you to work towards an implementation and testing for this feature.
Don Syme, current BDFL, F# Language


#### Comment by Fraser Waters on 7/26/2014 4:13:00 PM ####
Something that the CLI supports but is not allowed by C# is fixed pointers to generic types / arrays of generic types. This is very useful for communicating with DirectX/OpenGL and currently both major libraries for these APIs (SharpDX/OpenTK) have to rewrite their CIL code after C# compilation to add in fixed generic pointers. If we could diverge from C# here and allow everything the underlying CLI supports that would be useful.


#### Comment by Don Syme on 2/5/2016 8:57:00 AM ####
See here for a good motivating example: /archive/suggestion-5670163-fixed-length-arrays and this gist https://gist.github.com/jack-pappas/9725445

