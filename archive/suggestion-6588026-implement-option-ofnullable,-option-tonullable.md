# Implement Option.ofNullable, Option.toNullable [6588026] #

**Submitted by Lincoln Atkinson on 10/20/2014 12:00:00 AM**  
**6 votes on UserVoice prior to migration**  

Various .NET APIs use Nullable<'T> to represent something that might/might not contain data. Having a built-in function to convert to/from F# option type would be quite handy.
See similar suggestion here: /archive/suggestion-6103054-add-option-ofnull-to-help-remove-nulls



## Response ##
** by fslang-admin on 1/21/2015 12:00:00 AM **

Completed for F# 4.0, see https://visualfsharp.codeplex.com/SourceControl/network/forks/dsyme/cleanup/contribution/7672
Don Syme, F# Language/Library Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6588026)**


## Comments ##


#### Comment by Vasily Kirichenko on 10/20/2014 11:33:00 PM ####
Why not to pull all Option.xxx from ExtCore and/or FSharpx then?


#### Comment by Don Syme on 11/10/2014 11:27:00 AM ####
See https://visualfsharp.codeplex.com/SourceControl/network/forks/dsyme/cleanup/contribution/7672

