# Additional intrinsics for the NativePtr module [5670328] #

**Submitted by Jack Pappas on 3/23/2014 12:00:00 AM**  
**10 votes on UserVoice prior to migration**  

When interoperating with native code, it would be handy if the NativePtr module included some additional "intrinsic" functions for taking advantage of low-level IL instructions; specifically, I'd like to be able to use 'cpblk', 'initblk', 'initobj', and 'copyobj'.
It would also be nice to have an easy way of checking for null pointer values.
Example implementation of these functions:
[<RequireQualifiedAccess>]
[<CompilationRepresentation(CompilationRepresentationFlags.ModuleSuffix)>]
module NativePtr =
[<GeneralizableValue>]
[<NoDynamicInvocation>]
[<CompiledName("Zero")>]
let inline zero<'T when 'T : unmanaged> : nativeptr<'T> =
(# "ldnull" : nativeptr<'T> #)
[<NoDynamicInvocation>]
[<CompiledName("IsNull")>]
let inline isNull<'T when 'T : unmanaged> (ptr : nativeptr<'T>) =
(# "ceq" zero<'T> ptr : bool #)
[<Unverifiable>]
[<NoDynamicInvocation>]
[<CompiledName("InitBlockInlined")>]
let inline initBlock (p : nativeptr<'T>) (value : byte) (size : uint32) =
(# "initblk" p value size #)
[<Unverifiable>]
[<NoDynamicInvocation>]
[<CompiledName("CopyBlockInlined")>]
let inline memcpy (destPtr : nativeptr<'T>) (srcPtr : nativeptr<'T>) (count : int) =
(# "cpblk" destPtr srcPtr (count * sizeof<'T>) #)
[<Unverifiable>]
[<NoDynamicInvocation>]
[<CompiledName("InitPointerInlined")>]
let inline clear (p : nativeptr<'T>) =
(# "initobj !0" type ('T) p #)
[<Unverifiable>]
[<NoDynamicInvocation>]
[<CompiledName("CopyPointerInlined")>]
let inline copy (destPtr : nativeptr<'T>) (srcPtr : nativeptr<'T>) =
(# "copyobj !0" type ('T) destPtr srcPtr #)



## Response ##
** by fslang-admin on 11/8/2014 12:00:00 AM **

I’m marking this as “approved” for F# 4.0+.
A pull request for this feature has been submitted here:
https://visualfsharp.codeplex.com/SourceControl/network/forks/jackpappas/fsharpcontrib/contribution/7134
Thanks
Don, F# Language Design


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5670328)**


## Comments ##


#### Comment by Will Smith on 3/23/2014 10:50:00 AM ####
Definitely agree with this! I've had to create my own naive versions of some of these. https://github.com/TIHan/FQuake3/blob/4d5a5702a6ae06cd8e4b57431e656ab4dfd39ac4/src/FSharp/Engine/NativeInterop.fs#L73
With your listings, maybe another one that casts a nativeptr to another nativeptr type would be super useful as well, though may not be related to your intrinsics. Perhaps, NativePtr.cast ?


#### Comment by Jack Pappas on 3/28/2014 6:19:00 PM ####
Will -- nativeptr<'T> is just nativeint with a generic type annotation grafted onto it, and it's erased to nativeint at compile-time. Implementing a cast function like you described should be straightforward if you use the F# proto-compiler. IMO it wouldn't be a good addition to FSharp.Core though, because it would totally bypass any and all type-safety. In any case, the difference between your cast function and the intrinsics I listed above -- you can implement your cast with the current version of F#, but the above intrinsics can't be compiled due to some changes that were made to the ILX layer and metadata picker in F# 3.0.


#### Comment by Jack Pappas on 3/28/2014 6:21:00 PM ####
One other thing to point out -- having these intrinsics available in normal F# code would make it possible to implement high-speed native interop libraries like SharpDX without having to resort to IL-rewriting: https://visualstudio.uservoice.com/forums/121579-visual-studio/suggestions/4334135-extend-c-to-close-gaps-for-high-performance-nativ


#### Comment by Will Smith on 4/13/2014 1:55:00 PM ####
Yea, it was only recently did I found out that nativeptr<'T> is really just a nativeint. Thanks for giving more info on it.
You make a good point on the type safety, but as we are already in an unsafe context and potentially messing with unmanaged memory, a NativePtr.cast would only benefit handling memory. Is there a better way of going about it? I would interested in an alternative.


#### Comment by Anonymous on 6/25/2014 5:46:00 PM ####
In this vein, it would be useful to be able to easily use what amounts to a binary cast from a byte array, as in C# (fixed byte* p = &b[offset]) { return *(SomeUsefulStruct*)p; }


#### Comment by Frank Niemeyer on 7/2/2014 3:42:00 AM ####
@Sebastian: The only thing that F# is missing for this is the "fixed" statement (you'd have to pin the byte[] by allocating a GCHandle). The dereferencing (i.e. copy the contents of the byte array to a struct of type T) can achieved today using p |> NativePtr.toNativeInt |> NativePtr.ofNativeInt<'T> |> NativePtr.read.


#### Comment by Jack Pappas on 7/9/2014 7:00:00 PM ####
@Sebastian @FrankNiemeyer I've also suggested 'fixed' be implemented for F# 4.0: /archive/suggestion-5663721-add-support-for-fixed


#### Comment by Jack Pappas on 7/9/2014 7:01:00 PM ####
I've implemented these additional intrinsic functions and will be sending a pull request ASAP: https://visualfsharp.codeplex.com/SourceControl/network/forks/jackpappas/fsharpcontrib?branch=native-interop

