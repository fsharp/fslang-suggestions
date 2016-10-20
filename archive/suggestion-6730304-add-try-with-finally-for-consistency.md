# Add try-with-finally for consistency [6730304] #

**Submitted by Anonymous on 11/17/2014 12:00:00 AM**  
**3 votes on UserVoice prior to migration**  

F# supports try-with, try-finally, but not try-with-finally.
I know this can be workarounded, and that it is sometimes requested, but I think that for consistency it is a *nice to have* to be on par with C#.
http://stackoverflow.com/questions/2078603/f-exception-handling-constructs
http://stackoverflow.com/questions/1789682/how-do-i-ignore-exceptions-in-f



## Response ##
** by fslang-admin on 7/18/2015 12:00:00 AM **

Many thanks for this suggestion. It is being marked as declined – for discussion see the comments.
Further comments, use cases, information and discussion welcome
Don Syme, F# Language and Core Library Evolution.


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6730304)**


## Comments ##


#### Comment by Don Syme on 11/17/2014 8:35:00 AM ####
Hey Denis,
Do you think there is something more than consistency with C# as a rationale?
I guess I don't see any intrinsic reason why using a nested try/with is not clearer to reason about and keeps the constructs more orthogonal. Combining two orthogonal constructs into a single combined syntax isn't really normal - there has to be an intrinsic reason for it. I'll admit I've never quite understood _why_ C# needed to do this - I always thought it came from first supporting multiple "catch" blocks (because they didn't have pattern matching in exception handlers), and then they just tacked on an optional "finally" and/or "fault" block.
Mashing constructs together into a single construct can make things harder for the user, as they will expect that there is some semantic reason for offering the combination - i.e. there is something special that can only be done by the combined syntax.
Also, try/finally are really pretty rare in F# due to the use of "use" in async, sequences etc.


#### Comment by Steffen Forkmann on 11/17/2014 9:08:00 AM ####
there is a PR with a sample implementation for discussion: https://visualfsharp.codeplex.com/SourceControl/network/forks/OkayX6/visualfsharptools/contribution/7701


#### Comment by Sergey Tihon on 11/17/2014 1:09:00 PM ####
Agreed with Don here, I also do not understand why we need this.
I do not remember when I needed try-finally actually


#### Comment by Marc Sigrist on 11/27/2014 8:17:00 AM ####
When I first saw the F# try... with/finally rules, I thought they were strange, because I was used to C#. However, in practice, this has never bothered me during four years of F# programming. I can't remember when I actually used try...finally in F#. And now that I have read Don's answer below, the F# implementation also makes sense to me from a language coherence point of view. Thus, I am not in favor of adjusting to C#.

