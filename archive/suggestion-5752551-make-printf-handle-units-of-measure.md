# Make printf handle units of measure. [5752551] #

**Submitted by Matthew Peacock on 4/9/2014 12:00:00 AM**  
**21 votes on UserVoice prior to migration**  

Currently printf requires all numeric types with units of measure to have the units removed. For example:
let years = 1<year>
printfn "%d" years // compile error
printfn "%d" (int years) // works
This gets quite ugly in code that uses units of measure heavily.



## Response ##
** by fslang-admin on 11/8/2014 12:00:00 AM **

This work has now been completed for the “fsharp4” branch (submitted, reviewed and committed)
https://visualfsharp.codeplex.com/SourceControl/changeset/aa7e945db107d0baf8af8d39c2d82185213c2796
Thanks
Don Syme, current BDFL for F# Language Design


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5752551)**


## Comments ##


#### Comment by Loic Denuziere on 4/25/2014 11:41:00 AM ####
printf could even take advantage of the presence of the measure. We could imagine something like:
[<Measure>]
[<MeasurePrintFormat(" meters")>]
type meter
let distance = 3<meter>
printfn "The distance is %d" distance // Prints: The distance is 3 meters


#### Comment by Don Syme on 7/10/2014 10:59:00 AM ####
An implementation of this feature has now been submitted at: https://visualfsharp.codeplex.com/SourceControl/network/forks/dsyme/cleanup/contribution/7107


#### Comment by exercitus vir on 6/19/2015 6:10:00 PM ####
This was definitely needed. I love Loic's idea of being able to specify the print format of measures.

