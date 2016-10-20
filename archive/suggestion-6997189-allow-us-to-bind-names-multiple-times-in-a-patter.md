# Allow us to bind names multiple times in a pattern match [6997189] #

**Submitted by Richard Gibson on 1/22/2015 12:00:00 AM**  
**3 votes on UserVoice prior to migration**  

Why not allow us to use the same name multiple times in a pattern? I find myself writing code like this an awful lot:
match a with
| Some (x, y, z) when x = y && y = z && x = z ->
printfn "Something interesting"
| _ -> printfn "Something boring"
As shorthand for exactly this, why can't I write:
match a with
| Some (x, x, x) -> printfn "Something interesting"
| _ -> printfn "Something boring"



## Response ##
** by fslang-admin on 2/14/2015 12:00:00 AM **

This was considered in F# 1.0-2.0 but was not included.
Among other things, the various notions of equality in F# (and indeed any programming language) are sufficiently subtle that it is better if uses of equality checks are made explicit at some point in the code.
So while the feedback is appreciated, this kind of extension is beyond the scope of what we would consider for the F# language at this point.
Thanks
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/6997189)**


## Comments ##


#### Comment by Isaac Abraham on 1/24/2015 8:38:00 AM ####
Because you're binding those fields to specific values for use on the right hand side of the -> - it's not for equality checks.


#### Comment by luketopia on 2/8/2015 7:44:00 AM ####
I think this is a reasonable proposal. It's not contradictory to bind multiple values to a single pattern variable if they are equal. It's reads nicer than the when guard.


#### Comment by Marcus Magnusson on 2/8/2015 8:33:00 AM ####
I agree, I think this would be nice. Shows intention very clearly. I believe this is supported in Erlang, and the little experience I have of Erlang hasn't shown me any drawbacks to this.

