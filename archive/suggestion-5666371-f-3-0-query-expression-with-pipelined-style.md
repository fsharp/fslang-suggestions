# F# 3.0 query expression with pipelined style [5666371] #

**Submitted by Anonymous on 3/22/2014 12:00:00 AM**  
**10 votes on UserVoice prior to migration**  

http://visualstudio.uservoice.com/forums/121579-visual-studio/suggestions/2715068-f-3-0-query-expression-with-pipelined-style



## Response ##
** by fslang-admin on 2/5/2016 12:00:00 AM **

Thank for the suggestion. Declined per my comment, please take a look
Thanks
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5666371)**


## Comments ##


#### Comment by Anonymous on 3/22/2014 2:07:00 AM ####
The idea title should be F# query expression with pipelined style
dataSource
|>Sql.where (fun a->a.ColumnA)
|>Sql.sortBy (fun a->a.ColumnB)
|>Sql.skip 10
|>Sql.take 20
|>Sql.run
|>Seq.iter (fun a->printfn "%s" (string a.ColumnA))


#### Comment by Don Syme on 2/5/2016 4:12:00 AM ####
You can actually do this as a library today if you try hard enough. Just make Sql a type and each of the functions a method that takes a quotation as an argument implicitly.
Either way, this belongs in a library not in FSharp.Core.

