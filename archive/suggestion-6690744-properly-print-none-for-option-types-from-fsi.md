# Properly print 'None' for option types from FSI [6690744] #

**Submitted by TeaDrivenDev _ on 11/9/2014 12:00:00 AM**  
**18 votes on UserVoice prior to migration**  

FSI output properly handles 'Some x', but often prints 'None' as 'null', apparently when the value is part of a larger type.
let x : uint16 option = None
correctly results in: val x : uint16 option = None
let y : string * uint16 option = "", None
instead prints: val y : string * uint16 option = ("", null)



## Response ##
** by fslang-admin on 2/5/2016 12:00:00 AM **

This should certainly be fixed, as much as possible
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6690744)**


## Comments ##


#### Comment by Grant Crofton on 11/13/2014 4:03:00 AM ####
Yes please, this can be pretty annoying (especially when trying to show people F#)


#### Comment by FANG Colin on 12/7/2014 6:35:00 PM ####
> printfn "%A" (1, None)
printfn "%A" None
printfn "%O" (1, None)
printfn "%O" None
(1, null)
<null>
(1, )
<null>

