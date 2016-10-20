# Make FSharp.Core collection functions for Array.Parallel more regular [5665432] #

**Submitted by Jon Harrop on 3/21/2014 12:00:00 AM**  
**63 votes on UserVoice prior to migration**  

In F# 3.0, lots of standard functions are missing from Array.Parallel including tryFindIndex, exists, forall, filter, tryFind, reduce, minBy, maxBy and tryPick. A mapReduce function would also be useful.
Efficient implementations of all of these have been described in the F# Journal. http://fsharpnews.blogspot.co.uk/2013/01/parallel-aggregates.html



## Response ##
** by fslang-admin on 2/4/2016 12:00:00 AM **

Approved in principle subject to RFC and well-tested implementation being submitted as PR.


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5665432)**


## Comments ##


#### Comment by Don Syme on 2/4/2016 12:41:00 PM ####
I am going to mark this as "approved in principle". That is, we would accept design additions with well-tested implementations of coherent subsets of these functions.
If someone would like to submit a PR for these that would be great.

