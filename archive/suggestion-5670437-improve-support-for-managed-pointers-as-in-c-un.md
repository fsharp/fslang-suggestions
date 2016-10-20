# Improve support for managed pointers (as in C# unsafe code) [5670437] #

**Submitted by Jack Pappas on 3/23/2014 12:00:00 AM**  
**33 votes on UserVoice prior to migration**  

It is currently quite difficult in F# to interoperate with 'unsafe' C# code due to C#'s use of managed pointers (ilsigptr<'T> in F#). At the very least, it would be handy to have a ManagedPtr module available in FSharp.Core under the Microsoft.FSharp.NativeInterop namespace, similar to the existing NativePtr module.
If support for managed pointers were to be improved, it would be beneficial to rename them -- ilsigptr<'T> is a rather obscure name for those without a good understanding of IL and the CLR's type system. Perhaps we could rename it to managedptr<'T>, which would fit nicely alongside the existing nativeptr<'T>.
Improved support for managed pointers would also go hand-in-hand with support for 'fixed'-bound variables: /archive/suggestion-5663721-add-support-for-fixed
When using the (&&) operator, and the * modifier in external function signatures, the F# compiler infers the types as nativeptr<'T>; I think it would be preferable if the compiler inferred these as managedptr<'T> instead, for better type safety when interoperating with other languages (e.g., C#). This could be implemented as the new default behavior in a future version of F#, and anyone relying on the nativeptr<'T> behavior could turn it back on using a compiler flag (e.g., --prefer-nativeptrs).



## Response ##
** by fslang-admin on 2/4/2016 12:00:00 AM **

Marking as declined pending an example where this is needed


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5670437)**


## Comments ##


#### Comment by Jack Pappas on 3/29/2014 10:02:00 AM ####
One additional idea which is semi-related to this -- the 'nativeptr<'T>' type in F# is currently just a type alias for 'nativeint'. Why doesn't it use the CLR's built-in unmanaged pointer type to preserve type information in the compiled assemblies? C# supports this unmanaged pointer type, e.g., when using the 'fixed' construct.


#### Comment by Frank Niemeyer on 6/22/2014 11:18:00 AM ####
@Jack: Only concrete instances of nativeptr<'T> translate to the corresponding T*. When you expose an F# function with a, e.g., nativeptr<byte> in its signature it surfaces as a byte* in C#; only a generic nativeptr<'T> shows up as an IntPtr (= native int), maybe because C# cannot really handle generic typed pointers (no "unmanaged" type constraint).


#### Comment by Don Syme on 2/4/2016 1:02:00 PM ####
I need more information on this. Could you give an example please that shows a case where we need to make use of ilsigptr from C#, and they are not interpreted as byref<T>?


#### Comment by Don Syme on 2/4/2016 1:03:00 PM ####
I will mark this as declined pending more details.

