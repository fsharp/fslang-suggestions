# Featurize static optimization literals [5663116] #

**Submitted by Alex Rønne Petersen on 3/21/2014 12:00:00 AM**  
**18 votes on UserVoice prior to migration**  

I understand that the inline IL feature is discouraged because it depends on compiler implementation details, but it seems like static optimization literals would be genuinely useful and also portable across (potential) compilers, yet they are currently disallowed outside of the core library.
Would it make sense to featurize them so they're usable everywhere?



## Response ##
** by fslang-admin on 2/4/2016 12:00:00 AM **

Declined per my comment below
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5663116)**


## Comments ##


#### Comment by Will Smith on 3/21/2014 5:53:00 PM ####
Inline IL is interesting, but it should always be discouraged because we don't need a habit of using it. If we use F#, it should be just F#. The kind of optimizations that you would want to gain from inline IL, the F# compiler optimizer should give you that. If it can't, then a change to the optimizer would be needed.


#### Comment by Alex Rønne Petersen on 9/27/2014 3:31:00 AM ####
Just to be clear, inline IL is a separate thing from static optimization literals. What I meant is that while inline IL should not be featurized, static optimization literals are perfectly useful and portable - I see no reason that those should be disallowed outside FSharp.Core.
I worded it that way originally because FSharp.Core tends to use inline IL alongside static optimization literals, but static optimization literals are useful in more general situations too.


#### Comment by Michael on 11/12/2014 5:34:00 PM ####
Yes and they should have the syntax streamlined, too. I should be able to write:
let inline foo f (x: ^a) = x.Foo f
And have it "just work" and infer the syntax. Versus having to use the strange member-accessing syntax for every member used.
Also, lambdas should be inlineable. I should be able to do "xs |> iter (fun x -> x + 1)" and have it compile to equivalent code as if I just did a loop.


#### Comment by exercitus vir on 6/19/2015 6:08:00 PM ####
I agree that lamdas should be inlined.


#### Comment by Don Syme on 2/4/2016 11:21:00 AM ####
This feature is unsafe to use and can interact badly with type inference and generalization if used incorrectly. For this reason we definitely decided to keep it to be FSharp.Core-only in F# 1.0 onwards.
My inclination is to stick with this decision since there's been no specific change of circumstance.

