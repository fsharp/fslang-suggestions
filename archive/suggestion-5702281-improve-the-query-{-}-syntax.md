# Improve the query { ... } -syntax [5702281] #

**Submitted by Tuomas Hietanen on 3/30/2014 12:00:00 AM**  
**12 votes on UserVoice prior to migration**  

Three ideas of the new query{ ... } -syntax:
1) Do something for the amount of white space needed for new line as the arrow "->" can't break the line!
As the tutorial shows, there is like one word per line:
http://www.tryfsharp.org/Learn/data-science#further-data-analysis
2) Improve the syntax: Now it is weird and have more noise than SQL or LINQ. So I even rather use LINQ-to-IQueryable in F# than F#'s own query-syntax. This can be done By making as simple query {...} as possible and then use Linq-library to manipulate it further.
3) Make it compile-time-aware of capacities of the queryed interface. For example, Azure Table Storage won't support most of the queries:
http://msdn.microsoft.com/en-us/library/windowsazure/dd135725.aspx



## Response ##
** by fslang-admin on 2/5/2016 12:00:00 AM **

Thanks for the suggestions! Per my comment and the other comments, I’m declining this, please take a look at the links.
One reason for declining was that some of the suggestions were not that concrete. Please open new issues if there are specific changes proposed
Many thanks
Don Syme, F# Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5702281)**


## Comments ##


#### Comment by Loic Denuziere on 3/31/2014 8:39:00 AM ####
1) you can perfectly break the line before or after "->". In the linked example this works just fine:
Chart.Point([for cy in cyclonesWithFatalities ->
cy.``Highest winds``.Value,
cy.``Total fatalities``.Value])
(in case the whitespace gets mangled: the "cy..." lines are indented further than the start of "for")
2) Do you have concrete examples?
3) I agree with this one, it would be nice.


#### Comment by Don Syme on 2/5/2016 6:47:00 AM ####
My feeling is that the solution to these problems is not in modifications to the "query" feature but in taking alternative approaches to querying. For example:
The Azure Storage Type Provider shows a better way to have queries when the query language is limited: http://fsprojects.github.io/AzureStorageTypeProvider/
The SqlCommandProvider shows how to do checked SQL directly using type providers: http://fsprojects.github.io/FSharp.Data.SqlClient/

