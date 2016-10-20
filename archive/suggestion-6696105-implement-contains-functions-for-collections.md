# Implement 'contains' functions for collections [6696105] #

**Submitted by luketopia on 11/10/2014 12:00:00 AM**  
**5 votes on UserVoice prior to migration**  

Seems like there should be a simple 'contains' function in all the collection modules, e.g.
List.contains
Seq.contains
Array.contains
Right now we have 'exists', but it seems cumbersome to have to do Seq.exists ((=)value) all the time, and this might be confusing to newcomers. I think this is a common enough operation that it merits its own function.



## Response ##
** by fslang-admin on 11/12/2014 12:00:00 AM **

See below, done in F# 4.0


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6696105)**


## Comments ##


#### Comment by Steffen Forkmann on 11/11/2014 2:15:00 AM ####
It's already done - see https://visualfsharp.codeplex.com/wikipage?title=Status

