# Allow "as" in match head [9829650] #

**Submitted by mikero on 9/19/2015 12:00:00 AM**  
**6 votes on UserVoice prior to migration**  

I always seem to be doing this, which seems natural, but isn't allowed:
match ((fn h) as res) with
| ...



## Response ##
** by fslang-admin on 1/23/2016 12:00:00 AM **

See comment above,
Don Syme, F# Language and Core Library Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/9829650)**


## Comments ##


#### Comment by mikero on 9/19/2015 11:19:00 AM ####
BTW, the reason is that if there are many following complex matches then you wouldn't need to wrap each in a "(...) as res" to capture the original un-de-structured result.


#### Comment by Paulmichael Blasucci on 9/28/2015 3:56:00 PM ####
If you're using this in a lot of match cases, maybe using a local binding before the match would be easier...
let res = fn h
match res with
| ...


#### Comment by mikero on 9/28/2015 7:44:00 PM ####
But that's a whole extra line, dude :)
Seriously though, it's not big deal, but seems consistent with allowing these in assignments and pattern matches.
They could just be allowed anywhere:
if (fn h) as res = 42 then printfn "%d" res


#### Comment by Don Syme on 1/23/2016 11:58:00 AM ####
I don't think this adds enough to really be necessary in the language. I'm marking as declined, though thank you for the suggestion.

