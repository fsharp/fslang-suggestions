# Code clarity: Remove Object Pascal-style for ... to|downto ... do ... loops from the language (from Swift) [13302753] #

**Submitted by Alexei Odeychuk on 4/4/2016 12:00:00 AM**  
**4 votes on UserVoice prior to migration**  

The for ... to|downto ... do ... loop appears to be a mechanical carry-over from Object Pascal rather than a genuinely F#-specific construct. The for ...to|downto ... do ... loops do not lend themselves to use with sequences and other core F# types supporting IEnumerable interface. It is rarely if ever used in pro-level apps. More F#-typical construction is already available in the language with the for ... in ... do ... loop that has much better readability and expressiveness.
Example # 1:
// it provides equivalent behavior to: for i = 1 to 100 do ...
for i in 1 .. 100 do ...
// it provides equivalent behavior to: for i = 100 downto 1 do ...
for i in 100 .. -1 .. 1 do
Example # 2: Clear advantage in using the for … in … do … loop compared to the for … to|downto … do … loop in expressiveness
// some complicated expression to generate a sequence
let sq = seq { 1 .. 2 .. 999 }
(*........*)|> Seq.filter (fun item -> item <= 199 || item >= 501)
// simply try each item of the sequence supporting
// IEnumerable interface
for s in sq do …
Removing the for .. to|downto ... loops would simplify the language. The value added of this construct is limited and I believe its gradual removal from F# should be seriously considered.
Alternative to be considered:
Not removing the for ... to|downto ... do ... loop from F#, losing the opportunity to streamline the language and discard an unneeded control flow item.
Approach suggested:
I suggest that the for ... to|downto ... do ... loop be deprecated in F# vNext and removed entirely in F# vNext vNext.



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/13302753)**


## Comments ##


#### Comment by Alexei Odeychuk on 4/4/2016 5:09:00 AM ####
Removing the for .. to|downto ... loops would mean the removal of the unneeded "to" and "downto" keywords from F#.


#### Comment by Vasily Kirichenko on 4/10/2016 1:03:00 PM ####
Nothing can be removed from the language.


#### Comment by Alexei Odeychuk on 4/11/2016 4:16:00 AM ####
Vasily, obsolescences and deletions are part of the history of programming languages. Some features are identified as obsolescent; some features are deleted from programming languages in the course of time.
The languages are rid of rarely used or unsafe features, borrows new features from others in order to survive, boost their competitive strengths, and be modern after all.
Features removal occurs not only in old programming languages like Fortran (list of obsolescent and deleted features in Fortran: https://en.wikipedia.org/wiki/Fortran#Obsolescence_and_deletions), but also in new languages that are actively developed, for example, Swift (Remove C-style for-loops with conditions and incrementers. Status: Accepted for Swift 3.0: https://github.com/apple/swift-evolution/blob/master/proposals/0007-remove-c-style-for-loops.md).
I believe it would be OK to deprecate and then remove the rarely-if-ever-used for ... to|downto ... do ... loop from the language.
I think the list of obsolescent and deleted features has to be an integral, normal part of the F# programming language specification.

