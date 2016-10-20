# AddObsoleteAttribute method on ProvidedStaticParameter [7916448] #

**Submitted by Dmitry Morozov on 5/11/2015 12:00:00 AM**  
**3 votes on UserVoice prior to migration**  





## Response ##
** by fslang-admin on 7/17/2015 12:00:00 AM **

This is approved for inclusion in a future release of F# subject to an implementation and detailed design. A pull request
to implement this feature will be necessary and we encourage contributors to submit one with adequate design detail and
testing to http://github.com/Microsoft/visualfsharp. Discussion of the particular version for this to be included in can
be made once an implementation is available.
Design detail can also be discussed below.
Don Syme, F# Language and Core Library Evolution.


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/7916448)**


## Comments ##


#### Comment by Don Syme on 6/9/2015 1:39:00 PM ####
This is entirely reasonable and we would accept a PR to implement this.
Don Syme


#### Comment by luketopia on 7/31/2015 7:07:00 AM ####
I'm confused about what is being suggested here. Are we talking about the ProvidedStaticParameter that's internal to FSharp.Data.TypeProviders.dll? Most type providers I've seen provide their own implementation of ProvidedStaticParameter via their ProvidedTypes.fs. Should an issue be opened on FSharp.TypeProviders.StarterPack instead?

