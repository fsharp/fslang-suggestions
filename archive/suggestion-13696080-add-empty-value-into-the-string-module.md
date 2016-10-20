# Add empty value into the String module [13696080] #

**Submitted by Rex Ng on 5/2/2016 12:00:00 AM**  
**1 votes on UserVoice prior to migration**  

Copied from this GitHub issue: https://github.com/Microsoft/visualfsharp/issues/1139
Right now, if I do not want to use the empty string literal "", I have to do something like
printfn "%s" System.String.Empty
in order to reference the public static readonly instance of the empty string in the BCL.
It would be more convenient if I can just do:
// Referencing the F# String module here instead of System.String
printfn "%s" String.empty
I would imagine String.empty to be an alias to System.String.Empty so there should be just a one-line code change:
module String =
[<CompiledName("Empty")>]
let empty = ""
// Other String functions
I think this will be useful because we already have similar empty values from other modules such as Seq, List, and Array.
This will also make the code more explicit (i.e. convey to others that 'I want an empty string here' instead of 'this can potentially be a typo').



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/13696080)**


## Comments ##


#### Comment by Reed Adams on 5/3/2016 10:10:00 AM ####
While you're waiting for an official library solution, it might be worth noting that you can extend and approximate the desired functionality in your own code for the time being, possibly giving you the expressiveness you're after.
Example at: https://dotnetfiddle.net/rFSPQl
Hopefully this gets you closer to where you want to be until a library solution is in place.

