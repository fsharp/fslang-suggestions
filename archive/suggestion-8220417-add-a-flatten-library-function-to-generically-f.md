# add a 'flatten' library function to generically flatten a tree to a sequence [8220417] #

**Submitted by lr on 6/3/2015 12:00:00 AM**  
**3 votes on UserVoice prior to migration**  

I need this function in most of my projects in one way or another, so I always copy/paste it. It's not a big hassle, but I think it is general enough to warrant inclusion in the std lib.
The idea is to traverse a tree by passing a 'root' and a function to extract the 'children'. This works for both actual tree types and anything logically representing a tree like the directory structure.
Sample Usage:
get all files from directory and subdirectories in a single line:
"c:\test" |> flatten Directory.GetDirectories |> Seq.collect Directory.GetFiles |> Seq.toArray
sample implementation:
let rec flatten func source = seq {
yield source
for x in func source do
yield! flatten func x
}
I got the general idea from these SO Posts:
http://stackoverflow.com/questions/10253161/efficient-graph-traversal-with-linq-eliminating-recursion
http://stackoverflow.com/questions/11830174/how-to-flatten-tree-via-linq
Since F# has yield!, we don't need to explicitly use Stack<'T> like in C#.



## Response ##
** by fslang-admin on 7/17/2015 12:00:00 AM **

Many thanks for this suggestion. However, I’m declining this for the reasons given in the comments above.
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/8220417)**


## Comments ##


#### Comment by Don Syme on 6/9/2015 12:48:00 PM ####
While the function is a fine thing, I don't think it fits with the current F# core library design by itself - there is no generic library of tree-traversing or tree-mapping functions - instead you write an appropriate for your tree type.
It is also not easy to make a one-size fits all function. For example, even for this function in many cases it would be better to return the flattened tree as an array or list, rather than a on-demand sequence.
Don Syme, F# Language and Core Library Evolution


#### Comment by George on 6/10/2015 10:35:00 AM ####
Why not bring the tree into the standard collections conversion treatment
Seq.ofTree : (parser: 'node -> 'node seq) (root: 'node)

