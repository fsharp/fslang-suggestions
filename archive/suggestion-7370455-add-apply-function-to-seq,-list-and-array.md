# Add `apply` function to Seq, List and Array [7370455] #

**Submitted by David Torbonof on 3/29/2015 12:00:00 AM**  
**6 votes on UserVoice prior to migration**  

Simply a function a la
let apply (mapping: 'T -> 'U) (source: seq<'T>) : seq<'T * 'U> = source |> Seq.map (fun x -> (x, mapping x))
This would for instance be useful when creating graphs like
[0. .. 0.01 .. 1.] |> Seq.apply sin |> plot



## Response ##
** by fslang-admin on 7/17/2015 12:00:00 AM **

Many thanks for this suggestion. It is being marked as declined – for discussion see the comments above.
Further comments, use cases, information and discussion welcome
Don Syme, F# Language and Core Library Evolution.


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/7370455)**


## Comments ##


#### Comment by Don Syme on 6/9/2015 1:53:00 PM ####
I feel this is more a convenience function than something to have in the core. Also, is
[ for x in 0 .. 0.01 .. 1.0 -> (x,sin x) ]
too much?
Cheers
Don Syme

