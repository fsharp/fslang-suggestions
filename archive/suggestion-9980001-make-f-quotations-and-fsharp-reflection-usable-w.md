# Make F# quotations and FSharp.Reflection usable with mscorlib and FSharp.Core for other target profiles [9980001] #

**Submitted by Don Syme on 9/29/2015 12:00:00 AM**  
**6 votes on UserVoice prior to migration**  

F# quotations have nodes related to tuple, delegate, function, union and record types. Likewise, FSharp.Reflection has helpers related to union and record types.
When running on .NET 4.x everything works fine. But if you use ReflectionOnlyLoadFrom to get an FSharp.Core for an alternative profile, then you can't use most F# quotation nodes correctly - all sorts of things go wrong when you try to construct nodes that refer to the types stemming from this "other profile" FSharp.Core. Note you are still running .NET 4.x code, but reflecting over assemblies relevant to other profiles.
This also applies when implementing the System.Reflection types yourself based on information extracted from these DLLs. THis is done in the CommonProviderImplementation in FSharp.Data, e.g. see https://github.com/fsharp/FSharp.Data/tree/dbfe86e00c766de1227e7e1994942ed93f74db97/src/CommonProviderImplementation
There are workarounds to use backdoors to avoid the checks that the constructors for quotation nodes perform. For example, see https://github.com/fsharp/FSharp.Data/blob/dbfe86e00c766de1227e7e1994942ed93f74db97/src/CommonProviderImplementation/UncheckedQuotations.fs
However, this should really be fixed in FSharp.Core. There are various fixes possible: either add the Unchecked family of functions, or make the checks only take into account type names rather than assembly identities.
Likewise fixes should be made in FSharp.Reflection (especially FSharpUnionCase)



## Response ##
** by fslang-admin on 6/17/2016 12:00:00 AM **

Approved, this should always have been allowed.
Don Syme, F# Language and Core Library Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/9980001)**


## Comments ##


#### Comment by Don Syme on 1/27/2016 12:27:00 PM ####
I started the implementation of this but it is quite tricky. Here's the work in progress. The main thing missing is testing and fixes for FSharpUnionCase https://github.com/dsyme/visualfsharp/tree/quotation-fixes-1
Don Syme


#### Comment by Jared Hester on 3/6/2016 1:26:00 AM ####
I did a rough sketch of getting union field names with reflection only using TypeInfo
https://gist.github.com/cloudRoutine/3884b1ac325bbd5553f9

