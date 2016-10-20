# Expand on cardinality functions Seq.exactlyOne, with Seq.tryExactlyOne and add oneOrMore, zeroOrMore [16308904] #

**Submitted by Abel on 9/22/2016 12:00:00 AM**  
**7 votes on UserVoice prior to migration**  

While it is quite trivial to write these functions, I think they have merit. First of, it is good there's a Seq.exactlyOne, but it throws and if you want a non-throwing version, you'll have to write one your own. It's odd there's a creator function, Seq.singleton, but not a test-function.
Since we have Seq.exactlyOne, it should have its logical cardinality counterparts for zero-or-one and one-or-more to be available too.
I suggest we add:
Seq.tryExactlyOne
Seq.oneOrMore (throws)
Seq.zeroOrMore (throws)
Seq.tryOneOrMore
Seq.tryZeroOrMore
The reason it is better to have these in FSharp.Core is that, if one implements these by hand, it requires at least two iterations until the 2nd element. An optimized implementation may prevent this.
See also the discussion here: http://stackoverflow.com/questions/39628567/non-throwing-version-of-seq-exactlyone-to-test-for-a-singleton-sequence



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/16308904)**


## Comments ##

