# Allow upcast in type test pattern (inside computation expression) [10596684] #

**Submitted by Sehnsucht on 11/7/2015 12:00:00 AM**  
**1 votes on UserVoice prior to migration**  

See this SO subject along with Tomas response ; that convey pretty well what i mean (as my english is rubbish).
http://stackoverflow.com/questions/33585508/why-this-for-type-test-pattern-fails



## Response ##
** by fslang-admin on 1/23/2016 12:00:00 AM **

See comment above
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/10596684)**


## Comments ##


#### Comment by Don Syme on 1/23/2016 11:47:00 AM ####
Perhaps I don't fully understand the suggestion. However essentially we decided against this in the design of computation expressions, instead the recommendation is to use "match" if doing a runtime type test, and ":>" if doing a static cast.

