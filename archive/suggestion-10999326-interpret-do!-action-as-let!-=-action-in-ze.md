# interpret `do! action` as `let! () = action in zero` when the Builder has no Return defined [10999326] #

**Submitted by Max Malook on 12/7/2015 12:00:00 AM**  
**3 votes on UserVoice prior to migration**  

In general there are two types of workflows represented by computation expressions:
1) process (async)
2) sequential (seq)
The former usually uses return or return!, the later yield and yield!.
With asyncSeq it's actually a combination of both worlds, but the main purpose is to be sequential, and also allow side effects to happen (do! Async.Sleep 200).
Currently `do! action` is interpreted as `let! () = action in return ()`, with this the Builder has to provide the Return method. With it in place also return keyword becomes available.
In case of asyncSeq the result of `return expr` is completely ignored, what can lead to inconvenience for the users of asyncSeq.
The proposal is to interpret `do! action` as `let! () = action in zero` when the Builder do not provide a Return method.
With it return keyword would be unavailable to the users of the Builder.
Original discussion: https://github.com/fsprojects/FSharp.Control.AsyncSeq/issues/38



## Response ##
** by fslang-admin on 1/23/2016 12:00:00 AM **

This PR has been merged, so this design item is completed, though not yet released in a specific version of F#
This is approved for F# 4.1+. It’s the right adjustment to the language given the problem discussed in the linked gituhb thread
See also the proposed implementation here: https://github.com/Microsoft/visualfsharp/pull/773
Don Syme
F# Language and Core Library Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/10999326)**


## Comments ##

