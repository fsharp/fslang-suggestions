# Have String.ofChars in the standard library [9324276] #

**Submitted by Bang Jun-young on 8/14/2015 12:00:00 AM**  
**10 votes on UserVoice prior to migration**  

Wouldn't it be convenient if String.ofChars function was part of the standard library? The implementation is quite straightforward:
module String =
let ofSeq (seq: char seq) =
seq |> (System.Text.StringBuilder() |> Seq.fold (fun sb c -> sb.Append(c))) |> string
Currently, we have to use an inefficient chaining to convert a seq of characters to a string:
['a'; 'b'; 'c'] |> Array.ofList<char> |> System.String
which can be simplified with String.ofChars:
['a'; 'b'; 'c'] |> String.ofChars
String.ofSeq also can be handy for profiles like PCL where the String type is not regarded as seq<char>.



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/9324276)**


## Comments ##


#### Comment by Don Syme on 2/3/2016 12:06:00 PM ####
Given that this would be pretty low-performance in any case, the use of StringBuilder appears adequate to cover this case.

