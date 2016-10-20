# Add a shorthand/literal syntax for creating Maps [12536532] #

**Submitted by Brad Collins on 3/1/2016 12:00:00 AM**  
**3 votes on UserVoice prior to migration**  

A shorthand/literal syntax or computation expression for building Maps would be nice—something like the following:
let m = map ["a",97; "b",98; "c",99]
The shorthand for dictionaries ...
let d = dict ["a",97; "b",98; "c",99]
... is nice, but while Maps implement IDictionary, dictionaries do not play well with Map module functions. One must inevitably convert a dictionary to a Map or create a Map with Map.ofArray, .ofList, or .ofSeq.



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/12536532)**


## Comments ##


#### Comment by amazingant on 3/7/2016 6:15:00 AM ####
You can add this yourself fairly easily by adding the following anywhere in your code:
let map = Map.ofList
and then your first code sample works


#### Comment by Brad Collins on 3/7/2016 9:08:00 AM ####
@amazingant, no argument that it's an easy fix, but its seems like an obvious oversight (and perhaps even that's too strong a word) when we have shorthand for every other built-in F# container: lists, sequences, arrays, and sets. As someone who came to the language just a little over a year ago, I found it incongruous for map shorthand to be missing.


#### Comment by AK on 3/10/2016 3:41:00 PM ####
You can already do this
i.e Map [("Key", "Value); ("Key2", "Value2")] works fine in my code. Notice the capital M on Map


#### Comment by Brad Collins on 3/10/2016 5:31:00 PM ####
@ak, ah, I see! I am embarrassed that I had not explored that option. But I see now that it's merely a call to the Map constructor.
I will quibble that the style is inconsistent. That is, it's set [ ... ] for sets, dict [ ... ] for dictionaries, seq [ ... ] for sequences, but it's Map [ ... ] for maps. That inconsistency is not satisfying.
Nevertheless, I concede the point that a shorthand clearly already exists. I just overlooked it.

