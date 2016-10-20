# Support for [<CLIEvent>] on modules [6984621] #

**Submitted by Isaac Abraham on 1/19/2015 12:00:00 AM**  
**5 votes on UserVoice prior to migration**  

As the name suggests. You can create [<CLIEvent>]s on classes as both instance and static members but not on a module. As far as the consuming e.g. C# library, the fact we're using a module in F# is unknown; from the F# side it's a pity you have to create classes for this behaviour rather than more idiomatic modules.



## Response ##
** by fslang-admin on 7/17/2015 12:00:00 AM **

Many thanks for this suggestion. It is being marked as declined – for discussion see the comments above.
Further comments, use cases, information and discussion welcome
Don Syme, F# Language and Core Library Evolution.


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6984621)**


## Comments ##


#### Comment by Don Syme on 7/17/2015 9:16:00 AM ####
Hi Isaac, my feeling is that requiring a class is consistent with the F# language design. CLIEvent is an object-programming feature - like properties, abstract members etc.


#### Comment by Don Syme on 7/17/2015 9:16:00 AM ####
Also, static events are rare in design.


#### Comment by Isaac Abraham on 7/17/2015 9:19:00 AM ####
Understood. Perhaps a warning or error would be preferable to what you currently get though, which kind of falls between both options i.e. it compiles but generates something unexpected.

