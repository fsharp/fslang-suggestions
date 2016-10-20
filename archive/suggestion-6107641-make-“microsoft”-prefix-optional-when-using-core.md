# Make “Microsoft” prefix optional when using core FSharp.Core namespaces, types and modules [6107641] #

**Submitted by Don Syme on 6/27/2014 12:00:00 AM**  
**7 votes on UserVoice prior to migration**  

The modules and types from the FSharp.Core dll use the names "Microsoft.FSharp.Collections" etc.
Since the F# language is now cross-platform and open-source, it is appropriate that source code be able to optionally use just "FSharp.Collections". This would also mean the names match the name of the DLL (FSharp.Core).
This would not be a breaking change, existing code would continue to compile.
The compiled form used in FSharp.Core.dll wouldn't change, for reasons of binary compatibility.



## Response ##
** by fslang-admin on 1/21/2015 12:00:00 AM **

This has been completed for F# 4.0+, see https://github.com/fsharp/FSharpLangDesign/blob/master/FSharp-4.0/MicrosoftOptionalDesignAndSpec.md
The overall status for F# 4.0+ is here: https://github.com/Microsoft/visualfsharp/wiki/F%23-4.0-Status
Don Syme, current BDFL for F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6107641)**


## Comments ##


#### Comment by John Tarbox on 9/7/2014 8:03:00 AM ####
Is this a breaking change? In other words will references to Microsoft.FSharp.Collections need to be changed before a program will compile under F# 4.0?


#### Comment by Alfonso Garcia-Caro on 9/7/2014 8:25:00 AM ####
I don't believe it's a bad thing to keep "Microsoft" prefix as a remainder that F# started as a contribution of Microsoft to the community. This can be an incentive for big companies to contribute to open source projects.


#### Comment by Don Syme on 9/7/2014 9:49:00 AM ####
@JohnTarbox - using the "Microsoft" prefix would be optional (as stated in the title of the suggestion)


#### Comment by Kevin Ransom on 9/7/2014 12:02:00 PM ####
This will indeed break applications that, contain types with the names of our collection types in the namespace fsharp.collections. That may not be very likely but it could happen.


#### Comment by Don Syme on 9/7/2014 2:34:00 PM ####
Hi Kevin - Yes, I'd like to investigate this to make sure this is not a breaking change.
The F# name resolution rules currently mean that types defined in non-FSharp.Core DLLs would have precedence (F# name resolution prefers the most recently introduced type based on the assembly reference list and "open" declarations, Since FSharp.Core comes first in asssembly resolution, later types will have precedence).
However there are some exceptions that we need to innvestigate, particularly for generic types that get overloaded on arity. However that case will very rare indeed and any example would be very contrived - but we'll still check it out.

