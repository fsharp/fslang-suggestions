# Implement interface delegating [15915547] #

**Submitted by Ivan J. Simongauz on 9/3/2016 12:00:00 AM**  
**1 votes on UserVoice prior to migration**  

Implement interface delegating by next syntax:
type MyType() =
let delegator : IAddingService
interface IAddingService by delegator with
member this.Add x y = // <- this is override
x + y
Special behavior when event in interface - sender substitution



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/15915547)**


## Comments ##

