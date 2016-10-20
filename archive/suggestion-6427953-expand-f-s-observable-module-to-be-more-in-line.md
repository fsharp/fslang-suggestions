# Expand F#'s Observable module to be more in line with Reactive Extensions [6427953] #

**Submitted by Dave Thomas on 9/12/2014 12:00:00 AM**  
**29 votes on UserVoice prior to migration**  

With F#'s Observable module we only have:
add, choose, filter, map, merge, pairwise, partition, scan, split, subscribe.
It would be great to expand the default F# experience along the same lines that the Collections are being enhanced, adding in missing functions like: buffer, delay, interval, sample, throttle, timeout, timestamp, generate, etc



## Response ##
** by fslang-admin on 7/18/2015 12:00:00 AM **

“Completed” is not quite the right tag to close this with but it’s certainly not “Declined”.
This topic is now in progress through the F# library https://github.com/fsprojects/FSharp.Control.Reactive/
Please use and contribute to this library, or use Rx directly.
Control.Reactive may well need more work, but from the point of view of the language/core-library design, it is best that people use and contribute to that library.
See also https://github.com/fsprojects/FSharp.Control.AsyncSeq.
Don Syme, F# Language and Core Library Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6427953)**


## Comments ##


#### Comment by Phillip Trelford on 9/12/2014 9:14:00 AM ####
A while back I wrote a small extension library, MiniRx https://minirx.codeplex.com/ with many of the features you suggested which has now been bundled up and maintained in FSharpX: https://github.com/fsprojects/fsharpx/blob/master/src/FSharpx.Core/Observable.fs
It might be interesting to cherry pick some of the methods and add them to FSharp.Core.


#### Comment by Don Syme on 9/16/2014 4:49:00 AM ####
I agree this should be done, though as a full, independent, cross-platform, properly documented F# component and nuget package (e.g. see http://fsharp.org/community/projects). But my opinion is it should not be done in FSharp.Core.
In other words I'd like to see the Observable part stripped out of FSharpx and made into FSharp.Control.Observable nuget component. This should combine the best of the FSharpx.Observable and FSharp>Reactive etc. It can build on Rx if needed.


#### Comment by Don Syme on 10/15/2014 7:48:00 AM ####
There is a relevant community project here: https://github.com/fsprojects/FSharp.Control.Reactive/

