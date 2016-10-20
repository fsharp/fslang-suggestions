# Allow modules within classes [6080632] #

**Submitted by David Siegel on 6/20/2014 12:00:00 AM**  
**2 votes on UserVoice prior to migration**  

I assumed I could declare modules within classes, and I tried to create one to organize values private to my class, and found that it was not allowed:
type MyView() =
module Colors =
let button = 0x0000FF
let label = 0xCCCCCC

let Button = new UIButton(BackgroundColor=Colors.button)



## Response ##
** by fslang-admin on 9/6/2014 12:00:00 AM **

Declining this. Allowing nested type definitions ala C# would take priority, and nested modules would be considered as part of that feature.
Don Syme, BDFL F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6080632)**


## Comments ##

