# Make the .Tag property public in DUs [5736822] #

**Submitted by Eirik George Tsarpalis on 4/6/2014 12:00:00 AM**  
**3 votes on UserVoice prior to migration**  

A common problem I encounter is when I need to group a list of incuming DU values according to branch. Having the .Tag property public would make this as simple as writing
values |> Seq.groupBy (fun v -> v.Tag)
At the moment, this can only be achieved either by cumbersomely defining a custom tag function or by using reflection.
For the ML purists that don't like the idea of a property, this could also be achieved through the definition of a static method, for instance
UnionType.GetInternalBranchRepresentationValue : UnionType -> int



## Response ##
** by fslang-admin on 6/25/2014 12:00:00 AM **

Merging this with /archive/suggestion-5683698-make-is-discriminated-union-properties-visible-f
This is not actually being declined, quite the opposite, it is being approved and merged


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5736822)**


## Comments ##


#### Comment by Don Syme on 6/20/2014 11:57:00 AM ####
I generally approve of this particular suggestion and think it would make a good addition to F#. (I don't think the loss of purity (e.g. wr.t. ordering of union cases) is a critical problem and I believe you can turn of the DefaultAugmentation in any case)
Some technical issues may need to be ironed out during implementation.
If this is done, the Is* properties present on these types should also be revealed, that is covered by a separate item.
An implementation and testing would need to be provided by someone in the F# community (possibly including Microsoft or Microsoft Research, though not limited to them).
Implementations of approved language design can now be submitted as pull requests to the "fsharp4" branch of https://visualfsharp.codeplex.com/SourceControl/latest.
I'd be glad to help guide people through the implementation process.
If you strongly think this should _not_ be approved please chime in with your technical feedback.
Thanks
Don Syme, current BDFL for F# Language Design

