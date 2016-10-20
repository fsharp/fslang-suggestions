# Allow opening of static classes (matching the C# design) [6958404] #

**Submitted by Isaac Abraham on 1/13/2015 12:00:00 AM**  
**31 votes on UserVoice prior to migration**  

You currently can't "open" a static class e.g. System.Console - only modules or namespaces. We should be able to also open static classes as well.



## Response ##
** by fslang-admin on 2/4/2016 12:00:00 AM **

Thanks for the suggestion. Approved in principle.
We will open an RFC for this in due course https://github.com/fsharp/FSharpLangDesign/tree/master/RFCs


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6958404)**


## Comments ##


#### Comment by exercitus vir on 6/22/2015 3:32:00 PM ####
I agree. Modules are compiled down to static classes anyway, so there should be no technical reason for disallowing it.


#### Comment by Don Syme on 2/4/2016 5:49:00 PM ####
Yes, this should I suppose be implemented to match the corresponding C# feature, since static classes will begin to be more common coming from the C# world.


#### Comment by Marc Sigrist on 2/10/2016 6:15:00 AM ####
As in C#, static classes defined in F# will probably become more common. If so, would we still require static classes in F# to be defined via [<AbstractClass; Sealed>]? Or, would it make sense to reuse the static keyword known from 'static member' for 'static type'?

