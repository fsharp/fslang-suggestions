# Query expression array and list syntax [5681770] #

**Submitted by Phillip Trelford on 3/26/2014 12:00:00 AM**  
**2 votes on UserVoice prior to migration**  

For brevity instead of
query { (*... body *) } |> Seq.toList
allow
query [ (* body *) ]



## Response ##
** by fslang-admin on 2/3/2016 12:00:00 AM **

Declining per the comment from Don Syme below


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5681770)**


## Comments ##


#### Comment by Keith Battocchi on 4/10/2014 8:36:00 AM ####
As a workaround, you can also add a suitable ToList extension member to QueryBuilder and put it into the query itself, which looks a bit cleaner than piping to Seq.toList.


#### Comment by ADMIN
fsharporg-lang (F# Software Foundation Language Group, F# Software Foundation) on 2/3/2016 2:43:00 PM ####
The use of Seq.toList or the workaround below seems adequate for this case.

