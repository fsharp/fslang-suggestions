# Make let optional [5681764] #

**Submitted by Phillip Trelford on 3/26/2014 12:00:00 AM**  
**3 votes on UserVoice prior to migration**  

Make F# even more terse by removing the requirement for the let keyword, particularly on local variables.



## Response ##
** by fslang-admin on 2/5/2016 12:00:00 AM **

Thanks for the suggestion, though declined per my comment below
Best regards
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5681764)**


## Comments ##


#### Comment by Jon Harrop on 3/26/2014 5:26:00 AM ####
How would you distinguish between the definition x=2 and the test for equality x=2?


#### Comment by Patrick Q on 3/28/2014 7:37:00 PM ####
I've made a related suggestion that doesn't completely get rid of "let", but allows a single let to create multiple bindings. This is similar to how "where" in Haskell can group together a number of bindings. See "Allow a single let to create multiple bindings" for details.


#### Comment by Eamon Nerbonne on 6/21/2014 3:04:00 AM ####
Go uses a slightly different operator to distinguish assignment from definitition with assignment - F# could use a slightly different operator to distinguish definition from equality.


#### Comment by Don Syme on 2/3/2016 2:57:00 PM ####
I propose to decline this. A completely revamped F# syntax may choose to make let optional. But I don't think it is really technically feasible within the current F# syntax.


#### Comment by Ideaflare on 5/14/2016 8:29:00 AM ####
I think it's a great idea!
But I agree that making things optional opens up the door for multiple ways of doing the same thing, which adds unnecessary cognitive load for maintainers.
My suggestion is - that if it is optional, that it is a toggle feature that requires all code per-project(or solution) mandatory to have let, or mandatory to not have the let for that project, but not to be able to mix let and no let in the same project.

