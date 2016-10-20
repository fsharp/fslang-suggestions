# Have String.ofList in the standard library [9288600] #

**Submitted by Bang Jun-young on 8/12/2015 12:00:00 AM**  
**5 votes on UserVoice prior to migration**  

Wouldn't it be convenient if String.ofList function was part of the standard library? The implementation is quite straightforward:
module String =
let ofList (list: list<char>) =
list |> (System.Text.StringBuilder() |> List.fold (fun sb c -> sb.Append(c))) |> string



## Response ##
** by fslang-admin on 9/7/2015 12:00:00 AM **

see alternative suggestion


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/9288600)**


## Comments ##


#### Comment by Bang Jun-young on 8/14/2015 10:17:00 AM ####
This has been superceded by String.ofSeq. Go to /archive/suggestion-9324276-have-string-ofseq-in-the-standard-library and vote for it!. :-)

