# comment in supporting files [8998102] #

**Submitted by Steven Taylor on 7/23/2015 12:00:00 AM**  
**0 votes on UserVoice prior to migration**  

if code is self documenting, adding comments later for API purposes gets in the way of readability. Padding out with comments also gets in the way of a well crafted level of code density. Therefore it'd be nice to be able to comment functions in supporting files, and to have a mechanism for VS / F# to both maintain these links, and link to the relevant information for intenseness purposes.
Additionally, a transitive, find inherited comment would be quite useful too. VS could have a InheritedIntellisense tag.
Perhaps a code merge as a part of the build process would suffice.
The idea of sprinkling comments in code for automatic document generation, although useful, seems back-to-front for an actively maintained code base (assuming good tooling support). It'd be nice to separate things out and to have things flowing in the reverse direction too.



## Response ##
** by fslang-admin on 2/3/2016 12:00:00 AM **

zero votes, declined


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/8998102)**


## Comments ##


#### Comment by luketopia on 7/27/2015 8:18:00 PM ####
Have you looked into F# signature files? These allow you to have your API comments in a separate file from your implementation, just as you described.
https://msdn.microsoft.com/en-us/library/dd233196.aspx

