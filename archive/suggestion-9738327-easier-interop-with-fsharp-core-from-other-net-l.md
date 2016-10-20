# easier interop with FSharp.Core from other .net languages [9738327] #

**Submitted by Gauthier Segay on 9/13/2015 12:00:00 AM**  
**11 votes on UserVoice prior to migration**  

A first example is FSharpOption<T> and it's usage in C#/VB, extend FSharp.Core with this module to make it easier to use:
http://fssnip.net/so
There are other efforts to be made to make FSharp.Core look not too alien in other languages, like being able to await on FSharpAsync.
Having design guidelines for this type of interop doesn't remove the need for basic F# constructs to be exposed in a convenient way to other dotnet languages.



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/9738327)**


## Comments ##


#### Comment by Gauthier Segay on 9/13/2015 5:26:00 AM ####
For discrimated union, the root type expose get_Is* methods, it should be exposed as Is* methods instead.


#### Comment by Dzmitry Lahoda on 9/22/2015 12:46:00 PM ####
It would be yet another path to introduce F# into C# heavy bureaucratic enterprise. I know that F# Core is part of .NET 4.5. So just add reference from GAC.

