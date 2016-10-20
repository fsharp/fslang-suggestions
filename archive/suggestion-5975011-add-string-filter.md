# Add String.filter [5975011] #

**Submitted by Patrick Q on 5/27/2014 12:00:00 AM**  
**4 votes on UserVoice prior to migration**  

The absence of a filter function from the String module is a major deficit for the usefulness of the String module. It already supports map, mapi, iter and iteri, so it seems quite strange that filter is missing. Not having a filter function means that we have to turn the string into an array (or seq/list), do the filtering and then convert back to a string, resulting in complicated and convoluted code.
As map, mapi, iter and iteri already exist it would seem that most of the core machinery already exists, so it shouldn't be too difficult to add a filter function.
I would like add that a filter function would actually be more useful for string processing that map and iter, so it's absence is all the more puzzling.



## Response ##
** by fslang-admin on 11/8/2014 12:00:00 AM **

This work has been completed for the “fsharp4” branch, see https://visualfsharp.codeplex.com/SourceControl/network/forks/marten_range/visualfsharp/contribution/7255
Thanks
Don Syme, current BDFL for F# Language Design


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5975011)**


## Comments ##

