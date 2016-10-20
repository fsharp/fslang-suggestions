# Add slicing syntax to F# lists [6642034] #

**Submitted by Don Syme on 10/31/2014 12:00:00 AM**  
**1 votes on UserVoice prior to migration**  

The F# list type already supports an index operator, xs.[3]. This is done despite the fact that lists are linked lists in F# - lists are just so commonly used in F# that in F# 2.0 it was decided to support this.
Since an index syntax is supported, it makes sense to also support the F# slicing syntax, e.g. xs.[3..5]. It is very strange to have to switch to an array type to use slicing, but you don't have to make that switch for indexing.



## Response ##
** by fslang-admin on 11/8/2014 12:00:00 AM **

This has been approved as an F# 4.0 language feature, and the implementation has been completed here: https://visualfsharp.codeplex.com/SourceControl/changeset/83106bf0f7d1984b8a52c4d2219f68faaba1693d. (This fslang.uservoice.com entry was added mainly for tracking, visibility and discussion)


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6642034)**


## Comments ##

