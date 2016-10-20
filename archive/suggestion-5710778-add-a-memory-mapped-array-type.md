# add a memory-mapped array type [5710778] #

**Submitted by Steven Sagaert on 4/1/2014 12:00:00 AM**  
**5 votes on UserVoice prior to migration**  

Add a memory mapped array similar to what is available in the Julia and Python languages. This would allow to process arrays backed by a binary file that do not fit in RAM (on a single host) transparently as if they did. This would be very useful for scientific programming / machine learning on big data on a single host. The syntax/interface of the array should be the same as a standard array/ distributed array (see my proposal concerning distributed arrays) so that one can transparently switch the implementation from standard array -> mmapped array -> distributed array to scale up from small data/single host -> large data/single host -> large data/multiple hosts to transparently scale in data size & computing power size.



## Response ##
** by fslang-admin on 6/25/2014 12:00:00 AM **

Support for memory mapped files already exists in .NET 4.5 and can be used already.
It’s possible that nicer support can be added for an F#-defined type too. However that should be done in an upstack library like MathNet.Numerics or FSharp.Data or Deedle or elsewhere, rather then in the language and FSharp.Core library.
If you’re interested in contributing some functionality here, http://fslab.org may be a place to do so?
Don Syme, F# Lang


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5710778)**


## Comments ##


#### Comment by Anonymous on 4/2/2014 4:35:00 AM ####
You are aware of the existing support for memory mapped files in .Net? Why not just go and implement the idea?


#### Comment by Don Syme on 6/25/2014 7:03:00 AM ####
Support for memory-mapped files exists in .NET 4.5, e.g. http://msdn.microsoft.com/en-us/library/dd997372(v=vs.110).aspx.
I believe that can be used directly.

