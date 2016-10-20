# Allow record types to implement interfaces just by adding the interface name when compatible [12838959] #

**Submitted by Pierre Irrmann on 3/7/2016 12:00:00 AM**  
**32 votes on UserVoice prior to migration**  

When a record type already has all the members necessary to impement an interface, it could implement it without having to write the code.
For instance:
type IHasAnAge =
abstract member Age: int
type Person = {
Name : string
Age: int
} with interface IHasAnAge



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/12838959)**


## Comments ##

