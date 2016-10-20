# Provide a concise and performant item+index for loop ("with index") [7098665] #

**Submitted by mikero on 2/15/2015 12:00:00 AM**  
**2 votes on UserVoice prior to migration**  

It's a very common pattern to want to get an item and its index, especially for code that is meant to be performant.
Currently (AFAIK) to get the index and item from a sequence or collection you must use iteri() (or Zip with a range) -- this causes code to become syntactically less clear (esp. when nested) and is less performant than adding a mutable counter inside each loop:
seq1 |> Seq.iteri (fun index item ->
...
seq2 |> Seq.iteri (fun index2 item2->
...)
...)
I suggest that a for loop with an additional "with" clause:
for item with index in seq1
....
or
for item in seq with index
....
The advantage of this syntax is that (a) it uses the existing "with" keyword and (b) it does not conflate the index with the user's data as the tuple used in iteri does.
This would be roughly equivalent to:
let mutable index = 0
for item in seq do
...
index <- 1 + index
However, the goal would eventually be for the compiler in the case of native collections (arrays, lists, etc.) to avoid the call the iterator and access successor items directly, as the C# compiler foreach does in some cases.
One could imagine that this pattern could be extended by the user (a la workflows) to provide a richer item than an index - such as an object that provides a mutator/zipper function, etc., but that a whole other kettle of fish.



## Response ##
** by fslang-admin on 2/3/2016 12:00:00 AM **

Declined in favour of using Seq.indexed in F# 4.0, see comment below


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/7098665)**


## Comments ##


#### Comment by Don Syme on 6/9/2015 2:13:00 PM ####
I've often wanted something in this zone for F# comprehension syntax. I'd appreciate additional feedback on this proposal and ideas about alternative syntaxes


#### Comment by Don Syme on 2/3/2016 2:46:00 PM ####
In F# 4.0 Seq.indexed has been provided as a marking combinatory, please use that.

