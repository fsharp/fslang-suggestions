# Allow Type Providers to be compiled to *.exe file. [5672202] #

**Submitted by Sergey Tihon on 3/23/2014 12:00:00 AM**  
**10 votes on UserVoice prior to migration**  

http://stackoverflow.com/questions/18181906/f-type-provider-compiled-as-exe-file
Type Provider compiled as *.exe file can have [<EntryPoint>]. Such assembly may be executed as standalone process for design-time type inference.
This feature dramatically simplify development of Interop Type Providers (R, Python, PowerShel). It allows to execute type inference in 64 environments and safely deal with unmanaged code that potentially can crush VS process.



## Response ##
** by fslang-admin on 2/5/2016 12:00:00 AM **

Declined per my comment – this is best done by having a type provider start a proxy process, just as the R provider does.
Don Syme
F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5672202)**


## Comments ##


#### Comment by Gustavo Guerra on 3/24/2014 5:43:00 PM ####
This is actually a very annoying limitation. I know it's not that a common pattern, but I often use libraries as .exe so they can have both uses, and not being allowed in TPs is annoying. I keep changing project type to debug


#### Comment by Bryan Edds on 3/27/2014 9:46:00 PM ####
This sounds like something that just needs to get done.


#### Comment by Don Syme on 6/25/2014 7:36:00 AM ####
I think the best way to progress this is to somehow generalize the technique used by the FSharp R type provider, which (optionally?) uses a server process. Putting the generalization of that into the F# Type Provider Starter Pack would make sense.
Neither of these would require changes to the F# compiler itself.

