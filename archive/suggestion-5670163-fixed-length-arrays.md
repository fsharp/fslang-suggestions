# Fixed Length Arrays [5670163] #

**Submitted by Will Smith on 3/23/2014 12:00:00 AM**  
**12 votes on UserVoice prior to migration**  

Originally posted here: https://groups.google.com/forum/#!topic/fsharp-opensource/pI73-GkoxbY
The ability to have fixed arrays would most definitely make interop easier, instead of having to calculate the size by hand and just hope for the best. I have been burned by calculating everything by hand a ton.



## Response ##
** by fslang-admin on 2/5/2016 12:00:00 AM **

Closing since it appears this is possible in F# – but “fixed” is missing, which is this approved issue: /archive/suggestion-5670163-fixed-length-arrays


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5670163)**


## Comments ##


#### Comment by Jack Pappas on 3/23/2014 10:56:00 AM ####
Hi Will -- can't you already do this via the [<MarshalAs>] attribute? For example, the code from your newsgroup post could be implemented like this:
namespace Blah
open System.Runtime.InteropServices
[<Struct>]
type vec3_t =
val mutable X : int
val mutable Y : int
val mutable Z : int
[<Struct>]
[<StructLayout(LayoutKind.Sequential, CharSet = CharSet.Ansi)>]
type md3Frame_t =
[<MarshalAs(UnmanagedType.ByValArray, SizeConst = 2)>]
val mutable bounds : vec3_t[];
val mutable localOrigin : vec3_t;
val mutable radius : float32;
[<DefaultValue>]
[<MarshalAs(UnmanagedType.ByValTStr, SizeConst = 16)>]
val name : string;


#### Comment by Will Smith on 3/23/2014 11:35:00 AM ####
I believe I've tried this in the beginning, it doesn't exactly like I want. Some more info: http://www.mono-project.com/Interop_with_Native_Libraries#Marshaling_Class_and_Structure_Members
Example:
[<Struct>]
[<StructLayout (LayoutKind.Sequential)>]
type ManagedStruct_Slow =
[<MarshalAs (UnmanagedType.ByValArray, SizeConst=10)>]
val data : int []
[<MarshalAs (UnmanagedType.ByValTStr, SizeConst=32)>]
val name : string
The actual size of this struct is only 8 bytes, and this struct isn't considered unmanaged anymore. I need the struct to be exactly the same size as what is on the C side. This makes the interop 1-to-1 completely. When I tried this in the beginning, it did not work, especially when C is calling F#.


#### Comment by Jack Pappas on 3/23/2014 1:00:00 PM ####
Will -- one issue with your example code is that you left out the CharSet.Ansi modifier in [<StructLayout>]. This means that unless you're using Windows 98 or ME (hopefully not!), your strings are getting marshalled with 2-byte Unicode chars instead of 1-byte 'unsigned char's as C expects.
If you define this type, then do sizeof<ManagedStruct_Slow> in your code, it'll return 8 or 16 depending on whether you're on a 32- or 64-bit platform, because the struct only really contains two references. It should still be marshalled correctly though, thanks to the MarshalAs attributes.
As for the struct not being considered 'unmanaged', I assume you want to use the struct with nativeptr<'T>? If possible, you're better off using byref<'T> (&) instead of nativeptr<'T> (&&)/(*); I often just create simple structs wrapping 'nativeint' for this purpose. I'm personally not a big fan of nativeptr<'T> -- I've run into too many issues with it over the years.


#### Comment by Will Smith on 3/23/2014 4:10:00 PM ####
Hey Jack,
It was an example to just show that the struct will not be the same size as a C version. I'm aware of the differences that occur with strings and how they need to be handled properly.
I can try to give this another go using MarshalAs and byref; but if I remember right, this wasn't working for me. Last time I tried was 8-9 months ago. If it works out then cool, :) , interops will be a bit better.
What are some the issues that you run into with nativeptr<'T>? I've only run into the fixed length problems.
Also, here is an example of how I'm using nativeptr https://github.com/TIHan/FQuake3/blob/7a42a92d1a182a173eb09590ffd7f0c50dd24adc/src/FSharp/Engine.Renderer/NativeMappings.fs


#### Comment by Will Smith on 3/23/2014 5:26:00 PM ####
From the Mono documentation in a previous comment, it says "the runtime doesn't automatically allocate arrays specified as UnmanagedType.ByValArray. The programmer is still responsible for allocating the managed array." More info: http://www.mono-project.com/Interop_with_Native_Libraries#marshaling-members-summary
This is why I couldn't use it. Having to manually allocate, adds not only additionally overhead, but additional complexity. Only having the param type be "nativeptr<md3Frame_t>" and that's all I have to worry about, feels a lot more sane considering the magnitude of the amount of C structs I'm having to deal with. Also, with the type being unamanaged and using nativeptr, I'm not doing any marshaling at all, therefore I do not have any performance issues associated with marshaling at that layer.
I need this kind of control when manually mapping an unmanaged type to an idiomatic F# record/struct, and vice versa.


#### Comment by Jon Harrop on 3/27/2014 5:27:00 AM ####
I would also like fixed arrays in F# but, alas, I have long since run out of user voice votes. :-(


#### Comment by Jack Pappas on 3/29/2014 9:55:00 AM ####
I've hand-translated an example using C# fixed buffers to F#. Unfortunately, the F# code doesn't compile, because the original example used the C# 'fixed' construct to pin the class containing the buffer; however, the structs shown in the example could be used in current versions of F#, e.g., for marshalling purposes.
https://gist.github.com/jack-pappas/9725445


#### Comment by Don Syme on 2/5/2016 8:56:00 AM ####
Looking at the discussion it seems the last comment by Jack Pappas shows a way to do this, apart from the orthogonal question of support for "fixed", covered here: /archive/suggestion-5663721-add-support-for-fixed
So I think we can close this and I'll link across to here for the "fixed" issue

