# Add "lengthBy" function to Seq/Array/List [6466039] #

**Submitted by Patrick Q on 9/21/2014 12:00:00 AM**  
**7 votes on UserVoice prior to migration**  

Currently there is no function that returns a number representing how many elements in a specified collection satisfies a condition.
For instance consider what we need to do to count the number of odd numbers in a list:
let numbers = [ 5; 4; 1; 3; 9; 8; 6; 7; 2; 0 ]
let oddsCount = numbers |> List.filter (fun n -> n % 2 = 1) |> List.length
It would be much more efficient and convenient to have a lengthBy function to allow the following:
let oddsCount = numbers |> List.lengthBy (fun n -> n % 2 = 1)
Getting a count based on a predicate is such a fundamental operation that I believe there should be a single dedicated function. In C# for instance there is an overload for the Count method that provides this functionality and it's equivalent absence in F# appears to be a bit of an oversight.



## Response ##
** by fslang-admin on 10/15/2014 12:00:00 AM **

I’m marking this as declined since it is not included in the F# 4.0 FSharp.Core design. However please feel free to continue the discussion.
Don Syme


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6466039)**


## Comments ##


#### Comment by Sergey Tihon on 9/21/2014 7:11:00 AM ####
I think countBy do this job. So Seq.countBy is already available, so you can write
let oddsCount = numbers |> Seq.countBy (fun n -> n % 2 = 1)
countBy is planned for List and Array - see here https://github.com/fsharp/FSharpLangDesign/blob/master/CoreLibraryFunctions.md
PR is here https://visualfsharp.codeplex.com/SourceControl/network/forks/forki/fsharp/contribution/7079#!/tab/comments


#### Comment by Patrick Q on 9/21/2014 8:58:00 AM ####
Sergey, I initially had the same thought as you did, but the existing CountBy function provides very different functionality. For a given sequence, the result is sequence of tuples. Each tuple represents the result of the supplied function and the associated count.
So for "let oddsCount = numbers |> Seq.countBy (fun n -> n % 2 = 1)", the result is the sequence: seq [(true, 5); (false, 5)]. The proposed lengthBy function would simply return 5, representing the number of odd numbers in the collection.


#### Comment by Don Syme on 10/15/2014 7:38:00 AM ####
This has been discussed in this thread : https://github.com/fsharp/FSharpLangDesign/issues/36
My conclusion is that adding "Where" variations of functions - e.g. countWhere, mapWhere etc. is not appropriate given the explosion of variations this would cause.
Please feel free to continue the discussion here.

