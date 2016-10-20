# Easier to copy data between records of different types. [6124011] #

**Submitted by Matthew Moloney on 7/1/2014 12:00:00 AM**  
**32 votes on UserVoice prior to migration**  

Large data projects require lots of records with 100+ fields. These records require small changes over time, e.g. a new field is added. To update the data the old records are read in and copied to the new record field by field. The proposal is to automatically copy fields from an old record of type A to a new record of Type B where both the field names and the field types match.
type A = {x : int}
type B = {x : int; y : int}
let a : A = {x = 1}
let b : B = {a with y = 2}



## Response ##
** by fslang-admin on 2/3/2016 12:00:00 AM **

Closing in favor of /archive/suggestion-5663704-copy-and-update-on-class-types


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6124011)**


## Comments ##


#### Comment by Dax Fohl on 5/25/2015 9:54:00 AM ####
I'd extend this idea to also make it easier to *create* records of different types.
type A = {x: int}
type B = {A with y:int}


#### Comment by Don Syme on 2/3/2016 1:16:00 PM ####
This is very much related to /archive/suggestion-5663704-copy-and-update-on-class-types
I will close this suggestion in favour of that one and link back here

