# Make records extensible a la Elm [8592088] #

**Submitted by Boris on 6/28/2015 12:00:00 AM**  
**14 votes on UserVoice prior to migration**  

It seems very useful when types don't fully defined in advance, but I don't sure if it is possible in F#.
http://elm-lang.org/guide/core-language#records



## Response ##
** by fslang-admin on 2/3/2016 12:00:00 AM **

Closing in favour of the more conrete proposal at /archive/suggestion-9633858-structural-extensible-records-like-elm-concrete


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/8592088)**


## Comments ##


#### Comment by Xavier Zwirtz on 6/29/2015 3:02:00 PM ####
This could be accomplished by type providers if it was possible for type providers to return records.


#### Comment by Boris on 6/30/2015 7:37:00 AM ####
Type Providers is a (only) design/compile-time story, and extensible records is a run-time one.
For exampe in AI applications like an Expert System You (your users) have no VS nor Type Providers and still have to introduce new concepts wich can(definitely will) affect types. Working with external data sources that mutated somehow after You used Type Providers without recompilation is at least problematic. With extensible records we could have almost dynamic languages flexibility.
Please look at http://elm-lang.org/docs/records for the ext rec details.


#### Comment by Anonymous on 8/13/2015 11:43:00 AM ####
Worth pointing out that the idea comes from Microsoft Research's own Daan Leijen. The link below to elm includes a link to the paper "Extensible records with scoped labels", but I will add it here for convenience -- seems to solve quite a few problems very naturally: http://research.microsoft.com/pubs/65409/scopedlabels.pdf


#### Comment by trek42 on 9/5/2015 12:38:00 AM ####
Added a more elaborate proposal for this: see /archive/suggestion-9633858-structural-extensible-records-like-elm-concrete


#### Comment by Don Syme on 2/3/2016 12:27:00 PM ####
Closing in favour of the more elaborate proposal at /archive/suggestion-9633858-structural-extensible-records-like-elm-concrete

