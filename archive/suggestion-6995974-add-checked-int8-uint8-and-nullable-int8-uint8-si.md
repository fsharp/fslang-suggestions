# Add Checked.int8/uint8 and Nullable.int8/uint8/single/double [6995974] #

**Submitted by Don Syme on 1/22/2015 12:00:00 AM**  
**1 votes on UserVoice prior to migration**  

This is the tracking issue for https://github.com/Microsoft/visualfsharp/pull/19
F# defines "int8" and "uint8" as synonyms for "sbyte" and "byte", both as types and operators. While reviewing the behaviour of "open Checked" (which brings new versions of operators into scope) we noticed that new versions of the "int8" and "uint8" operators are not defined in the "Checked" module. This is inconsistent, though a simple workaround is to use the checked "sbyte" and "byte" operators instead.
We also noticed that "Nullable.int8" and "Nullable.uint8", "Nullable.single" and "Nullable.double" are missing.
The proposal is to add these.



## Response ##
** by fslang-admin on 7/17/2015 12:00:00 AM **

Completed, see https://github.com/Microsoft/visualfsharp/pull/19


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6995974)**


## Comments ##

