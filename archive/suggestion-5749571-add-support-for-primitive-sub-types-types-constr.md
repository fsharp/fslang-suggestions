# Add support for primitive sub-types (types constrained by sub-ranges or length) [5749571] #

**Submitted by exercitus vir on 4/9/2014 12:00:00 AM**  
**16 votes on UserVoice prior to migration**  

Please add support for sub-types like Ada which are enforced by the F# compiler. A sub-type is basically just a sub-range of an existing primitive type like int.
This is extremely useful for domain modelling and makes code much more robust.
Examples using existing range syntax or existing for-loop syntax or :
//restrict range (specify min value and max value)
type percent = decimal for 0M to 1M //for-loop syntax
type positive_int = int in 1 .. int.MaxValue //range syntax
type non_negative_int = int for 0 to int.MaxValue //for-loop syntax
//a positive_int should be assignable to a non_negative_int
//specify minimum and maximum length of string
type path = string for 1 to 256 //for-loop syntax



## Response ##
** by fslang-admin on 2/4/2016 12:00:00 AM **

Declined per my comment below: this feature almost immediately leads you to dependent types, see the comments here: /archive/suggestion-6062821-add-dependent-types


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5749571)**


## Comments ##


#### Comment by Tony Williams on 4/16/2014 4:58:00 AM ####
Wouldn't dependent typing also solve this? If so then hopefully the work on F* could be used here.


#### Comment by Patrick Q on 5/1/2014 7:12:00 AM ####
Wish I could give more votes. Ever since I saw this in Ada I've always thought it would such a useful feature to have in F#. Certainly agree that it would enhance safety and robustness.


#### Comment by Don Syme on 9/16/2014 5:53:00 AM ####
Just to note that this feature is very difficult to add to F# satisfactorily, and quickly leads you towards full dependent types.

