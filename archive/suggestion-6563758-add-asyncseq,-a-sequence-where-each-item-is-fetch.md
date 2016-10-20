# Add AsyncSeq, a sequence where each item is fetched asynchronously [6563758] #

**Submitted by Daniel Bradley on 10/15/2014 12:00:00 AM**  
**6 votes on UserVoice prior to migration**  

Incorporate asynchronous sequences with associated module (with similar methods to the Seq module) and computation expression builder.
Existing implementations:
FSharpx: https://github.com/fsprojects/fsharpx/blob/master/src/FSharpx.Core/AsyncSeq.fs
ExtCore: https://github.com/jack-pappas/ExtCore/blob/master/ExtCore/Collections.AsyncSeq.fs



## Response ##
** by fslang-admin on 7/18/2015 12:00:00 AM **

Completed through the library linked in the comments


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6563758)**


## Comments ##


#### Comment by Alfonso Garcia-Caro on 10/15/2014 3:45:00 AM ####
Using event streams in an ordered fashion seems to be the best fit for AsyncSeq, but as async APIs increase they may have other uses and it make sense to add them to the core. For example, I'm using them to handle async cursors in the HTML5 IndexedDB API.


#### Comment by Don Syme on 2/14/2015 11:56:00 AM ####
I believe this should be done as an independent nuget package. It is extremely useful.
I would recommend creating a new project at http://github.com/fsprojects/FSharp.Control.AsyncSeq and just getting this under way


#### Comment by Don Syme on 7/18/2015 1:38:00 PM ####
This is addressed through http://github.com/fsprojects/FSharp.Control.AsyncSeq. Please use that library.

