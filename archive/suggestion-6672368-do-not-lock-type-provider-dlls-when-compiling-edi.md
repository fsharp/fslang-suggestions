# Do not lock type provider dlls when compiling/editing [6672368] #

**Submitted by Gustavo Guerra on 11/6/2014 12:00:00 AM**  
**18 votes on UserVoice prior to migration**  

This is a huge pain in developing type providers.
Maybe it's possible to use the same strategy used for FSI recently?



## Response ##
** by fslang-admin on 2/4/2016 12:00:00 AM **

Declined per comment below – this belongs in Microsoft\visualfsharp or FSharp.Compiler.Service


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6672368)**


## Comments ##


#### Comment by Vasily Kirichenko on 11/6/2014 5:41:00 AM ####
Do you have problems debugging TPs in an Experimental VS instance?


#### Comment by Gustavo Guerra on 11/6/2014 5:59:00 AM ####
It forces you to keep closing and reopening the second VS instance, which is very time consuming.
Additionally, this means that you can't keep the project and the tests in the same solution. For example, in FSharp.Data, if I'm changing anything which is actually not even related to TPs, I have to build, open the test solution, build and run the tests, then close that second solution to be able to do more changes. It completely kills anything even remotely close to TDD


#### Comment by Ben Lappin on 9/29/2015 7:00:00 AM ####
What is Experimental VS?


#### Comment by Don Syme on 2/4/2016 6:05:00 PM ####
I'm closing this in the F# Language User Voice because it's a Visual Studio or FSharp.Compiler.Service issue. Please raise a bug in those repos.

