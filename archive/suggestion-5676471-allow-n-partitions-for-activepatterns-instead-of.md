# Allow n partitions for ActivePatterns instead of a max 7 [5676471] #

**Submitted by Steven Taylor on 3/25/2014 12:00:00 AM**  
**23 votes on UserVoice prior to migration**  

Active patterns can only have seven partitions (see: http://msdn.microsoft.com/en-us/library/dd233248.aspx)
It would be good if this was a stylistic constraint that could be overridden if desired.
For example, if active patterns are getting used to split up XML nodes meaningfully, you aren't in control of how many nodes sensibly fit into the top level.



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5676471)**


## Comments ##


#### Comment by Jack Pappas on 3/28/2014 6:05:00 PM ####
I have often wished for F# to have this feature. I would be OK if the compiler required active patterns with >7 cases to be inlined -- most of the time I've wanted to use this, the active pattern would only be used in 1 or 2 places in the code, and I've mainly wanted to use an active pattern to take advantage of the exhaustivity checking provided by the compiler.


#### Comment by Mickey on 11/10/2014 10:42:00 AM ####
640K. That'll be enough!


#### Comment by bleis-tift on 11/7/2015 8:04:00 PM ####
type Choice<'T1> =
| Choice1Of1 of 'T1
type Choice<'T1, 'T2, 'T3, 'T4, 'T5, 'T6, 'T7, 'TRest> =
| Choice1OfN of 'T1
| Choice2OfN of 'T2
| Choice3OfN of 'T3
| Choice4OfN of 'T4
| Choice5OfN of 'T5
| Choice6OfN of 'T6
| Choice7OfN of 'T7
| ChioceRest of 'TRest
let (|P1|P2|P3|P4|P5|P6|P7|P8|) x =
match x with
| 1 -> P1
| 2 -> P2
| 3 -> P3
| 4 -> P4
| 5 -> P5
| 6 -> P6
| 7 -> P7
| _ -> P8
// Chice<unit, unit, unit, unit, unit, unit, unit, Choice<unit>>
This is the same way as the System.Tuple.


#### Comment by Don Syme on 2/10/2016 11:06:00 AM ####
As an aside, we looked at implementing this in F# 2.0 and it seems that it became surprisingly hard very quickly. I can't quite remember the details though.

