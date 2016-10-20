# modules to extend a DU [7156559] #

**Submitted by Steven Taylor on 3/1/2015 12:00:00 AM**  
**1 votes on UserVoice prior to migration**  

If you extend a DU with a static member, there is no way to define and use Active Patterns or Partial Active Patterns from within such a member. I propose that we create a way to do this.
Otherwise, to group such items under a similar name, we need to come up with a new area.
Say:
type AST = | One | Two
module ASTEx =
If you don't go with a new module, it's possible to overuse the catch all pattern for reasons of convenience:
| _ -> failwith "failed"
It'd be better to default to type safe expression that would warn you to incomplete coverage.



## Response ##
** by fslang-admin on 7/17/2015 12:00:00 AM **

Many thanks for this suggestion. It is being marked as declined – for discussion see the comments above. More details are needed.
Further comments, use cases, information and discussion welcome
Don Syme, F# Language and Core Library Evolution.


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/7156559)**


## Comments ##


#### Comment by Gauthier Segay on 3/1/2015 6:25:00 PM ####
Steve, I'm not understanding the proposal, could you give further details?
I think currently you can add static (and instance) members to the whole DU, is that something which is related to what you would like to have supported?


#### Comment by Steven Taylor on 3/2/2015 3:47:00 AM ####
Yes you can add static members (and instance) members to the whole DU. That's not the issue. What you can't do, to my knowledge, is include active patterns (or partial active patterns) to be used while defining these static / instance member definitions. It'd be nice to be able to do this. I I sometimes cover all cases explicitly... as the _ wildcard hides when the DU has had an additional member placed in it. I like the warning that pops up. When in a module, if you wanted to skip being explicit every time, you might use an Active Pattern (like perhaps there are broad categories in your DU). I think there's an extra opportunity here to place this load onto the compiler. Active Patterns tend tom cut down the amount of effort needed to set-up / maintain your match statements
Does that make sense?


#### Comment by Gauthier Segay on 3/5/2015 3:16:00 PM ####
Steven, I think I understand what you explain about maintaining matches and avoiding _ wildcard (see this where I define a SetTimeout/DontSetTimeout https://github.com/smoothdeveloper/FSharp.Data.SqlClient/commit/dce847e3ab3d189cf414d9bc74b7399a39fdf5a5#diff-84c178c9589f3c3838173d2c2a6988eaR60) but I don't see how this fits in the DU you would have defined.
I think your suggestion would get more thorough feedback if you could make a better sample of the issue with current language, and how adding the feature would fix the usage of _ wildcard or reduce the burden of maintaining the matches.


#### Comment by Don Syme on 6/9/2015 2:05:00 PM ####
Yes, more detail please (as per Gauthier's comment)


#### Comment by Steven Taylor on 3/13/2016 6:41:00 PM ####
you can add static to a DU definition, but not post the definition. Say you've got some recursive DU structure, or simply that you'd like to remove clutter (the statics) from the direct DU definition -- this isn't currently possibly. This can lead to a programming style conflict whereby it is possible to extend general types after-the-fact, but not DUs. A good example of a well written, but a little cluttered DU based structure can be seen in HTML type provider.
It's more the need to have a extra grouping strategies for function to get around such shortfalls.

