# Add 'except' function to core collection modules [7068430] #

**Submitted by luketopia on 2/8/2015 12:00:00 AM**  
**7 votes on UserVoice prior to migration**  

In C# you can do
xs.Except(ys)
Without defining a function, the F# equivalent is
xs |> Seq.filter (fun x -> ys |> Seq.exists ((=)x) |> not)
Of course, with the F# 4.0 collection normalization you can replace "Seq.exists ((=)x)" with "Seq.contains x".
If you convert to a Set first then there's Set.difference but the problem is that it is not in correct order for partial application so can't be used in a pipeline, and the other argument also needs to be a set.



## Response ##
** by fslang-admin on 4/9/2015 12:00:00 AM **

This proposal has been accepted and completed as part of F# 4.0, see https://github.com/Microsoft/visualfsharp/pull/253#issuecomment-87232623
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/7068430)**


## Comments ##


#### Comment by Anonymous on 2/8/2015 9:33:00 AM ####
If we add this, then it needs to be done for array, seq and list.


#### Comment by Don Syme on 2/14/2015 12:14:00 PM ####
This is a reasonable suggestion.
An implementation of this for Seq, Array and List with full testing and performance analysis on empty, small and large inputs would be needed (with appropriate optimizations when the inputs are arrays or ICollection), and testing under a range of inputs to check that F# equality semantics are being used. Performance comparisons with the LINQ implementation should also be made.
Although this wasn't on the list of functions for F# 4.0 FSharp.Core 4.4.0.0 update, if you're quick about a PR we could still consider it for that release. Even if it isn't accepted for that release (indeed, it is quite possible it wouldn't be), it would still be useful to have the PR prepared and in place for some later library update.
Don


#### Comment by luketopia on 2/14/2015 5:04:00 PM ####
Thanks for the response! I think this would be a good first PR for me but it probably won't make it on time due to other things I'm working on, plus needing to get the CLA signed.


#### Comment by David Obadz on 2/15/2015 5:34:00 AM ####
xs |> Seq.filter (not << flip Set.contains (set ys)) <= wish we didn't need the flip..


#### Comment by Patrick McDonald on 2/20/2015 3:52:00 AM ####
I've create a PR on github for this: https://github.com/Microsoft/visualfsharp/pull/253
The implementations suggested here are different from the LINQ implementation, as LINQ removes duplicates from the results.

