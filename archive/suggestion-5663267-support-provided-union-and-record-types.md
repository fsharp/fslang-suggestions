# Support Provided Union and Record Types [5663267] #

**Submitted by Gustavo Guerra on 3/21/2014 12:00:00 AM**  
**111 votes on UserVoice prior to migration**  





## Response ##
** by fslang-admin on 2/4/2016 12:00:00 AM **

Marking as “approved in principle” (it will show as “planned”).
However, in reality it is both relatively low priority and relatively hard to implement, so I don’t expect this to happen any time soon.
For example, we would have to reverse-map the metadata associated with F#-specific types. This is already done in F# reflection FSharpType.IsRecord and so on.


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5663267)**


## Comments ##


#### Comment by Jack Pappas on 3/22/2014 8:30:00 AM ####
What limits you from generating DUs and Records in type providers now? Is the limitation in the F# compiler itself, or in the ubiquitous ProvidedTypes.fs? If it's the latter, this feature could be implemented through a community effort.


#### Comment by Keith Battocchi on 4/10/2014 8:21:00 AM ####
@Jack - it's a compiler limitation (there's no way to provide the metadata that the F# compiler uses to recognize F#-specific types).


#### Comment by mavnn on 5/7/2014 4:45:00 AM ####
Yes please for this one; let's allow TPs to create idiomatic F# apis!


#### Comment by Don Syme on 2/4/2016 12:35:00 PM ####
I plan to mark this feature as "approved in principle" (it will show as "planned"). It would be great if it were done.
However, in reality it is both relatively low priority and relatively hard to implement, so I don't expect this to happen any time soon.
For example, we would have to reverse-map the metadata associated with F#-specific types. This is already done in F# reflection FSharpType.IsRecord and so on.

