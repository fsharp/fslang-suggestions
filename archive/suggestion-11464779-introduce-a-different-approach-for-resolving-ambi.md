# Introduce a different approach for resolving ambiguity of record types [11464779] #

**Submitted by Kevin Rood on 1/15/2016 12:00:00 AM**  
**3 votes on UserVoice prior to migration**  

See the example here under the "Conflict Resolution" heading:
http://davefancher.com/2012/11/27/f-record-types/
Prefixing the type on a label seems inconsistent with how types are annotated elsewhere in the language. Perhaps something like this with the type annotation on the end would be more consistent:
"let myRecord = {} : RecordTypeName"



## Response ##
** by fslang-admin on 1/23/2016 12:00:00 AM **

Yes, as noted in the comments a type annotation can already be used.
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/11464779)**


## Comments ##


#### Comment by Bill Hally on 1/19/2016 6:32:00 AM ####
You can already do this as follows:
"let myRecord : RecordTypeName = {...}"


#### Comment by Kevin Rood on 1/23/2016 7:44:00 AM ####
Very helpful, thank you. I can't recall seeing that elsewhere.

