# Allow Attributes to follow the `member` keyword [11628951] #

**Submitted by Jared Hester on 1/28/2016 12:00:00 AM**  
**1 votes on UserVoice prior to migration**  

instead of just -
[<DebuggerStepThrough>]
member __.ReturnFrom (value: 'T option) : Async<'T option> = async.Return value
and -
[<DebuggerStepThrough>] member __.ReturnFrom (value: 'T option) : Async<'T option> = async.Return value
^ which causes indentation issues for following definitions without attributes
allow -
member [<DebuggerStepThrough>] __.Zero () : Async<unit option> = Some () |> async.Return



## Response ##
** by fslang-admin on 2/3/2016 12:00:00 AM **

Declines see comment above
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/11628951)**


## Comments ##


#### Comment by Don Syme on 2/3/2016 10:36:00 AM ####
Thanks for the suggestion
However I will decline this: what we have works, and the proposed saving is only one line, and the lines become loooong. In balance I don't see a net benefit.

